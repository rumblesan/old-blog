---
date: '2010-11-17 21:33:55'
layout: post
slug: patch-a-day-month-day-17-a-full-rhythm-generator-hats-and-all
status: publish
title: 'Patch-a-Day Month Day 17: A Full Rhythm Generator, Hats and all'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- drums
- generative
- Music
- patch-a-day
- pure data
- sequencing
comments: true
---

So the hats have now been added on and this patch is nearing a first phase of completion. I took a slightly different approach with the rhythm generation for the hats, a sort of subtractive probability generation sort of thing. Anyway, I wanted to try something slightly different and it's worked pretty well.



![Full Rhythm Generator](/a/2010-11-17-patch-a-day-month-day-17-a-full-rhythm-generator-hats-and-all/17-FullRhythmGenerator.png)

So firstly, I'll point out the new stuff. We have two new tables, hatpattern and hat chance, a new message that sets up the hatchance table, a new subpatch called hatgen and then the playback section reading from hatpattern. This should all seem familiar from the snare generation and realistically it's much the same. The difference comes in how the hatchance table is created.

The setup message doesn't set the table to all zeros, but instead fills it with alternating values of 0.5 and 0.7. The outputs of the kickgen and snare are also being written to the hatchance table, the important thing to note being that whenever they generate a value that would play a kick or a snare they will write a zero out to hatchance. In this way we seed hatchance with some values to generate from, but make sure that it can't sequence any hatsounds to play at the same time a kick or a snare will play. Later I may change this so that there can be some overlap but I'm unsure yet. The contents of hatgen are exactly the same as those in snaregen, just reading and writing to different tables.

At the playback section I've got a random object and a moses object set up so that about a third of the hat triggers will play an open hat and the rest a closed. I thought about having separate rhythms for each of these but this is much simpler and still gives some good results.

I still want to extend this patch further but from here the plan is really just going to be to add in extra small things. I want to have some way of sequencing re-triggers on the kicks and some way of adding a bit of swing in would be nice. If I am going to keep this solely in PureData then I really want to improve the drum sounds. I might spend some time making a better general purpose drum machine and general sampler soon. Would be a good patch of the day I suppose.

Patch available here

[Full Rhythm Generator patch](/a/2010-11-17-patch-a-day-month-day-17-a-full-rhythm-generator-hats-and-all/17-FullRhythmGenerator.zip)
