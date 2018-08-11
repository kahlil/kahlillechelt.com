---
date: 2018-08-10T15:30:40+02:00
title: "belly FAQ: Y U NO USE ALIASES?"
---

Some people react to what I am doing with [*belly*](https://github.com/kahlil/belly) with the question why I didn't use Git aliases or bash aliases.
It is true, that the general behavior could have been implemented using aliases. But even in its current MVP-state belly does more than I comfortably could cover with aliases.

## The Spinner
In order to show that belly is working, I am using a command line spinner. The spinner has different states and shows different text for those different states. 

Clearly this could have been done with bash scripts of some sort but yeah, why would I do that?

I am JavaScript developer so I use the tools that I am comfortable with, to make things. 

Also *whoop whoop* for npm because that said spinner is actually a ridiculously useful and powerful npm package by none other than the one Sindre Sorhus called [*ora*](https://github.com/sindresorhus/ora).

## Shareability & Portability 
Aliases are just a little text in a config file and therefore quite easy to share and to drag around to your other machines or friend's machines. 

It does not beat `npm install` though. If you want to port your config files to other computers or share it with other people you have to back them up somewhere and also provide some installation script in order to add them easily to a Git setup (if you're friendly).  

By keeping this functionality in an npm package I get backup, easy-install and shareability out-of-the-box. On top of that, many developers are very familiar with using npm to install tooling.

## More UX
Going forward I would like to further improve belly's CLI-UX by, for instance, improving error display and improving the spinner states and who knows what I come up with. 

By writing this tool with JavaScript, it is extremely easy for me to extend the tool and to keep iterating. Aliases with bash scripts would just break my brain and it would take me forever.

## Try belly
If you want to know what I am talking about, [get belly](https://github.com/sindresorhus/ora) by doing `npm i -g belly`. 
If you have any ideas for extending it or improving it, hit me up in the [belly issues](https://github.com/kahlil/belly/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc).





