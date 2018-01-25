---
title: "Keeping TypeScript Benefits In A JavaScript Project With Visual Studio Code"
date: 2018-01-25T00:11:10Z
tags: ["Building Grit"]
---

When I started [Grit](https://www.producthunt.com/upcoming/grit) I was excited to find out that the Electron team is shipping types with Electron which expose the Electron API in your tooling. Since I am a fan of TypeScript I set up my dev environment to write my code in TypeScript as well.

After a few days of writing TS code to transpire it for my app I started to get annoyed with the fact that I am transpiling code. And here is the reason:

In Electron you write code for very capable browser. ES2015 is fully implemented minus ES Modules. That means the code I can write for the browser directly is already so close to ideal for me that it felt wrong to transpile from something else. So I converted my project back to JavaScript. 

After years of dealing with Babel and TypeScript, writing ES2015+ code directly for the browser feels very freeing.

No source maps to decode, no types to manage. 

Losing the types would be a little annoying though. For me personally in a this one-man-project I enjoy the types especially because they enhance the tooling. 

Thankfully there is VSCode!

VSCode has introduced something that is called [`jsconfig.json`](https://code.visualstudio.com/docs/languages/jsconfig). It's a configuration file that tells VSCode that the folder containing it is a JavaScript project.

From [code.visualstudio.com](https://code.visualstudio.com/docs/languages/jsconfig): 

> `jsconfig.json` is a descendent of `tsconfig.json`, which is a configuration file for TypeScript. `jsconfig.json` is the `tsconfig.json` with the `"allowJs"` attribute set to true.

Adding that file tells VSCode to turn on the [JavaScript Language Service](https://github.com/Microsoft/TypeScript/wiki/JavaScript-Language-Service-in-Visual-Studio) which is based on the TypeScript Language Service. This gives you powerful Intellisense features throughout the project. 

This means you get autocompletion and type errors for a normal JavaScript project. Types are being inferred by TypeScript type definition files as well as JSDoc comments. 

## Setting up jsconfig.json For Electron

In order to get it to work satisfyingly for my Electron setup I had to configure a few things.
jsconfig.json is just a tsconfig.json so the options are the same.

First of all I excluded `node_modules` since I don't want VSCode to type check all my dependencies. 

```
"exclude": ["node_modules"]
```

In the `compileroptions` property I set the `checkJs` property to `true` so that the JavaScript code is type checked as much as possible.

Because I (have to) use CommonJS Modules in Electron I had to set the `module` property to `commonjs` so that `index.js` files are resolved CommonJS-style.

And last but not least in order to be able to write ES2015+ code without warnings I set the `target` property to `es2017`.

You can have a look at my config file [right here](https://github.com/kahlil/grit/blob/master/jsconfig.json). 

## Adding A Type Definition For HyperHTMLElement

I had to create a type definitions file for HyperHTMLElement because the JavaScript Language Service didn't like me having to use the `default` property on the required module. This is the code in question:

```
const HyperHTMLElement = require('hyperhtml-element').default;
```

I went to the trouble to actually add all the class properties in the definition which gives me the sweet sweet code completion feature in VSCode. If you need it you can pick it up from [here](https://github.com/kahlil/grit/blob/master/types/hyperhtml-element.d.ts).

This setup allows me to write modern JavaScript code directly for the browser as well as benefit from many TypeScript features. Love it.






