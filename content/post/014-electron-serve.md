---
title: "electron-serve"
date: 2018-01-26T00:00:00Z
---

In a default setup, Electron serves the app's index.html file directly from disk with the `file://` protocol. This does not work well with JavaScript apps that want to use client-side routing. 

The browser does not support `history.pushState` for files served from disk. This means every time you navigate to a different route with a client-side router it will try to resolve the path on disk which leads to a 404. 

Thankfully earlier this year, [@sindresorhus](http://twitter.com/sindresorhus) published [electron-serve](https://github.com/sindresorhus/electron-serve). This package registers a custom file protocol called `app://` with a slightly tweaked behavior to `file://`: 

It serves a file if it exists and serves index.html as a fallback if it doesn't. 

This makes it possible for client-side routers to process routes and for the app to respond to them without having to spin up a server in your Electron app. 

One thing I had to do to get it to work though was to pass a fully resolved path to the `require` call for my entry file. I used `path.resolve` to do that. It did not work with a regular relative path like `require('./renderer')`.

