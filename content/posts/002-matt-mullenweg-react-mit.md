---
title: "How Matt Mullenweg Single-Handedly Made Facebook Relicense React to MIT"
date: 2017-09-26
---

OK, I have no proof that this is actually true, but it is a fun thought experiment / conspiracy theory. Here me out.

[Facebook just announced that they are relicensing a few of their open source projects to the MIT license](https://code.facebook.com/posts/300798627056246/relicensing-react-jest-flow-and-immutable-js/).

I am pretty sure this change will be extremely well received by everybody using React.

It will also ensure that the majority of React users will switch to React 16 (the first version under the MIT license) because their BSD + patents license is widely mistrusted and / or disliked.

I for one like to think that this change was triggered by the shots that Matt Mullenweg fired in [his post "On WordPress and React"](https://ma.tt/2017/09/on-react-and-wordpress/) a few days ago. I re-read his post a couple of times because I found some of the statements he made very interesting. At first glance the post reads like "OK WordPress just ditched React no big dizzle" but after re-reading it I realized that Matt just deprived React of a quantum leap in growth. Wow. Let's go through the interesting points:

First :boom::

> Big companies like to bury unpleasant news on Fridays

This statement is in context of Facebook's post about sticking with the BSD + patents license after the Apache Foundation put their license on the black list.

Right in the beginning of his article he accuses Facebook of shady behavior.

Second 💥:

> I'm not judging Facebook or saying they're wrong, it's not my place.

This is hilarious. Translation: "I am judging Facebook and I am saying they are wrong."

Third 💥:

> We had a many-thousand word announcement talking about how great React is and how we're officially adopting it for WordPress, and encouraging plugins to do the same. I’ve been sitting on that post, hoping that the patent issue would be resolved in a way we were comfortable passing down to our users.

Now for the squeeze.

Translation: "We were going to officially adopt React as the WordPress JavaScript thing and make a big fuss about it which would have been massive promo for you for free and would most likely have pushed React adoption into jQuery-like spheres. But now we're not doing that, lol."

Fourth 💥:

Squeeze even harder:

>  Core WordPress updates go out to over a quarter of all websites, having them all inherit the patents clause isn’t something I’m comfortable with.

Translation: "For realz Facebook?!?!? You don't want your Framework to be used by over 25% of _all websites on the internet_ with a snap of a finger!?!? Maybe y'allz want to think about that a little bit?"

Fifth 💥:

Now for the kill:

> But we have a lot of problems to tackle, and convincing the world that Facebook’s patent clause is fine isn’t ours to take on. It’s their fight.

Translation: "We don't need all your drama. You're on your own."

> We’ll look for something with most of the benefits of React, but without the baggage of a patents clause that’s confusing and threatening to many people.

Translation: "React is not indispensable and can easily be switched out with something similar, thank you."

So good. He whacked them over the head in the nicest way possible.

It makes total sense to me that Matt's post would make them rethink their licensing strategy. The Apache Foundation reject did not really mean a big impediment to their growth but loosing WordPress would deprive them of more massive adoption and may even mean a decline in React adoption going forward because Matt and WordPress as a project are just incredibly influential in the web development community.

Potentially being the JavaScript thing for WordPress and WordPress plugins and the growth React would gain by that must outweigh the litigation costs they would save by sticking with BSD + patents. 

Matt has already reacted to Facebook's anouncement:

> I am surprised and excited to see the news that Facebook is going to drop the patent clause that I wrote about last week. They’ve announced that with React 16 the license will just be regular MIT with no patent addition. I applaud Facebook for making this move, and I hope that patent clause use is re-examined across all their open source projects.

Matt is pleased about the change. 

But Facebook has lost the chance to be the designated WordPress JavaScript framework: 

> Particularly with Gutenberg there may be an approach that allows developers to write Gutenberg blocks (Gutenblocks) in the library of their choice including Preact, Polymer, or Vue, and now React could be an officially-supported option as well.

Looks like the WordPress team found out about [this new-fangled compiler](https://twitter.com/_developit/status/898952382960119808/photo/1) that Jason Miller of Preact-fame is working on which compiles, Web Components, VueJS components and Preact components into highly optimized Preact components. That's awesome.

Interestingly Matt is not mentioning if they will still switch away from React for [Calypso](https://developer.wordpress.com/calypso/). Somebody opened [an issue asking about](https://github.com/Automattic/wp-calypso/issues/18198) it but nobody has responded yet.

Meanwhile React 16 has been released and [the license is indeed MIT](https://github.com/facebook/react/blob/master/LICENSE).



