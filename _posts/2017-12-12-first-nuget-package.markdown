---
layout: post
title:  "My first (published) Nuget package."
date:   2017-12-12 04:00:00 -0500
categories: dotnet nuget
description: "We all built a thing and it's pretty cool."
published: true
---

> We all built a thing and it's pretty cool

A while ago I was showing a friend how the map, filter, and left fold functions might work under the hood. Together we worked out all three functions using a language we were both familiar with: C#.

I made the foolish mistake of saying "a lot of the methods we find in LINQ Enumerable extensions are based on the left fold function." Now I had to prove it. So I got to work, first by giving the fundamental (map, filter, and left fold) functions the same alias that they have in `System.Linq`, then by gradually building out some of the other functions like `max` and `count`.

Realizing that this source could be pretty valuable to people who are learning these higher-order functions, I decided to put this code up on Github. Furthermore, if someone is having a hard time understanding these functions I could just point them to the implementation!

There was a problem, though. This project needed a name. When I first started off I [created the project and solution under the name ThingsThatAreNotAggregate_WithAggregate](https://github.com/jreina/ShittyLINQ/commit/6c91813e432e5ca9ff5c88f08007cf019d296c82), which is unwieldy at best.

After giving it some thought, and seeing a whole bunch of easter eggs in NPM packages while searching for passwords and curse words in source trees, the project had a name: ShittyLINQ. How perfectly fitting! Rather than hide the easter egg deep in the source, the project itself would be an easter egg. You don't even have to read the tagline of the repository to know what this project does, the name says it all.

The project had a name, but now it was woefully incomplete compared to the _good version_ and completely untested, so there could be inaccuracies in the implementations and nobody would know. With [Hacktoberfest](https://hacktoberfest.digitalocean.com/) on the horizon, I saw ShittyLINQ as a great way to get first-time contributors involved in a way that would be somewhat comfortable. I mean, _this is the shitty version of LINQ, nobody here is demanding perfection_. I decided to open up a few issues and mark them with the _Hacktoberfest_, _good first issue_, and _help wanted_ labels. The response was fantastic. ShittyLINQ was able to pick up a handful of new extension methods, a suite of really solid tests, and best of all several first-time contributors made their first pull request!

Somewhat facetiously, I thought it would be fun to publish this thing as a NuGet package. Even if only for novelty's sake, I wanted to get it out there for anyone who decided they weren't interested in the good version of LINQ. The contributors wouldn't have their work stashed away in a code vault. The code would be built and available to use by anybody! I didn't want to manually build and publish, so I tried out various CI platforms and ultimately ended up using AppVeyor to get the job done.

At the time of this writing, ShittyLINQ is in prerelease version 0.1.22 on NuGet.

Relevant links:

* [Hacktoberfest](https://hacktoberfest.digitalocean.com/)
* [AppVeyor](https://ci.appveyor.com)
* [ShittyLINQ Source](https://github.com/jreina/shittylinq)
* [ShittyLINQ NuGet](https://www.nuget.org/packages/ShittyLINQ)
* [ShittyLINQ AppVeyor](https://ci.appveyor.com/project/jreina/shittylinq)
