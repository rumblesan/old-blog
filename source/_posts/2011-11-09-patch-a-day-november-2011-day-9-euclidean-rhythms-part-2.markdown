---
date: '2011-11-09 23:34:16'
layout: post
slug: patch-a-day-november-2011-day-9-euclidean-rhythms-part-2
status: publish
title: 'Patch-a-Day November 2011 Day 9: Euclidean Rhythms (part 2)'
wordpress_id: '357'
categories:
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- euclidean rhythms
- sequencer
comments: true
---

Putting everything together now. This patch will actually output a rhythm sequence from two given input lists. It's using the improved list matching abstraction from last night along with the list interleaving patch and then some extra objects to do routing and element length measurement of the remainder to see if we need to recur any more.

![Euclidian rhythm generation](/a/2011-11-09-patch-a-day-november-2011-day-9-euclidean-rhythms-part-2/Euclidian-rhythm-generation.png)"

When the remainder is output from the lmatch, we check how many elements there are in it. If the number is one or less then we don't need to do any recursion and we can just join the two lists and output our sequence, otherwise the lists need to be sent round again. The routing is done by pre-pending "recur" or "output" to the front of the lists then routing them accordingly. This feels a bit clunky but I think it's better than using pairs of spigots. If we don't need to recur then the remainder is joined to the output of the interleaving and that's the sequence. Otherwise the output becomes the main list and the remainder the sublist.

The interleave abstraction has been updated a bit so that it will keep track of and increment the element size of the list accordingly. I find it quite amusing that actually the whole thing now just boils down to these two objects and a bit of recursion. Initially when I was wrestling with this it felt really difficult to do. Now I'm pretty sure these objects could be simplified a lot and something quite efficient can be made. This algorithm is still trickier to implement in PD than I'd like but it'll do.

Tomorrow night I'll polish this patch up a bit and turn it into an abstraction that can be used easily in a patch and by the weekend I'll hopefully have a working sequencer running.
