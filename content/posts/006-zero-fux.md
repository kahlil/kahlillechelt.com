---
title: "ZeroFux - A Stateless Unidirectional Data Flow Implemented With Custom Events"
date: 2017-12-20
---

Undirectional Data Flow, Flux, Redux, Whateverux is essentially this: 

- something happens 
- what happened is being described with an action object
- that action object is being dispatched through a central point, the dispatcher
- on the other side of that dispatcher actions are matched to reducers 
- the reducers take the information of the actions and return state

This allows you to manage interactions in your UI in a stateless and synchronous manner.

As a developer, the only thing that really interests you are the actions and the reducers, all the rest is just implementation detail. Actions and reducers shape the app‘s state.

In the following I describe a really simple way how you can implement this type of state management with Custom Events.

## Actions

First let’s define what an action is. An action is a JavaScript object that has one required property with the key  „type“ and two optional ones with the keys „payload“ and „error“. Here an action defined as a TypeScript interface.

```
{
  type: string;
  payload?: any;
  error?: boolean;
}
```

I think we can agree that the JavaScript community mostly agrees on this definition pioneered by Redux, maybe minus the `error` property. I stole that from `redux-observable`.

## Dispatcher

So, now that we have actions how do we dispatch them through the dispatcher and what is the dispatcher?

We want to use Custom Events. Those event get dispatched on a DOM element with the `dispatchEvent` method. That means our dispatcher is a DOM element. It is really not important which one but let’s just use the `body` element since that element is present on any web app.

```
const dispatcher = document.querySelector('body');
```

Great. Now that we have the dispatcher how do we dispatch an action? That’s where the Custom Events come in. We‘re using Custom Events because they allow us to add Custom event data (which we will, sneakily, call actions).

```
dispatcher.dispatchEvent(
  // The first argument of the Custom Event is 
  // the event name. The event name is the same
  // as the action type.
  // The second argument are options.
  new CustomEvent('SOME_ACTION', {
    // Here goes our custom data, the action object.
    detail: { 
      // Action type and event name are the same.
      type: 'SOME_ACTION', 
      // Here goes the optional data.
      payload: someData, 
      error: false,
    },
  })
)
```

So now that all these actions are being piped through one point in the DOM via Custom Events, we can match them to reducers. 

In your component that expects some some state, take an array of action names that the component is interested in and set up event listeners. In the event listeners callback match a reducer with the same name per action to update the component state: 

```
// Some example action names.
const ACTIONS = [
  'INCREMENT',
  'DECREMENT',
  'ADD_TEN',
];

...

// As a convention components need a setter and 
// a getter for the state property. 
// That allows you to call a render function or similar
// whenever state is set to a new value.
set state(s) {
  this._state = s;
  // Use lit-html or some other library that efficiently
  // can update DOM in the render function. 
  this.render();
}

get state() {
  return this._state;
}

// This is a method on some component.
setReducers() {
  ACTIONS.forEach(ACTION => {
    if (reducers[ACTION]) {
      // Again we are using the reference to the body
      // element as the dispatcher.
      dispatcher.addEventListener(ACTION, e => {
        // Reducers are kept in an object and matched
        // via action name.
        this.state = reducers[ACTION](e.detail, this.state);
      });
    } else {
      throw new Error(
        `Please add a reducer for the "${ACTION}" action.`
      );
    }
  });	
}

...

```

## The ZeroFux Library

The code above is a little boilerplate-y so let's make a simple library out of it. 
No Flux plus no Redux euquals ZeroFux:

```
export class ZeroFux {
  constructor(element) {
    if (element) {
      this.dispatcher = element;
    } else {
      this.dispatcher = document.querySelector('body');
    }
  }

  // The dipatch method takes an action argument
  // of the previously defined action type.
  dispatch(action) {
    this.dispatcher.dispatchEvent(
      new CustomEvent(action.type, {
        detail: action,
        // In case you set a custom dispatcher element
        // and want them to bubble.
        bubbles: true,
        // In case your custom dispatcher is in the
        // Shadow DOM and you want them to bubble between
        // the borders or Shadow DOM and regular DOM.
        compose: true,
      })
    )
  }

  // This method takes an array of action types
  // that can influence a component's state,
  // an object with reducers with the same names
  // as the action types and a reference
  // to the component on which we want to set
  // the state propery.
  setReducers(actionTypes, reducers, component) {
    actionTypes.forEach(actionType => {
      if (reducers[actionType]) {
        this.on(actionType, e => {
          const action = e.detail;
          component.state = reducers[actionType](component.state, action);
        });
      } else {
        throw new Error(
          `Please add a reducer for the "${actionType}" action.`
        );
      }
    });
  }
}

export const zeroFux = new ZeroFux();
```

🎉 tadaa!

It's up on [Github](https://github.com/kahlil/zero-fux) and [npm](http://npmjs.org/zero-fux) right now if you want to try it. 

You can see ZeroFux in action in this [CodePen](https://codepen.io/kahlil/pen/bapoPK).

## Side Effects

"Ah-haaa! How do we manage side effects with ZeroFux?", you may ask. Well, there is actually a <strike>simple</strike> zero-fux way to deal with this. 

Since these custom events are all streaming through one point in the DOM, the point that we can access via `zeroFux.dispatcher`, we can just listen to these events separately and fire effects on certain actions.

These side effects have to fire an action themselves when they are done with whatever they were doing. That's how we introduce data coming from theses side effects synchronously back into the the data flow. 

This is how your SideEffects class could look:

```
import { zeroFux } from 'zero-fux';

export class SideEffects {
  run() {
    const on = zeroFux.dispatcher.addEventListener;
    on('SOME_ACTION', () => { 
      someApi.doSomethingAsync()
        .then(data => zeroFux.dispatch({
          type: 'SOME_RESPONSE_ACTION',
          payload: data,
        }));
    });
    
    ...
  }
}
```

See it in action in the [CodePen](https://codepen.io/kahlil/pen/bapoPK).

## Conclusion
So there it is, a bare bones, straight forward unidirectional data flow implementation using custom events. 

It uses the same principle I have also used in oddstream, a unidirectional data flow library implemented with RxJS: matching  a "stream of actions" to reducers. This just has zero dependencies and is practically no code.

In Node this could be implemented using `EventEmitter`.

I think this solution for a unidirectional data flow could be used in apps of any size because ultimately all you have to manage and think about is actions and reducers, same as in any other unidirectional data flow solutions. 







