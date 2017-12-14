---
title: "Use Web Components To Build JavaScript Apps"
date: 2017-12-14
---

Web Components are generally described as ["custom, reusable, encapsulated HTML tags"](https://www.webcomponents.org/introduction) that encapsulate some DOM, some styling and behavior implemented with JavaScript.

I don't understand why this use case is pushed so extensively when Web Components offer a perfectly good component abstraction for building complete JavaScript web apps.

I'm not so much interested in Web Components for individual new custom tags à la `<google-maps></google-maps>` or something. I'm interested in using Web Components for building full fledged JavaScript apps with a component-tree architecture, unidirectional data flow and efficient DOM rendering. And I think they are perfect for it!

And they are perfect for it _now_. 

Web Components are typically described as the combination of the following four web standards: 

- Custom Components
- Shadow DOM
- HTML Template
- HTML Imports

First of all let's forget about HTML Imports. Vendors don't agree on them, they block rendering and honestly they feel super clunky to me.

We have ES Modules. Web Components don't work without JavaScript anyway so let's import them via ES Modules or bundle them up and serve them from a server or CDN. 

Mikeal Rogers actually [already built a solution](https://medium.com/@mikeal/ive-seen-the-future-it-s-full-of-html-2577246f2210) for himself that allows him to write Web Components in JavaScript, publish them to npm and automatically serve them automatically on a CDN via unpkg.

That's totally the way to go. But he also talks about isolated components as far as I can see.

Like I said I think they are the perfect building blocks for building JavaScript web apps how we build them today with React, Vue, Angular and so on.

My opinionated list of things that of what Web Components consist looks like this.

- Custom Components (with Shadow DOM and HTML Template behind the scenes)
- Tagged Template Literals

Custom Components are the heart. They are the building blocks for web applications. Shadow DOM should always be used for encapsulation and HTML Template should be used to efficiently build the DOM for the component. 

The developer should really just interact with a Custom Component class without having to think about Shadow DOM and the HTML Template.

What Custom Components are missing is an efficient way to automatically update the DOM on component state changes.

Basically something like React‘s vDOM.

But adding a vDOM library doesn’t feel right because one of the big wins of Web Components is that you don’t have to manage a separate DOM next to the one in the browser. So what to do?

While watching the talks of the 2017 Polymer Summit I stumbled on [this talk about lit-html](https://www.youtube.com/watch?v=ruql541T7gc) and I was impressed by it right away.

It’s a genius little 2k-sized library that goes with Web Components beautifully. It allows you to build the DOM for your Custom Component with a tagged template literal.

Tagged Template Literals are a JavaScript standard. They are Template Literals that are marked by a function name. The string contained in the Template Literal is processed by that function before it's returned. In the case of lit-html it looks like this: 

```js
const markup = html`
  <div>
    ${state.someValue}
  </div>
`;
```

lit-html comes with the `html`-function to use with Template Literals and with a `render` function that efficiently renders updated state to the DOM.

Under the hood lit-html uses HTML Template to efficiently clone the markup. The `html` function returns something called a `TemplateResult` which gets passed to the `render` function along with the DOM element to which it should be rendered. lit-html remembers the dynamic parts of the template and makes sure these get updated when needed. The static parts of the template are always just rendered once.

According to [this talk from the Google Web Summit](https://youtu.be/Io6JjgckHbg?t=1254) lit-html fairs pretty well performance-wise.

I think it is the perfect library for managing DOM updates of Custom Components because it it just uses Web Standards to do its job and refrains from maintaining a second DOM tree in order to be fast. 

With a little luck some sort of efficient DOM updating will also land in the browser as a standard but for now this is great!

So in conclusion: the perfect web app building block for me is just a Custom Component that uses a base class that hides away creating the Shadow DOM and the usage of lit-html. 

[I made such a subclass](https://github.com/kahlil/kaf/blob/master/js/util/lit-element.js) for [my little Café search app](https://kaf.kahlillechelt.com), it's called `LitElement` and it is str8 🔥.

```js
// A super chill custom element subclass with
// some nifty default behavior.
export class LitElement extends HTMLElement {
  constructor() {
    super();
    // Initialize the state variable.
    this.state = {};
    // Create the Shadow DOM for this element.
    this.attachShadow({ mode: 'open' });
    // Just a convenient alias for addEventListener
    this.on = this.addEventListener;
  }
  
  // The state getter.
  get state() {
    return this._state;
  }
  
  // The state setter calls the 
  // invalidate function, which invalidates the
  // state and calls render.
  set state(s) {
    this._state = s;
    this.invalidate();
  }

  // This function makes sure that 
  // the lit-html render function is called 
  // when invalidate() is called. 
  // But it makes sure it is always called 
  // on next tick so that render calls are 
  // batched.
  invalidate() {
    if (!this.needsRender) {
      this.needsRender = true;
      Promise.resolve().then(() => {
        this.needsRender = false;
        // this.render is the render function of 
        // the Custom Component that subclasses this
        // class and it returns a TemplateResult created
        // with the lit-html html-function and a Tagged 
        // Template Literal. 
        // The location to which the DOM is rendered to is
        // always the shadow root of the component.
        render(this.render(this.state), this.shadowRoot);
      });
    }
}
```

❤️ the platform.
