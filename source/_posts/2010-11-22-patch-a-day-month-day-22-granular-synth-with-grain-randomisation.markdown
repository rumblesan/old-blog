---
date: '2010-11-22 21:06:17'
layout: post
slug: patch-a-day-month-day-22-granular-synth-with-grain-randomisation
status: publish
title: 'Patch-a-Day Month Day 22: Granular Synth with Grain Randomisation'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- granular synthesis
- patch-a-day
- pure data
- sampling
- synthesis
comments: true
---

So the granular synth posts continue as I build up this noisy machine. It's nearing a state of completion now where I'll make the patch down-loadable and put a few examples up on SoundCloud. There are a few bits and pieces that I want to do yet but I think that this will be the last Patch-a-day post about it. Don't want to bore anybody after all.



![Granular Synth with Grain Randomisation](/a/2010-11-22-patch-a-day-month-day-22-granular-synth-with-grain-randomisation/22-GranSynthWithRand.png)

So I've spent a bit of time just cleaning up the interface, part of that has been using the receive-symbol options in all the number objects so that the loadbang and message on the right can set values for the controls when the patch loads. I've also pulled the LFO controls out of the sub-patch so they're easily accessible.

The new stuff is the Rand controls and the multiple grains that are there now. The GrainPlayer abstraction now has randomising functionality on a per-grain basis. This means that when randomised the grains will be playing slightly different sample sections at slightly different speeds which results in a very interesting sound. This is implemented in a similar way to the LFOs.

![Grain Player with Parameter Randomisation](/a/2010-11-22-patch-a-day-month-day-22-granular-synth-with-grain-randomisation/22-GrainPlayerWithRand.png)

The grain speed and grain start parameters are both being modified but this time our source is a noise~ object. When the startRand or speedRand buttons are pressed we take a snapshot of the noise, this gets multiplied by 0.9 to set the absolute limits, then multiplied by the modulation amount and finally offset to centre around a value of one. This results in all our grains having a differing value for their speed and/or grain starting position, but all centring around the chosen global value.

Playing around with this it's pretty easy to get some dense sounding grain clouds, even with only the six grains currently there. I'm planning on adding a similar system to this for stereo panning to get some spread amongst the grains, probably with some LFO modulation as well. I'd like to have some per-grain LFOs as well thinking about it so that there's the possibility to have different grains coming in and out of the sound. Maybe it's worth looking at some frequency modulation of grains? I'll investigate at some point.

One of the things I definitely want to add is the ability to globally change the start position of the grains so as to move through the sample. It shouldn't be difficult to do and will result in there being the ability to have more obvious movement. Either way, I'll be leaving the granular synthesis out of Patch-a-day month for now and just put stuff up here once it's done.
