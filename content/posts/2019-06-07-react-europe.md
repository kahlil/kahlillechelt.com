
---
date: 2019-06-07T15:33:30.451Z
title: "I was at ReactEurope and now I \"get\" React Hooks"
---

Last week, I went to Paris to spend some time there with my family and to attend ReactEurope. 

Based on the kind of mediocre design of their website I did not expect a lot of care to go into the organization of the conference. I expected a dull conference room in a hotel and some interesting talks. 

I got some interesting talks and a dull, stuffy conference room in a dull, ugly area of Paris. The room was too small for so many people though. The air was terrible and people coughing and sneezing all around me. I was not capable of spending a lot of time in there.

Instead, I took some time to read through the [React Hooks documentation](https://reactjs.org/docs/hooks-intro.html). Let me just take a second to say how well written and how thought-out the documentation is. Really world-class. Unlike the ReactEurope conference. 

I also started rewriting [my Grit editor](https://github.com/kahlil/grit) from [Preact](https://github.com/preactjs/preact) and [htm](https://github.com/developit/htm) to React with hooks. Just so to get familiar with them. 

It is always hard to convey how features like that impact your development experience without trying it out. I have only rewritten a small part of it so far but I like it a lot. 

The concept of custom hooks especially seems to have a lot of impact when it comes to simplifying your code. 

Here is an example. 

In order for Grit to work the user has to store the path to their Markdown files in the settings. I store the settings by using this ace package called electron-store by Sindre Sorhus (Shout out to him, what would I do without his stellar open source work?!).

This path needs to be shown in the UI via a state variable and it has to be synced back to the electron-store if it is changed. 

So I created this custom hook called useElectronStore to read the path from electron-store and to set the filePath state variable from it and to set both, the state variable and electron-store, with the new value once it is changed. 

And it makes getting and setting electron-store values incredibly easy. The API basically looks like this: 

```
const [someValue, setSomeValue] = useElectronStore('someValue', '');
```

The `'someValue'`-string is the path in electron-store and the second value is the default value for it. 

I can now say that I "get" React Hooks because ReactEurope was not that great. Works for me. 






