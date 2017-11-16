---
title: "Web Components And The CMD-R Development Workflow"
date: 2017-11-16
---

A couple of months ago I stumbled across Mikeal Rogers' article [I’ve seen the future, it’s full of HTML.](https://medium.com/@mikeal/ive-seen-the-future-it-s-full-of-html-2577246f2210) in which he lays out his reasons why he started to dive into Web Components for the web apps he is working on right now and hinted to the workflow he uses. 

His enthusiasm for Web Components is infectious and because I have a lot of respect for Mikeal and his work, his article was a strong signal for me personally that Web Components might be something to take a closer look at. 

I have ignored them so far because the little I knew about them seemed a little gross to me: HTML imports? HTML, CSS and JavaScript in one file? Ewww. Who wants to write code like that? 

Polymer didn't help a lot either: all I heard was Polyfills and Bower and WTF is Shady DOM? 

And oh yeah everybody kept screaming "OH PRAISETH OUR NEW LORD AND SAVIOR HIS HOLINESS THE REACT". 

So I kept ignoring it. 

But then Mikeal came along and showed how to write Web Components purely with JavaScript. He said the only tooling he uses is a little Browserify in order to package the component so he can distribute it via npm and automatically serve it via a CDN.

I was like: "No tooling? Hmmm... that sounds pretty sweet."

A few weeks ago I took some time to write a tiny application just with Web Components. I used no tooling, no compilation no polyfills, no nothing. Just Chrome, ES 2015+, ES Modules, `<template>`, Custom Elements and an "actions up data down" data flow with Custom Events.

I used the CMD-R (CTRL-R on Windows) web development workflow as Alex Russel calls it. 

Now that's a _developer experience_ 😉!

It was surprising to me how freeing it was to be able to use modern syntax, modules and a component architecture in the browser without any tooling. Not to mention the excellent debuggability since you are feeding the browser what you write directly. 

The browser has become the only tool and even the only "framework" we need to write JavaScript apps. 

Just write your app using Chrome and then make a bundle with dynamically loaded polyfills to make it work everywhere. 

As it stands currently that latest versions of Google Chrome, Safari and Opera support these technologies natively, Firefox and Edge are lagging behind but working on it. 

