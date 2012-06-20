---
date: '2010-11-16 20:18:05'
layout: post
slug: patch-a-day-month-day-16-rhythm-generator-with-snares
status: publish
title: 'Patch-a-Day Month Day 16: Rhythm Generator with Snares'
wordpress_id: '173'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- audio
- drums
- generative
- patch-a-day
- pure data
- sequencing
comments: true
---

So the extension to yesterdays rhythm generator is here, and I'm pretty pleased with it. It uses the same sort of techniques as yesterday but with a new way of generating the chance data. It's probably easier to just look at it first of all.



![Rhythm Generator with Kick and Snare](/a/2010-11-16-patch-a-day-month-day-16-rhythm-generator-with-snares/16-RhythmGeneratorKickSnare.png)

So the first thing to notice is that the patch is a bit clearer thanks to moving most of the code into sub patches. The parts from yesterday that generate the kick patterns are mostly untouched inside the kickgen subpatch. I've moved the messages to clear the pattern tables and the snarechance table into the cleartabs subpatch and the kickgen subpatch itself just outputs the values we need to set to 1 in the pattern table.

When a value is sent out it also gets sent to the group of objects on the right. These use it to write some data to the snare chance table, and by adding to the index value it can write data to multiple points after where the kick will trigger. In this way we can have some variation as to where the snares might occur after each kick is played. The values for position and chance here need to be tuned but the results at the moment aren't too bad. I'm going to be fixing this up to hopefully use as a live patch so I'll work on choosing better numbers later.

The snaregen subpatch holds the rest of the magic here but is probably pretty obvious at this point.

![Snare Pattern Generator](/a/2010-11-16-patch-a-day-month-day-16-rhythm-generator-with-snares/16-SnareGen.png)

This is pretty much reusing code from the kickgen patch. An until object is used to count up from zero to 31, pull the values out of a table and compare them to a random number. If the random number is smaller than the table data then pack a one in with the index value, otherwise pack in a zero. This data gets written directly to the snarepattern table and then the sequencer on the left plays it back.

Patch is available below for those that want it. Tomorrow I intend to add functionality for hi-hats and maybe some other sounds. I'm not yet sure how I'll end up using this, whether a stand alone PD thing or maybe with other sound sources but I've got plenty of time to decide.

[Kick and Snare Rhythm Generator](/a/2010-11-16-patch-a-day-month-day-16-rhythm-generator-with-snares/16-RhythmGeneratorKickSnare.zip)
