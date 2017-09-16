---
layout: post
title:  "Intro to the fold function (aka reduce or aggregate)"
date:   2017-09-16 04:00:00 -0500
categories: programming functional
description: "This fold function is as important to understand as it is difficult to understand."
published: true
---
This might sound a bit outlandish or ridiculous, but I seldom write loops nowadays. What I have found is that just about every programming language includes a set of methods or applicable functions that can replace just about every loop that I was previously writing. These [higher-order functions](https://github.com/hemanth/functional-programming-jargon#higher-order-functions-hof) are called map, filter, and fold.

In the previous two articles, we got a glimpse of the power of the map and filter functions. In this article, I want to discuss the Ma Dukes of iterative functions: the fold function, and hopefully, convey the importance of this function.  

Keep in mind that fold is generally not called fold in programming languages. This is true for JavaScript, where fold is actually called reduce. In this article, I will refer to the fold function, but the examples will show `Array.prototype.reduce`. The array type in JavaScript is said to be [foldable](https://github.com/hemanth/functional-programming-jargon#foldable) because it implements fold as `Array.prototype.reduce`.

## Fold

Fold accepts an accumulator function which it applies to the each item in the array and passes the result on to the next execution of the accumulator. Fold accepts an optional seed value to use as the starting point for your folding. This is rather difficult for me to express in words, so here's a diagram:   
![fold execution diagram](/public/reduce.png)  
Here, `f` is the accumulator function. Notice that each instance of `f` has two arrows pointing to it. That means the accumulator function you provide must accept two parameters: the value from the last execution, and the current value from the array. As a convention, I tend to use `(memo, value)` as my parameter names.  

## Starting off slow
I'll show some basic examples and try to work our way up to some heavier folding.  
<script src="https://gist.github.com/jreina/0a3e87a51e6aad04e9aa7f01ff7be298.js"></script>
What is happening here? The first example describes the sum of all of the elements of the `nums` array. If you follow the diagram, 0 is our seed value. So we start at 0, add 1, pass that on to the next execution where we add 2, pass that on to the next execution where we add 3, and so on. The second example is functionally equivalent to `f(5) => 5!`. In the third example, we are simply taking each letter and appending it onto `memo`. Notice that since a seed value wasn't specified, we just got back the result of running the accumulator function over the first element and used that as our seed.  

This is pretty cool, eh? It may take some staring at for the concept to fall into place, but once you figure it out you will want to fold everything! 

## We added some numbers. Big whoop. Why are you so excited about fold?
I consider fold to be the end-all-be-all iterative function. The bee's knees, if you will. The reason I say that is because the seed value can be **of any type**. That means we can fold over an array and kick out an object, array, number, string, boolean, or whatever your heart desires! Say we have an array of pairs that we want to transpose onto an object, this is easily done with fold:
<script src="https://gist.github.com/jreina/e7dc2e4bf58a549bd19ea572fc7fffc9.js"></script>
The first fold transposes the pairs onto a new object. The second fold, which acts on the new `person` object, pulls those pairs back out. This proves that we did not lose any information during the process. Additionally, folding does not mutate the original array. This is important because we might want to perform some additional transformations on that array after we fold over it.

The other two iterative functions that I've covered, map and filter, can easily be implemented as a function of fold! Consider the following:
<script src="https://gist.github.com/jreina/ece788b9f8daf8b5a8679a3dd0b34eb4.js"></script>
Implementing map and filter as a function of fold are a little bit verbose, due to the fact that map and filter are purpose-built. But, this example clearly shows the relationship between all three functions and thus why I lump these functions into the same bag.

## Holy shit! This is amazing!
I know, right!? I cannot stress enough how powerful this array transform is.

## Where should fold be used?
Due to the flexible nature of fold, it's rather difficult and limiting to say "definitely use it in *scenario a* or *scenario b*." Basically, when you want to accumulate the items of a collection in some way, fold is a great tool for doing so.  

Just as map and filter avoid mutating the original array, so does fold. This is important because we want to transform the list with fold, but we might also want to map and filter afterward. This idea of avoiding mutating data goes a bit beyond the scope of this article but I think Eric Normand did a great job of explaining [why you might want to treat data as unchangeable](https://dev.to/ericnormand/immutable-paper).
