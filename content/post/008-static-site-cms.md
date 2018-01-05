---
title: "Working Title: Static Site CMS"
date: 2018-01-05
---

Product development has always been of huge interest to me. I love creating something with web technologies that solves a problem and iterating on it. That is basically what I do at work but I always wanted to have my own thing. 

During the last year I have played around with a couple of ideas  while trying out different JavaScript frameworks. Altogether I think I must have at least started working on 4 or 5 things. Among those I made two small barely usable products: [TinyDraft](https://www.tinydraft.net) and [Kaf](https://kaf.kahlillechelt.com). They are very simple and incomplete but they do implement a very minimal use case quite OK. 

I always end up hitting a wall when it comes to adding a backend with database, authentication and authorization. Typically I would use services for that. But since I really just get to work on my personal stuff on the road during my commute I can't easily add any services. My connectivity is very limited during those train rides. 

I also tried out using Hoodie which is great to work with locally but deploying a Hoodie backend wasn't trivial to me and ultimately I only really want to think about the frontend side and have the backend just work and be there in local development as well as in production.

So these products are going nowhere. 

I realized in order to build and iterate on anything during my very limited free time I have to remove as much friction as possible. The solution to that problem came to me just a couple weeks ago. 

Recently I hooked up [NetlifyCMS](https://www.netlifycms.org/) to my site. It uses Netlify's auth service and GitHub to add posts to your site. If you set up automatic deployment via GitHub on Netlify that is a really great solution to adding posts to a static site through a nice UI.

But here I had the same problem. I write my stuff on the road and I can't rely on being online. But I really liked some of the functionality that NetlifyCMS provided, namely the schaffolding of posts, easy Front Matter editing as well as the automatic Git commit functionality. 

I thought to myself: "That's cool, I wish I had that for the desktop."

That's the moment when it clicked! I could make this myself with Electron! I actually love working on Electron apps and I would be solving a problem for myself as well as removing my above-mentioned friction from app building. This type of Electron app can be developed without being online at all. Hooray!

I have started working on this over the holidays and I am developing it in the open, the code is [on GitHub](https://github.com/kahlil/static-site-cms) and I will be posting about my progress here. 

For now the product really does not have a name. The working title is Static Site CMS. 

{{< figure src="/img/static-site-cms.png" caption="The empty state" >}}

In my next post I will be writing about the setup I am using to build it.
