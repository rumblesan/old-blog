---
date: '2011-11-13 14:39:59'
layout: post
slug: patch-a-day-november-2011-day-10-euclidean-rhythms-part-3
status: publish
title: 'Patch-a-Day November 2011 Day 10: Euclidean Rhythms (part 3)'
wordpress_id: '362'
categories:
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- euclidean rhythms
- recursion
- sequencing
comments: true
---

Right, back on track, mostly recovered from an active weekend and have cracked getting PD Extended running under Lubuntu (might do a post on this at some point)

Here, as promised, is an abstraction that will generate Euclidean Rhythmic sequences when given a number of beats and the measure length.

![Euclidean rhythm abstraction](/a/2011-11-13-patch-a-day-november-2011-day-10-euclidean-rhythms-part-3/Euclidian-rhythm-abstraction.png)"

There have been a few changes since the patch earlier this week and I spent a bit of time wrestling to clear up some awkward bugs that were difficult to track down because of all the recursion here.

The left hand side is where the beats and measure length values get parsed and then the lists of ones and zeros created. There's some logic here to limit the values a bit, so that the number of beats can never exceed the measure length, and neither value can go below zero.

To the right of this is a series of objects that check to see if either of the input lists is zero length. I found that there's a bit of a problem with the list matching and interleaving if one of the input lists is empty and it would require a lot of changes to the logic involved to cope with it. Instead I decided it would be a better idea to just check before hand. If one of the lists is zero then they get joined (so you don't need to check which is empty) and then output straight away. Otherwise they go to the Euclidean Calculation step.

Finally the routing to check if we recur or not is neatened up a bit and I've introduced a tiny delay. This is done so because otherwise PD will complain about buffer overrun errors because the patch is trying to calculate too much in one cycle. By introducing the delay we can spread the calculations over more cycles and we won't push things too much.

There were also a couple of small bugs I fixed in the interleave and lmatch objects but they're otherwise untouched.

Check out the repository for the abstraction and an example.

Next up, using this with a sequencer.
