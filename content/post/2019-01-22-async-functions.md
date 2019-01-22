---
date: 2019-01-22T11:43:02.215Z
title: "How to Use Async Functions"
---

[This article](http://2ality.com/2016/10/async-function-tips.html) by Dr. Axel
Rauschmayer was exactly what I needed to wrap my head around how to use async
functions without confusion.

Because I was just using them intuitively so far and because of their
synchronous style I got confused about when to `try-catch`. I also attempted to
call an async function without `await` in front of it while using `await` in
it's body, fully expecting it will be executed synchronously.

It's important to remember that the foundation of async functions is Promises.

The most interesting parts of Axel's article to me, were these:

- [Async functions are started synchronously, settled asynchronously](http://2ality.com/2016/10/async-function-tips.html#async-functions-are-started-synchronously-settled-asynchronously)
- [Parallelism](http://2ality.com/2016/10/async-function-tips.html#parallelism)
- [Immediately Invoked Async Function Expressions](http://2ality.com/2016/10/async-function-tips.html#immediately-invoked-async-function-expressions)
