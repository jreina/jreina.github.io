---
layout: post
title:  "What [I think] I know about van Laarhoven lenses"
date:   2018-08-14 16:20:00 -0500
categories: programming functional
description: "Composable magic"
published: true
---

## Mo' functions, mo' problems
We are always told to avoid mutation in functional programming. This is primarily achieved by using constant variables and in the case of reference types (objects, arrays, etc.), using methods and functions which avoid mutation. While there are a plethora of functions that are well-suited to this idea with arrays, such as map, filter, and reduce, such functions are much more cumbersome to use with objects and are not widely used. We have object spread and static methods like Object.assign, which can help tremendously but lead to messy syntax for all but the most simple of object structures. Because of this, most examples in JavaScript you see probably look something like this:  
<script src="https://gist.github.com/jreina/2870a8e7cfb45a5a34044ad683163950.js"></script>  

While this is generally fine for very shallow objects, the story gets much more complicated when trying to enforce immutability in complex objects while changing deeply-nested values...  
<script src="https://gist.github.com/jreina/e290610d587eacd0d00e6b96d4ef555a.js"></script>  

This is obviously not very idiomatic. The problem is made worse when a library like React enforces the idea of immutability (this isn't React's fault, though). So how do we deal with this in a way that feels a bit more natural? For this, I have turned to using lenses. Lenses are a special type of object that combines a setter and getter such that you can perform standard operations, most commonly setting, getting, and mapping, on values of an object in a way that the original object is not modified. Not only do lenses allow you to operate on objects while enforcing immutability, they also compose together such that each lens digs deeper into your complex objects and exposes a set of immutable operations for the entire object.

## So how do we make a lens?
Generally speaking, there should exist a lens package in your language of choice. For JavaScript, I use the lenses built into Ramda since Ramda also comes with functions that I tend to use including getters and immutable setters. Ramda also includes a function called `lensProp` that allows you to specify an object key and that will be the focus of the lens.

## What does this look like?  
<script src="https://gist.github.com/jreina/6ff331f335ccdaa37334e95af25afad6.js"></script>  
  
## This looks clunky enough. I bet lens composition is hideous!  
Let us see an example of lens composition:
<script src="https://gist.github.com/jreina/6843b1a62249a997de69b9230f4273eb.js"></script>  

## Compose is right to left, how are these working backward?
I honestly do not know. However, this makes them easier to read when under composition, especially when you consider that the compose operator in Haskell is `.`. So the same composition in Haskell would look like `employeeInfoLens . phoneLens . homeLens . numberLens`, and that sort of looks like normal dot notation for property access in C-based languages. This is sort of a cop out, but I'm sticking to my guns here.

## That is insane. How does this work?  
Magic.  
Honestly, I am not advanced enough to fully understand the nature of lens composition, but I do know it works and works well for my needs. For this reason, I almost scrapped the idea of writing this post altogether!

## Where should lenses be used?
Lenses should absolutely be used when enforcing immutability is our top priority, but also when we need to update an object and we don't quite know or even care about the structure of the object.

## Do we always have to compose lenses? Seems cumbersome to create a lens for every property down the chain.
The first thing to know is that `R.lensProp('x')` is shorthand for `R.lens(R.prop('x'), R.assoc('x'))`. If you are using Ramda, you are in luck because Ramda provides other ways to create lenses. `R.lensPath` allows you to specify a path into the nested value that you want to focus on, and `R.lensIndex` allows you to work with elements in an array.

## It seems like `R.view`, `R.over`, and `R.set` are doing all the work. What are those?
These are standard operators for lenses and will generally be included with all lens packages. On their own, lenses are not very useful (just like any other structure). So what do these functions do?

### `view`
This function accepts a lens, then an object, and returns the value of the focused property of the lens. This essentially just calls the getter of the lens and is fairly straightforward.

### `set`
This function accepts a lens, a value, and then an object, and returns a copy of the object with the focused property set to the provided value. Again `set` essentially just calls the setter of the lens and is fairly straightforward.

### `over`
This function accepts a lens, a transform function, and then an object, and returns a copy of the object with the focused property set to the original value of the focused property \*after\* passing it through the provided transform function. This operator is a little harder to understand. This function is just like the `map` function since it runs a function \*over\* the focused value.

## Additional reading 
 - [Haskell Lens package wiki](https://github.com/ekmett/lens/wiki)
 - [History of Lenses (from same wiki as above)](https://github.com/ekmett/lens/wiki/History-of-Lenses)
 - [Ramda Docs - lens](https://ramdajs.com/docs/#lens)
