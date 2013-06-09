---
date: '2010-11-30 22:25:14'
layout: post
slug: patch-a-day-month-day-30-audio-fractals
status: publish
title: 'Patch-a-Day Month Day 30: Audio Fractals'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- chaos theory
- delay
- FM synthesis
- generative
- patch-a-day
- pure data
comments: true
---

And now I come to the final entry in my month of patching. It's been loads of fun but felt a little bit gruelling at some points if I'm honest. I've definitely learnt a huge amount in the last thirty days and my knowledge of Pure Data has improved hugely. I'll not be surprised if I do this again at some point next year.

Anyway, tonight's patch follows on in some ways from last night, but also has much to do with my thinking about the Mandlebrot set over the last couple of days. This is more like tentative exploration and philosophising than lessons or patches but it may prove interesting and useful to some.

When I looked further in to how people have used fractals in music, it seems that much of it involved taking the equations used to calculate the Mandlebrot set and then mapping these values to frequencies. I can see the logic in this and I'm sure it can be used to create some very interesting patterns but it felt a little detached to me insomuch as the maths and the audio aren't specifically related, just manually joined. When I started thinking more about what I felt a fractal to be I realised that, at it's core, it is just a structure that has great complexity and comes from feeding the result of an operation back into itself. Iterating in this way is what produces the end results, so I decided to apply this idea to sound.

The result of the first try was this patch.

![A patch to try and create an audio fractal](/a/2010-11-30-patch-a-day-month-day-30-audio-fractals/30-AudioFractal1.png)

A simple FM synth with the output being fed back into the input through a long delay was the starting point I chose. The output is multiplied to get it into a greater range and then used to modulate the initial frequency, the idea being that the system will iterate through this process, possibly arriving at an interesting tone, possibly just carrying creating interesting patterns. I haven't explored this as far as I would like but I feel that the possibilities of finding something surprising are high.

I made two extensions to this, after finding that manually playing with the frequency parameter to generate a quickly changing frequency created more chaotic patterns as it fed back. I also tried playing with the delay size but found that this gave less interesting results.

![An extension to the audio fractal patch](/a/2010-11-30-patch-a-day-month-day-30-audio-fractals/30-AudioFractal2.png)

The final extension was to have the original frequency control for the synth be removed after the random tones had been put into the system meaning that the whole thing was running just off the first sounds. This seems to make the output take a bit longer before it turns into a constant drone sound. The examples that I found all eventually become a fairly constant sound but there is quite a bit of movement within it. I don't know if this really qualifies it as the self similarity that you might look for in a fractal but it is interesting to hear the points of equilibrium.

![Final extension to original audio fractal patch](/a/2010-11-30-patch-a-day-month-day-30-audio-fractals/30-AudioFractal3.png)

I want to keep exploring the possibilities here. I'm sure that with a bit more tweaking and experimenting this pretty basic patch will turn up some interesting results. I'm going to be building more patches like this, trying to find a good balance between simplicity of the patch and complexity required to make the sort of sounds I'm hoping for. This will definitely be an ongoing thing.

The patches are available and I recommend having a play with them.

[Audio Fractal Patches](/a/2010-11-30-patch-a-day-month-day-30-audio-fractals/30-AudioFractals.zip)
