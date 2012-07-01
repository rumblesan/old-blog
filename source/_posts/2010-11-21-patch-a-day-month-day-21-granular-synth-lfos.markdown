---
date: '2010-11-21 17:32:28'
layout: post
slug: patch-a-day-month-day-21-granular-synth-lfos
status: publish
title: 'Patch-a-Day Month Day 21: Granular Synth LFOs'
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

Today I added the LFOs to the granular synth patch, and whilst they're pretty simple, they leave plenty of room for extension. I think that it's useful to show some of the thinking that went into this and that really the patch building is secondary to the designing, but then maybe I'm a little bias, let me know if you think so.

I've created the LFOs in a subpatch so I'll just show that for today.



![Granular Synth LFOs](/a/2010-11-21-patch-a-day-month-day-21-granular-synth-lfos/21-GranSynthLFOs.png)

So all the LFOs are the same here, a simple sin wave that will modify the values it's patched in to. The important thing to remember is that we can't design these based on knowing what the value they need to modify will be so for this reason the initial values are multiplied by the LFO, instead of having it add its value to them. This raises the new problem that we cant have the LFO reach a zero value, otherwise we end up with a grain that won't play because its speed is zero, or it's trying to play back no samples.

The other thing to remember is that we want to vary the amount that the LFO affects the parameter, but we don't want to be causing the zeroing problem if we set the modulation amount to zero as explained above. The answer is to move the center point around which the LFO moves. If we add one onto the value then when we set the modulation value to zero, the incoming parameter is multiplied by one and there is no change. It's also important to note that even if we add one to the signal value, when the LFO hits minus one we would still be having the zeroing problem. Multiplying the signal by 0.9 and then adding the one gets around this.

To have the LFOs affect the grains, I've changed the names of the send and receive objects so that the grains only get the output of the LFOs, not the signals direct form the controls.

Today's post is a bit light if I'm honest, but a substantial headache has settled and listening to the output of the grain synth isn't really helping. Hopefully I can make up for it tomorrow.
