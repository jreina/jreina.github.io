---
layout: post
title:  "Why compose?"
date:   2018-03-17 04:00:00 -0500
categories: programming functional
description: "Why would I use compose?"
published: false
---

This will make more sense if you know what currying is. If not, don't despair, [here is an article I wrote about currying](http://johnnyreina.com/programming/functional/2017/09/21/whats-up-with-currying.html)!

## Compose
`Compose` is a function that takes some functions and gives you a new function which accepts a value and works from right to left, passing in the value to the rightmost function and the return value into the next function in the list. Here is `compose` written and used in both an imperative and functional style:
<script src="https://gist.github.com/jreina/81e7792cff802081c947da68602bf611.js"></script>
<script src="https://gist.github.com/jreina/5ec0e513a9f6682a92e68215cee389f5.js"></script>

Awesome! We doubled a number and added 1 to it. How incredibly useful this will be!
Let me stop you right there. 

## Identities
Perhaps you learned about Pythagorean theorem in school, `a² + b² = c²`. It may seem kind of boring but this theorem is incredibly profound and the entire body of trigonometry is based on it. When you have two representations of the same thing with all information about that thing in both representations, you have an *identity*. Identities are great because they can simplify problems (or in some cases make them worse) for us.

## What the hell does this have to do with `compose`?
`Compose` is special because it gives us an identity for function composition. If you've ever written a big function composition in a language that uses parenthesis for function invocation, you know damn well that it can be an abomination when you are done. "Am I writing Lisp or JavaScript?", you ask yourself in bewilderment as you stare at the mountain of parentheses. `Compose` provides us with an identity between `f(g(h(w(x))))` and `compose([f, g, h, w])(x)`. This is neat for two reasons: 1. it retains the same function ordering and 2. we can build complex functions out of little simple ones without writing a humongous function and using up all the parentheses in our savings account.

## Don't we still have to write the functions to compose?
The answer is maybe. After using [underscore](http://underscorejs.org/) and [lodash](https://lodash.com) for a number of years, I have taken a strong preference for [Ramda](http://ramdajs.com/). The reason for this is because all of the functions in Ramda are curried and they all accept the data as the last parameter. This is important because it allows us to apply some stuff to a utility function and have a function waiting for our data. Let's take a look at an example from a [project I recently worked on](https://github.com/jreina/mocha-testrail-advanced-reporter/blob/master/lib/testrail-publisher.js#L9):
<script src="https://gist.github.com/jreina/b4e6fa9c983e829d9ac28853d26870f6.js"></script>

Now let us examine the same function, without using compose:
<script src="https://gist.github.com/jreina/cbc09fb2050519f1bded231ca1e32481.js"></script>

As you can see, a lot of work is being done here and I really only had to write one function! Not only that, but the `compose` version is MUCH easier on the eyes.

## The bigger picture
The fact that `compose` gives us an identity for composition is cool because it gives us a firm mathematical basis for representing our compositions differently. It tells us we have a choice in how we represent our actions. For me, this is the biggest lesson to be learned from functional programming as a whole: 
> "it doesn't have to be this way and I can prove it mathematically!"

## One last thing
You may have heard of the `pipe` function or even the [pipeline operator](https://github.com/tc39/proposal-pipeline-operator). `Pipe` and `compose` are related in the sense that they both do the same thing, except that `pipe` does left-to-right composition while `compose` does right-to-left composition. This may be more intuitive to some folks since the invocation order of the supplied functions is identical to the order in which they are supplied. That is, `pipe([f, g, h, w])(x)` is an identity for `w(h(g(f(x))))`. I have found several cases where people preferred `pipe` over `compose` due to this difference. I personally prefer `compose`, but it's easy to understand that people would prefer left-to-right composition.