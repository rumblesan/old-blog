---
date: '2010-11-03 18:50:50'
layout: post
slug: patch-a-day-month-day-3-simple-mono-synth
status: publish
title: 'Patch-a-Day Month Day 3: Simple Mono Synth'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- patch-a-day
- pure data
- synthesis
comments: true
---

So tonights patch is a small quick one because I'm running late for "Real World Stuff" and probably wont have time later. I decided to do something that I can easily build on later and that also provides a simple jumping off point for other people learning. In the next couple of days this will probably get hooked up to the previous Markov notes patch.



![Mono Synth](/a/2010-11-03-patch-a-day-month-day-3-simple-mono-synth/03-MonoSynthVoice.png)

The noise making part of this patch is the line~ object feeding the phasor~ oscillator. The line gets fed a list with a number it needs to reach and a time in which to reach it and this gives us some nice 303 style slides when moving between notes. The phasor~ feeds into a multiplier and then a clip object so we can vary the distortion on it and change the tone of the sound. The envelope generation is another line~ object which gets a bang to trigger the increase and has a variably delayed bang to trigger the decrease.

I didn't add a multiply object to this because I forgot and by the time I'd taken the screen cap it was already later than I wanted, I'll do that tomorrow. There are lots more variables and control stuff that we could add here but time is short, and I cant do everything for you.

Come back tomorrow for more
