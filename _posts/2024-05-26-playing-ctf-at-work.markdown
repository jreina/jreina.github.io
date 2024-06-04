---
layout: post
title: "Playing a CTF at Work"
date: 2024-05-26 00:00:00 -0500
categories: ctf
description: "We got to play a CTF with coworkers!"
published: true
---

## Preface

During our first ever EPDS (engineering, product, design, and security) offsite at SafeBase, a CTF was organized to promote team building and to encourage generally random groups of people to work together towards a common goal. Every CTF team consisted of at least one member of each EPDS group and usually in configurations that we are not accustomed to in our day to day work.

## Entry point

The CTF was set up on [HackTheBox's Business CTF platform](https://ctf.hackthebox.com/), which is a new one to me. Overall the platform is quite nice and similar to the main HTB experience. The CTF was set up jeopardy style, with most challenges in the easy ranking and a few in the medium ranking. Additionally, 9 of the 11 challenges were in the web category with the remaining 2 being in the OSINT category.

Setup was nice and easy. Most people were newcomers to the HTB platform so they were required to create a new account, but CTF access is federated through the main HTB SSO login so veterans can just use their main login here.

## Being a team captain

I was chosen as a team captain due to some previous CTF experience. If I learned anything from this experience, it's that being a team captain is more than just approving access to the team and assigning challenges. For completely new CTF players, the experience can be overwhelming and frustrating since you have no idea what you are even looking for. You may have never attempted SQL injection in your entire life!  

Team captains should help guide where necessary, find floating pairings of players in real time, and generally keep the team efforts organized. For example, if you are given a team of 6 but 3 have never played a CTF before, you should prefer to have 2 or 3 groups on your team each working a problem as opposed to 6 people assigned to 6 problems but only making progress on 1 or 2 and several players becoming frustrated with the task at hand.

## Result

We were allocated about 4 hours to work on it during the main itinerary, but many player's competitive and hacking spirit was in overdrive after to the main event. I believe we ended up in a 4-way tie at the end of the session, with some players discussing the remaining challenges over dinner and into the next day.  

As any CTF player knows, when the clock is ticking it is difficult to think about anything else. So after the day's (and night's) activities I chose to settle into my hotel room with a couple drinks and some music and continue working on the open challenges. Working by myself I managed to solve 2 of the challenges, with one of them being a really fun exploit chain (unsanitized input -> reflected XSS -> CSP -> canary). At the end of the second day, I paired up with [another player from a different team](https://patrickt.one/about/) to work through the 2 remaining problems. This session proved to be quite fruitful as they mentioned that we have access to a [PwnBox on HTB](https://help.hackthebox.com/en/articles/5185608-introduction-to-pwnbox)! Once we had access to the PwnBox, we solved the most nagging challenge in about 20-30 minutes. The final challenge was a straightforward OSINT challenge with a single pivot.

## Conclusion

This was a great activity for the team. It was nice to see a few dark horses coming through with the assistance of LLMs or natural curiousity (looking at you product team). The importance of the team captain cannot be overstated. It can make the difference between a massively enriching experience and a total frustration for some team members. This was admittedly a huge blind spot for me that I will be certain to pay careful attention to in the future.  

Inspired by a [talk by Adam Schaal](https://www.youtube.com/watch?v=z3VXjz4buJE), I have previously outlined the idea of Red Team Days, team wargames, or team CTFs. I hope to refine this idea further and implement at work at some point in the future. Overall, a team CTF can be an incredibly rewarding experience for your team. Not only as a team builder, but as a vehicle to help foster a security culture.

