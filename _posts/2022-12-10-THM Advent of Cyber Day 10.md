---
title: Advent Of Cyber 2022 Day 10
date: 2022-12-10 09.33.00 +/-TTTT
categories: [Try Hack Me, Advent OF Cyber 2022]
tags: [tryhackme,try hack me, hacking, advent of cyber, advent of cyber 2022, advent of cyber day 10]     # TAG names should always be lowercase
author: me
---

![day10](/assets/AOCD10/day10.png)

# Your a mean one Mr Yeti

## Overall thoughts

I really enjoyed this short look into how to manipulate memory in a game.  This was a nice look at something that can be a lot bigger.

## Getting started

We need to use the attackbox today as everything is on there that we need.

### Learn controls and explore

The controls were easy to figure out arrow keys to move and space bar to interact.

### The Guard
 
The guard is controling to entrace and wants us to guess a number.  With such a wide range we will never guess it so our first guess was wrong.  But it gave us some information we can use. We can open cetus and search for the value he gave us

![search](/assets/AOCD10/search.png)

Lets bookmark that so that we can use it

It gives us a base 16 number which we can decode using online tools.  We have a few options.  We can lock that value,  We can provide our own value, or we can just decode the next value he gives us.

Talking to the guard again I see the value changed so before I guess the number I go ahead and decode it using cyber chef

![cyber](/assets/AOCD10/cyberchef.png)

I give that decode value and the guard says he will let me in

#### Question 1

![q1](/assets/AOCD10/q1.png)


Talking to the  guard again we get the answer to the first question

![guard](/assets/AOCD10/guardflag.png)

### Enter the jail

We walk into the jail and we are killed by the snowball launching machines.  If only we could have more HP.   We can do this by doing a differental search.  A differential search is a series of searches that looks for values that have change in between each time we searched.  

So lets search using Cetus with no value. We get over 450 thousand results. Next lets walk in and out of a snowball cannon to lose some health and search again.  We can do that multiple times but I think I have the value I need.  I bookmark it in Cetus then on the bookmarks tab I lock the value.  To check this works I stand in a snowball launcher and my health doesn't go down.  Eureka!!

#### Question 2

![q2](/assets/AOCD10/q2.png)

Walking to the end of the jail and speaking with the bandit yeti we get the answer to questiion 2

![yetiflag](/assets/AOCD10/yetflag.png)

## Conclusion 

This was a very quick, enjoyable room that was looking at in browser memory manipulation.  A great topic and happy to have completed it.
