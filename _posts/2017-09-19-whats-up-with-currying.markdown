---
layout: post
title:  "What's up with currying?"
date:   2017-09-21 04:00:00 -0500
categories: programming functional
description: "Hard to get enough of, but not for everyone."
published: true
---
If you've been exposed to functional programming, you have almost certainly come across the concept of curried functions. Named after the man himself, [Haskell B. Curry](https://en.wikipedia.org/wiki/Haskell_Curry), a curried function is one that requires multiple arguments but cannot accept all of them in a single call. Consider the following example:
<script src="https://gist.github.com/jreina/47d840b1dde2ff558afcd3e86206642f.js"></script>
What is happening here? <code>magnitude</code> is rather straightforward in that we take three values and calculate the root of the sum of their squares. `magnitude_curried`, however, is quite a bit different and the syntax used to declare it is perhaps a bit offputting. Here is the same function as full function expressions:
<script src="https://gist.github.com/jreina/19f92293a88ff37fb6fc8c5e080b5431.js"></script>
If we walk through what occurs with `magnitude_curried`, we'll find that it, too, is straightforward, albeit somewhat strange (at first). When we apply the first argument `x`, as `1`, we get back a function. Same thing when we apply the second argument, `y` as `28`. Finally, when we apply the final argument, `z`, as `76`, the magnitude function is called and its result is returned.

### Where does currying come from?
Currying is a concept pulled out of the mathematical basis of functional programming, the lambda calculus. In mathematics, you cannot just go out and grab some value from the world at large and drop it in the middle of your functions. You must specify these outside values as parameters and pass them into your functions. The lambda calculus, as a formal system of arranging functions and how they are used, places additional restrictions on how your function can interact with outside information. In the lambda calculus, functions can have only a single input. In pure-functional programming languages like Haskell, every function is understood to be a curried function.

### Why would we ever need currying?
You need currying when you need a function to be:
1. Reusable
2. Minimally dependent on context
3. Callable after specifying some arguments

What do I mean by this? Consider how these three points apply to the following example:
<script src="https://gist.github.com/jreina/59bd4f74301f89e9db8e91454d68abb5.js"></script>
Here we see the `values` function being declared as a curried function. It takes an array of strings which represent keys of an object, and an actual object, and returns the values corresponding to the given keys from the provided object. In its most simple form, values could be called like so: `values(['a'])({ a: 'hello' })` and it would return `['hello']`. So how is this useful to us? On line number 8, we apply an array of strings to values and assign the resulting function to a variable called `getNameAndDepartment`. As we see on line number 9, this new variable is a fully-callable function. We pass in the first value in the `courses` array and as expected, we get back the `name` and `department` values from this object. Here comes the cool part. Since `getNameAndDepartment` is a callable function and has some of the body pre-filled, we can map over the entire courses array and use the `getNameAndDepartment` function as seen on line 12.  

Big deal. This still seems like a complicated way to get the values of some objects, right? Consider the fact that the `values` function doesn't know about any particular array or object. It doesn't describe the context, it only describes functionality. This satisfies requirement number 2 for me. Additionally, since it remained a callable function after applying the keys which we eventually map over, it satisfies number 3 as well.

This all seems fine, but what about requirement number 1: reusability? Since the `values` function doesn't describe the context, it is automatically reusable for another set of arguments. That is, we can pass in another set of values for `keys` and `obj` and it will work there, too! We see this on line number 26 where we apply the `carKeys` array and on line number 27 where we pass in a cars object and get back the `make`, `style`, and `id` values as expected. Just as before, we can use `getMakeStyleAndId`, a partially-applied function, to map over an array of car objects and get these values for each object in the `cars` array.

### Currying vs partial application
There seems to be some confusion regarding the difference between currying and another similar concept called partial application. This confusion is further compounded by the fact that sometimes they are the same thing. Currying takes a function which requires `n` arguments and reduces it to a series of functions which accept `1` argument, whereas partial application takes a function which requires `n` arguments and reduces it to a function which accepts `n - 1` arguments. Semantically speaking, currying is a _form of partial application_. In fact, in the case of a function which only needs two arguments, to begin with, these definitions are the same. This is the case for our `values` function above. We are _partially applying_ the required arguments, but since the function only ever accepts one argument at a time, it is also a curried function.

### Is there more insidious terminology hidden in functional programming that I should be aware of?
![fur sure](/public/fur-sure.gif)  
I recommend taking a look at the [functional programming jargon repo](https://github.com/hemanth/functional-programming-jargon) from [hemanth](https://dev.to/hemanth) for a huge list of well-defined FP terms. If you're feeling daring, the [fantasy-land spec](https://github.com/fantasyland/fantasy-land) provides the formal definitions of algebraic JavaScript and is what I consider to be reference material for FP in JavaScript.

### Parting notes
I want to stress that the three requirements I listed are sort of the rule of thumb that I use to determine if a function needs to be curried or if I should just leave it alone. Since currying is a concept that many people are unfamiliar with, using curried functions where it doesn't make any sense to do so is a sure-fire way to increase the probability of bugs down the road and stands to alienate newer devs and people who just don't care for FP. If you're [just currying because it kinda looks cool](https://github.com/jreina/Superlatives/blob/master/index.es6#L10), you are obfuscating the meaning of your code.

What do you think? Are these sound guidelines? Does this help you understand the concept?