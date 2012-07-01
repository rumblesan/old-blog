---
date: '2010-11-05 23:49:11'
layout: post
slug: patch-a-day-month-day-5-user-drawable-lfo
status: publish
title: 'Patch-a-Day Month Day 5: User Drawable LFO'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- patch-a-day
- pure data
comments: true
---

This patch is a pretty simple one, but it's a pretty useful one and introduces a couple of new objects and concepts. A user drawable LFO, the idea being that you can draw the shape of the waveform you want in the graph and set the speed of the playback. At the moment it just gives the output to the snapshot object but it can be built into lots of things. I'll have a go at getting some FM sounds out of it soon but for now, lets keep it simple.



![User Drawable LFO](/a/2010-11-05-patch-a-day-month-day-5-user-drawable-lfo/05-DrawableLFO.png)

So the important part here is the tabread4~ object and the graph. The graph has 100 points in it with values ranging between -1 and 1, the tabread is set up to read the values out of the graph. The phasor~ object will output a value between 0 and 1 which we multiply by 100 so that we can plug it straight into the tabread4~ and it will run through all the elements there. the output of the tabread4~ gets run through some maths so that it ends up going between 0 and 1.

The tabread4~ object has the 4 because its actually using 4-point polynomial interpolation. I'm unsure of the maths involved here but it means that we could actually feed it floats and it would interpolate between the values we've drawn for smoother curves. Maybe something for later.

The only other bit of clever stuff is the top where the toggle, trigger, multiple and number objects are combined so that the toggle will turn the LFO on and off and the number box can be used to change the playback frequency whilst the whole thing is running.

Very simple but pretty effective.

Anyway, I've been ill today and just want to eat chocolate and read right now so I'm disappearing. Tomorrows post will be earlier than this one as I'm out and about tomorrow evening. Probably going to have to get Sunday's patch sorted early as well. Better stop moaning and get patching hehe.
