---
title: "Asynchronous Validation With Angular Reactive Forms"
---

<div class="date">January 25, 2017</div>

The Reactive Forms Module in Angular allows you to add synchronous and asynchronous validators to form elements. Synchronous validators of a form element always run when a keyup event happens on that element.

_Note: in order to keep the information as current as possible I am posting updates at the bottom of this article. For now it still makes sense to read the whole article though._

When all the synchronous validators are valid the asynchronous validators run on every keyup. And there is no easy way to debounce them at this point in time.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">AFAIK there&#39;s no &quot;easy&quot; way. You&#39;d need to subscribe to changes, debounce, apply validator, set validity manually</p>&mdash; The Mighty Parrot 🐦 (@PascalPrecht) <a href="https://twitter.com/PascalPrecht/status/819542138975383553?ref_src=twsrc%5Etfw">January 12, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

I find this surprising since asynchronous validation mostly (always?) is server-side validation and you most likely don’t want to have multiple users sending a request per keyup event to the server.
In order to lighten the server load you would want to filter and debounce the values that are put into a form field by the user. This can be easily done via RxJS operators if you get access to the stream of value changes.
So how do we do that? Well, just like Pascal said in his tweet above.

Angular Reactive Forms come with powerful API, it is not as convenient as just adding an asynchronous validator but there is a decent way to take full control over asynchronous validation by subscribing to the Observable property `.valueChanges()`.
So lets say you have an input field like this:

```
const inputField = new FormControl('', [...mySyncValidators]);
```

`inputField` exposes the aforementioned Observable property `.valueChanges()` which is a stream of value changes of that input field. We can subscribe to it like so:

```
inputField.valueChanges.subscribe(x => console.log(x));
```

This is great because with the Observable operators that come with RxJS we have really good control over under which conditions and how often we want to send validation requests to the server.

```
inputField.valueChanges
    .filter(val => val.length >= 2)
    .debounceTime(500)
    .switchMap(val => this.http.get(`http://myapi.com/${val}`))
    .subscribe(valid => console.log(valid));
```

Let’s go through what the code above does:

- the `.filter()` operator makes sure that values are only passed through when they have 2 characters or more
- the `.debounceTime()` operator makes sure that only the latest value is passed through after 500ms have passed without a value change
- `.switchMap()` sends requests to the server whenever a value passes through `.filter()` and `.debounce()` but always only subscribes to the result of the latest request made all other requests are aborted

In the `.subscribe()` function at the end of the function chain you can then go ahead and set the validity of the inputField manually. The field is represented by the FormControl class which has an API to manually put the form field into different states. `FormControl` inherits AbstractControl which comes with methods like `.markAsTouched()`, `.markAsPending()` etc. as well as `setErrors()`.

`.setErrors()` is cool because it allows you to set specific errors on the field dynamically. Here is how it works: if you want to set an error you just call the method with an object that gives the error a name:

```
inputField.setErrors({ someError: true });
```

This puts the field and the whole form into the invalid state, when you want to make it valid again all you do is:

```
inputField.setErrors(null);
```

Hopefully the Angular team comes up with an easier way to debounce async validators in the future, but for now, this works well.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">AFAIK there&#39;s something declarative in the making. I&#39;ll double check with the team and let you know</p>&mdash; The Mighty Parrot 🐦 (@PascalPrecht) <a href="https://twitter.com/PascalPrecht/status/819550931289337856?ref_src=twsrc%5Etfw">January 12, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>


Sounds good.

## Updates

This article has been getting traffic on a regular basis so I am posting updates here at the bottom to keep the info as current as possible.

### 22nd of August 2017

Since Pascal said he would check with the Angular team if anything was planned I checked back with him and he was prompt in his response:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Yes - this should lay the foundations: <a href="https://t.co/qOpiXRDTLP">https://t.co/qOpiXRDTLP</a></p>&mdash; The Mighty Parrot 🐦 (@PascalPrecht) <a href="https://twitter.com/PascalPrecht/status/899967448723709953?ref_src=twsrc%5Etfw">August 22, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Progress is being made.

[Changes have landed](https://github.com/angular/angular/commit/1cfa79ca4e21788e0323baf544704ee7ef7d63ea) in v5.0.0-beta.4 that lay the foundation for declaratively debouncing async validators in reactive forms. For now it seems like the commit adds the possibility for template driven forms to delay form control updates to the blur or submit events. The commit description also explicitly states this:

> * Better support of reactive validation strategies

This seems to indicate that this commit introduces or at least sets the groundwork for more flexible asynchronous validation in Angular 👍.