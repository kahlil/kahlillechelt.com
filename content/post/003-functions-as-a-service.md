---
title: "I Finally Understood Functions As A Service"
date: 2017-10-24
---

Since I heard it for the first time, I was struggling to understand what "Functions As A Service" like AWS Lambda really is. I heard people explaining it on podcasts and read what it said on the AWS Lambda landing page but it just didn't click.

Last week me and [Henning](http://twitter.com/hglattergotz) recorded [the lastest episode of our podcast REACTIVE](http://reactive.audio/87). On that episode Henning talks about how he uses AWS Lambda and an AWS database to build an API for their app at work. This made me finally understand what this is all about. 

They built the API by writing some code that parses request parameters, retrieves some data from the database and then sends that data back as JSON in the JSON API format. That code is the function that is being provided "as a service".

That is it. 

The HTTP layer, security and scalability is all provided by AWS services. *Functions As A Service* also means that you only pay for computing time when the function is used. When there is no requests to the API then you don't pay. 

This is an incredibly fast and efficient way to build an API that is production ready in no time. 

On the podcast we also talked about how more and more of these "solved problems" like security and scalability will be packed up into some service and how the usage of them will certainly be very widespread in the not so distant future. 

[@codepo8](http://twitter.com/codepo8) said it best on Twitter yesterday: 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Prediction: in five years most of what we call &quot;coding&quot; now will be done by machines. And they&#39;ll be much better at it.</p>&mdash; Chris Heilmann (@codepo8) <a href="https://twitter.com/codepo8/status/922380136531537921?ref_src=twsrc%5Etfw">October 23, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

