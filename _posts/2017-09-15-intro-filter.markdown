---
layout: post
title:  "Intro to the filter function"
date:   2017-09-15 21:11:45 -0500
categories: programming functional
description: "Declarative filtering with examples!"
published: true
---
This might sound a bit outlandish or ridiculous, but I seldom write loops nowadays. What I have found is that just about every programming language includes a set of methods or applicable functions that can replace just about every loop that I was previously writing. These [higher-order functions](https://github.com/hemanth/functional-programming-jargon#higher-order-functions-hof) are called map, filter, and fold.

## Filter

The `filter` function takes a predicate, a function which accepts an item from your array and returns a boolean result, and returns a new array containing the elements that return true when passed through the predicate.

### Baby steps
We'll start off with some easy examples:
<script src="https://gist.github.com/jreina/12255d86bb0c68ce67dbd225556de3d9.js"></script>

Unlike its counterparts map and fold, filter's name immediately and obviously expresses what it does. Though it's a rather simple function, it is very powerful nonetheless.

### Learning to crawl
Here's an example of filtering an array of objects:
<script src="https://gist.github.com/jreina/d8186240301900666cc67f886a13321e.js"></script>

In the first filter, we are looking for people in the list whose name is Mary. Since there is only one person in the list with this name, we only get one result. Note that since `filter` always returns an array, we just got back an empty array when we looked for someone named Fred in the second filter. In the third example, we look for people whose age is greater than 40. Finally, in the last example, we look for people who have two hobbies.

If this is taking a bit to click, I'll show an example of `filter` done in an imperative style. This is a pattern I used to write quite often before I knew how to use filter.
<script src="https://gist.github.com/jreina/90a745a02a75b5ec809bc0370dc07161.js"></script>

While these loops have the same result as the previous examples, they are much more explicit and there is much more typing involved.

### Up and running!
These examples are pretty easy, right? Well, there really isn't a whole lot to it.  

Out of the map-filter-fold family of functions, `filter` is the function I use the least in JavaScript. However, C#'s counterpart, Where, is definitely my workhorse when working in C#.  

When I am filtering data based on multiple conditions, I like to define the predicates as named variables ahead of time. I've found that this improves the readability of the code tremendously, in addition to providing opportunities to reusing the pre-defined functions. Consider the following example:

<script src="https://gist.github.com/jreina/23513ce4a8d4daa846c7fe1cd540c172.js"></script>

Since `filter` always returns an array, you can chain together your calls to `filter` and drill down to the data you want _incrementally_. You **must be careful** with your logic, though, especially when the filtering logic you are trying to apply requires mixing **AND** and **OR** logic.  

### When should I use `filter`?
This might not need to be said, but you should use `filter` when you want to reduce the items in a collection to only those items which meet specific criteria.

### JavaScript is the worst! What other languages have `filter`?
Pretty much all the good ones. Though the names might be a bit different. In an effort to avoid plagiarism and only write what I really know about, I'll list out a few equivalent methods/functions that I know and have used here.

| Language | Function/Method |
| --- | :---: |
| JavaScript | Array.prototype.filter |
| C# | IEnumerable.Where<T> (as part of System.Linq) |
| Haskell | filter |
| PHP | array_filter |
| MongoDB | db.collection.find |

<br />
### Alright, I'm convinced. When do I start?
Right now! Go!  
The best way to get familiar with `filter` is to just start using it.
