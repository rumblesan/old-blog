---
date: '2010-11-20 19:13:02'
layout: post
slug: patch-a-day-month-day-20-granular-synth-with-enveloping
status: publish
title: 'Patch-a-Day Month Day 20: Granular Synth with Enveloping'
wordpress_id: '190'
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

So the patch for yesterday is now published. Apologies about that, I went to bed assuming I had done it but must not have. Today's patch will carry it on so if you haven't read the previous entry yet I recommend doing so.

The code for this piece is pretty much lifted from the PureData help files, which is a bit cheeky but it's useful stuff so I think it's a good idea to draw your attention to it. As well as that it just makes for a better synth. Enveloping and grain phase are the plan for today.



![Granular Synth with volume envelope](/a/2010-11-20-patch-a-day-month-day-20-granular-synth-with-enveloping/20-GranSynthWithEnvelope.png)"

So the only change to the main section of the patch is the addition of the envelope array and some objects that write into it. The array is 44100 samples long and the collection of objects next to it will write in one cycle of a sin wave. The sin wave frequency is set to 100 Hz so that it exactly fills up our array with 441 samples, we also set the phase to zero and add on 0.5 so that it will begin and end at zero. This way it ramps smoothly up and then back down.

![Grain player with envelope](/a/2010-11-20-patch-a-day-month-day-20-granular-synth-with-enveloping/20-GrainPlayerWithEnvelope.png)"

The major changes are to the Grainplayer abstraction. For a start the patch now has two grains playing at 180 degrees out of phase. This is done by adding 0.5 to the output of the phasor and then running it through the wrap~ object. Wrap~ will output the modulus of the input signal so that it stays between 0 and 1. By adding 0.5 and wrapping it, the signal to the second grain will always be 180 degrees ahead of the first meaning that they will overlap and keep a more constant tone.

The volume envelope is created by reading data out of the envelope tab and multiplying this with the audio output. the zero to one value of the phasor is multiplied by 441 so that it matches the number of samples in the table. This means that the volume envelope will exactly match the length of the grain being played back.

So there we go, short and pretty simple. Tomorrow I'm going to spend a bit of time working on the LFOs and then start adding multiple grain players to try and get some interesting audio going.
