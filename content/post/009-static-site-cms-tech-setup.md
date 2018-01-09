---
title: ""
date: 2018-01-05
draft: true
---

For me, Web Components are the way to go when building things with JavaScript. I have written about it here and here. So when I started setting up my development environment for Static Site CMS I planned to use lit-html and Custom Components. 

In the process of doing that I realized that I can't really use lit-html because Electron uses CommonJS for module imports and lit-html only supports ES Modules. So I took a look at hyperHMTL, which is very similar to lit-html. 

It turns out that hyperHTML is actually further along and then some and can do everything lit-html can do and more. Check out [lit-html vs hyperHTML](https://gist.github.com/WebReflection/fadcc419f5ccaae92bc167d8ff5c611b).

On top of that there is also HyperHTMLElement which does what I started doing with LitElement and more. Both of these products are pretty far along and I love what I am seeing. 

Since I am just supporting one version of Chrome in Electron I don't have to worry about polyfills or anything. It just works.

- I'm using TypeScript
- Made a type def file for HyperHTMLElement
- PostCSS with a few plugins
- BEM + ITCSS
- npm scripts: npm-run-all ftw
- 

