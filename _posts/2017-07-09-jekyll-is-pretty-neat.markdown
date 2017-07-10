---
layout: post
title:  "Jekyll is pretty neat."
date:   2017-07-09 08:13:33 -0500
categories: jekyll github ruby
description: "I tried out Jekyll."
published: true
---
I only discovered that Github hosts personal websites a few days ago. I knew that you could set up a `gh_pages` branch and have it hosted at `user.github.io/project`, but the idea of hosting my own personal site on Github using a repo is pretty neat.

I took the bait.

I found [a Github help tutorial](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) explaining how to set up Jekyll, a static site generator, to run locally. After following the steps in the article, I emerged with what appears to be a functioning Jekyll site. 

The Jekyll site looks and feels like a CMS. Posts are kept in a folder named `_posts`, and the main structure of the site appears to be contained within various files in another folder at the root of the project called `_site`.

What's really nice is that these pages are very small when served up. This page, for instance, loads in less than half of a second. Compared to a larger CMS, which may have many more features than I will every need, Jekyll appears to offer a nice balance of customization options, simplicity, and performance.

Additionally, Jekyll uses Markdown syntax so if you have written a README before, you should feel at home writing posts.

The one drawback, for me, is the fact that Jekyll is built on Ruby. Since I do pretty much zero Ruby programming, I had to install Ruby just to get started. This is really an inescapable nitpick since something like a Node.js solution would, of course, require Node to be installed, an ASP.NET site would require the .NET Framework, etc.

Overall, I like the idea of using Jekyll as a static site generator. The fact that Github detects a Jekyll site and automatically builds and deploys the site makes it a really attractive option for someone who just wants to get off the ground publishing a few articles (me).
