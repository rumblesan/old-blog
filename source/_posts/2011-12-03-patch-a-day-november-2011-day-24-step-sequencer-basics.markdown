---
date: '2011-12-03 23:37:32'
layout: post
slug: patch-a-day-november-2011-day-24-step-sequencer-basics
status: publish
title: 'Patch-a-Day November 2011 Day 24: Step Sequencer Basics'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- launchpad
- sequencer
comments: true
---

I've just noticed I think I missed out a day somewhere.... This patch is patch 25 in my repository, but it's day 24.... Looks like I made a patch titled Improved presets and haven't written it up but oh well. I might go back and slot it in if I think it's missed out anything vital.

On with the step sequencer for the moment though. I'm designing this to run on my Novation Launchpad, the plan being to have eight tracks with 64steps each. Track selection will be done by the left hand row of function buttons and all track steps displayed on the grid. The first thing to do is work out how the pattern will be stored, and I've decided that the data structures are the right way to go about doing it. Below is the beginnings of the patch.

![Beginning of the data structure sequencer](/a/2011-12-03-patch-a-day-november-2011-day-24-step-sequencer-basics/data-structure-sequencer-beginnings.png)

Structure and datawindow patches in the top left corner, struct has eight float fields named **a** to **h**. The central section just clears our window and creates the data for the 64 steps. The section on the right is just to that I can write out the data to a file for debugging and won't be there in the final patch.

The group of daisy chained objects on the left hand side are dealing with saving and loading the data about individual tracks. The left hand inlets/outlets deal with setting individual steps for specific patterns. The middle is so the object can receive a pointer to a specific step and load the value from it, the right hand inlets/outlets are where this data comes from. For the moment only the saving works, though the loading doesn't need much more done.

![Basic track abstraction](/a/2011-12-03-patch-a-day-november-2011-day-24-step-sequencer-basics/track-abstraction.png)

I've realised that in patch comments are probably a good idea heh, so I've started adding them. As they show, the creation arguments for the abstraction are the name of the data window, the name of the struct and the name of the field to set or get.

One of the things I decided for this was that the functionality for getting the right pointer when setting a value should be inside the abstraction, but when getting the value the pointer should come from outside. My reasoning was that when getting the value from a step we're actually going to want to get the value from all the steps and, because they would all use the same pointer, it would be wasteful to repeat that functionality. When we're setting a value we're usually just doing it for one track so it's simpler to contain that inside the abstraction.

The abstractions all use the passthrough design so when a message comes into the left hand inlet it is routed to the correct place by checking for the field name. From here the step position triggers a standard traverse->until>next style setup and then the value is set using the set object. Try sending some messages in and then saving the data to a file so you can have a look. This works pretty well and should mean the entire sequencer itself will be pretty compact.

Tomorrow I'll get the the retrieving side of it done, then time to start on interfacing it with the launchpad.
