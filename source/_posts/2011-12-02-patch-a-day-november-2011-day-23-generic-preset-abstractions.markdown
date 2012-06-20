---
date: '2011-12-02 23:19:03'
layout: post
slug: patch-a-day-november-2011-day-23-generic-preset-abstractions
status: publish
title: 'Patch-a-Day November 2011 Day 23: Generic Preset abstractions'
wordpress_id: '411'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- presets
comments: true
---

Back on the case finally. Too many things on the go and fairly behind on Patch-a-Day. I'm planning on getting quite a few patches built this weekend so I should be finished with the 30 days by mid way through next week, hopefully.

Anyway, this evenings patch is an extension of the preset saving that we've been looking at. I realised that actually it was very easy to move the get and set objects into their own abstractions for each preset value you're interested in saving. It's using the same sort of passthrough design I've talked about and it results in much less clutter and much more useful code I feel.

![Individual preset parameter abstractions](/a/2011-12-02-patch-a-day-november-2011-day-23-generic-preset-abstractions/improved-preset-abstractions.png)"

The bottom section is what's actually in the preset-param abstraction. This time the loading and saving are being triggered by a pointer sent into either the left side for saving, or the right side for loading. The param objects still get and set their values using the send and receive objects and now it's very simple to add more parameters to store in our preset.

I'm probably going to turn the file loading/saving and structure clearing section into an abstraction as well, at which point this should all work as a fairly generic solution. There are a few other things I think could be added but I'm probablly going to be leaving this for the time being.

I've decided over the weekend I'm going to build up a sequencer based on my Novation launchpad and using the data structure and preset stuff I've been learning. Tomorrow is a new day, full of patching!
