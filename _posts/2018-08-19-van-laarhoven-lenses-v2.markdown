---
layout: post
title:  "What [I think] I know about van Laarhoven lenses [v2]"
date:   2018-08-19 16:00:00 -0500
categories: programming functional
description: "Composable magic"
published: true
---

## Mo' functions, mo' problems
We are always told to avoid mutation in functional programming. This is primarily achieved by using constant variables and in the case of reference types (objects, arrays, etc.), using methods and functions which avoid mutation. While there are a plethora of functions that are well-suited to this idea with arrays, such as map, filter, and reduce, such functions are much more cumbersome to use with objects and are not widely used. We have object spread and static methods like Object.assign, which can help tremendously but can also lead to messy syntax for all but the simplest of object structures. Because of this, most examples in JavaScript you see probably look something like this:  
<script src="https://gist.github.com/jreina/2870a8e7cfb45a5a34044ad683163950.js"></script>  

While this is generally fine for very shallow objects, the story gets much more complicated when trying to enforce immutability in complex objects while changing deeply-nested values...  
<script src="https://gist.github.com/jreina/e290610d587eacd0d00e6b96d4ef555a.js"></script>  

This is obviously not very idiomatic. The problem is made worse when a library like React enforces the idea of immutability (this isn't React's fault, though). So how do we deal with this in a way that feels a bit more natural? For this, I have turned to lenses. Lenses are a special type of object that combines a setter and getter such that you can perform standard operations, most commonly setting, getting, and mapping, on values of an object in a way that the original object is not modified. Not only do lenses allow you to operate on objects while enforcing immutability, they also compose together such that each lens digs deeper into your complex objects and exposes a set of immutable operations for the entire object.

## So how do we make a lens?
Generally speaking, there should exist a lens package in your language of choice. For JavaScript, I use the lenses built into Ramda since Ramda also comes with functions that I tend to use including getters and immutable setters. The following example shows a lens being created for a name property.  
<script src="https://gist.github.com/jreina/ed73554f4b065b5215df825b922de2f1.js"></script>

While this is neat, lenses are not very useful on their own (just like any other structure). There is not a whole lot we can do with `nameLens` on its own. This is where lens operators come in. The three operators provided by Ramda are `view`, `set`, and `over`, which allow you to get, set, and map the focused property, respectively.

The examples below will use the following object:
<script src="https://gist.github.com/jreina/6913a671ee1e745d23cb54470da7eb5f.js"></script>

### `view`
This function accepts a lens, then an object, and returns the value of the focused property of the lens. This essentially just calls the getter of the lens and is fairly straightforward. Here, we can use `nameLens` to view the value of the focused property:  
<script src="https://gist.github.com/jreina/ad35b110f6ca4b52b659782854546eb6.js"></script>

### `set`
This function accepts a lens, a value, and then an object, and returns a copy of the object with the focused property set to the provided value. Again `set` essentially just calls the setter of the lens and is fairly straightforward. Here, we use the `set` operator along with `nameLens` to set the value of the focused property. Note that the original object remains unchanged.  
<script src="https://gist.github.com/jreina/95e6ac9d14fb1f321e4cfa7bdb499fdf.js"></script>

### `over`
This function accepts a lens, a transform function, and then an object, and returns a copy of the object with the focused property set to the original value of the focused property \*after\* passing it through the provided transform function. This operator is a little harder to understand. This function is just like the `map` function since it runs a function \*over\* the focused value. Here we use the `over` operator to call the `toUpperCase` method of the string. Just like before, the original object remains unchanged.  
<script src="https://gist.github.com/jreina/9b6032129f1d34dbe9d2219079e98f24.js"></script>

## What if we need to change a value in the `parking` object?
Suppose we need to update the value in `person.parking.row` while maintaining immutability. This is where the compositional nature of lenses come in handy since lenses compose using the standard compose operator! This is how we could create a lens for this scenario:
<script src="https://gist.github.com/jreina/b0334c07c587d2e8e263963757c2e36d.js"></script>  
Now, our `parkingRowLens` can be used with the lens operators to do the same setting, getting, and mapping operations. Best of all, the original object will still remain unchanged due to the nature of lenses.

## Is there an easier way to create lenses?
If you are using Ramda, then definitely yes. Otherwise, be sure to check the owner's manual for your lens package. Ramda provides a few convenience functions to help us create lenses:  

| Function | Description | Example |
| -- | -- | -- |
| R.lensProp | Creates a lens which focuses on the provided property. | `R.lensProp('name')` |
| R.lensPath | Creates a composition of lenses to focus on the provided path. | `R.lensPath(['parking', 'row'])` |
| R.lensIndex | Create a lens to focus on the provided array index. | `R.lensIndex(0)` |  
  
  
## Additional reading
 - [Haskell Lens package wiki](https://github.com/ekmett/lens/wiki)
 - [History of Lenses (from same wiki as above)](https://github.com/ekmett/lens/wiki/History-of-Lenses)
 - [Ramda Docs - lens](https://ramdajs.com/docs/#lens)
