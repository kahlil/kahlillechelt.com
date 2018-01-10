---
title: "Switching To hyperHTML And HyperHTMLElement"
date: 2018-01-10
---

When starting work on Static Site CMS I originally planned on using Custom Components and lit-html instead of a JavaScript framework. 

In the process of setting up my development environment I was a little annoyed to realize that lit-html can only be used with ES Modules and not with CommonJS modules. Since Electron uses CommonJS that is a requirement for my current project. 

I heard that hyperHTML basically does the same thing as lit-html so I went and checked it out.

I was very happy to discover that not only does hyperHTML do basically the same thing as lit-html, it also supports all module types and as a bonus there is a little ecosystem around it that enhances Custom Elements and even supports server side rendering. What?! Nice! See a chart that compares the two [right here](https://gist.github.com/WebReflection/fadcc419f5ccaae92bc167d8ff5c611b).

[HyperHTMLElement](https://github.com/WebReflection/hyperHTML-Element) is a Custom Element subclass that is exactly what I just had started to do with [LitElement](https://github.com/kahlil/kaf/blob/master/js/util/lit-element.js), only better. The author [@WebReflection](https://www.twitter.com/WebReflection) knows these emerging web standards very well and does an amazing job making them really usable and useful today.

In turn @WebReflection [is not a fan of TypeScript](https://github.com/WebReflection/hyperHTML/issues/107#issuecomment-339651380) so neither hyperHTML nor HyperHTMLElement have type definitions. 
Since I decided to use TypeScript in my app I created a simple type definition file for HyperHTMLElement. I didn't add it to @types yet but you can grab it [from my project right here](https://github.com/kahlil/static-site-cms/blob/master/types/hyperhtml-element/index.d.ts).

All in all lit-html and hyperHTML are very similar in what they do. The biggest difference at the moment is that hyperHTML is more complete and feels more mature, not to mention the addition of HyperHTMLElement and server side rendering via [ViperHTML](https://viperhtml.js.org/viper.html).



