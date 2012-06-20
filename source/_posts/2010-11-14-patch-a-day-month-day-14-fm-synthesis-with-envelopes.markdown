---
date: '2010-11-14 20:07:07'
layout: post
slug: patch-a-day-month-day-14-fm-synthesis-with-envelopes
status: publish
title: 'Patch-a-Day Month Day 14: FM Synthesis with Envelopes'
wordpress_id: '165'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- FM synthesis
- patch-a-day
- pure data
- synthesis
comments: true
---

So I'm revisiting the very first patch I made with the FM synthesis stuff. This time I've removed the square wave part of it and I'm adding in some envelopes to control the frequency modulation ratio. With this we can get some really interesting sounds happening with very little extra complexity. If I'm honest, this idea is mostly again pulled from the SimpleFM examples in the Max documentation. This idea is also used in one of the Autechre Max patches kicking about on the internet to synthesise some cool drum sounds. I haven't spent much time making cool presets but this is full of possibilities for extending.



![FM Synthesis with envelopes](/a/2010-11-14-patch-a-day-month-day-14-fm-synthesis-with-envelopes/14-FMSynthEnvelopes.png)"

So the obvious addition is the four arrays that are present, easily called env1, env2, env3 and env4. I've removed the clip object for the moment and I've also hard coded the modulation amount to 0.9 just to have less other stuff going on.

The envelope arrays are all 400 samples long and the values are all between 0 and 1. When the message is unpacked, the first argument will set the envelope that the tabread4~ is to read from. The second will bang a message into the vline~ that just tells it to run from zero to 400 over 400 milliseconds. This can be lengthened and the arrays made larger so that longer lasting sounds can be created if need be.

Other than that, the rest of the patch is pretty much the same. The modulation index will change over time now which can lead to some pretty cool and interesting effects. I'd like to turn this into an abstraction with the ability to have a few more modulation envelopes and some other interesting things. Then I can just drop it into other patches I make for some good sounds possibilities. Until then, I leave it to you to investigate as I need food.
