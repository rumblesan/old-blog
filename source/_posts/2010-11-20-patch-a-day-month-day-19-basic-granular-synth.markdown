---
date: '2010-11-20 18:54:34'
layout: post
slug: patch-a-day-month-day-19-basic-granular-synth
status: publish
title: 'Patch-a-Day Month Day 19: Basic Granular Synth'
wordpress_id: '186'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- granular synthesis
- patch-a-day
- pure data
- synthesis
comments: true
---

I'm just coming to do today's patch and I've realised that I never actually published this yesterday, it got left in the drafts. So here it is I suppose, a bit late but ready. Today's post which I'm just about to write up carries on from this so this is fairly important heh.

So I'm planning on spending the next couple of days rebuilding a granular synthesis patch I wrote in MaxMSP a while ago. This will partly be so I can extend and improve it, but also because this patch was actually my initial reason for learning SuperCollider so I'm going to spend some time prototyping what I do to it with an aim to port it over once I'm done.

Much of today's patch will look like the sampler abstraction and that's because really it is. The stuff here is actually a pretty big improvement on the sampler abstraction so consider it a follow on from that.



![Basic Granular Synth](/a/2010-11-20-patch-a-day-month-day-19-basic-granular-synth/19-BasicGranularSynth.png)"

So really there's nothing here, the important stuff is in the GrainPlayer abstraction but it's worth pointing out how I'm doing some of the maths here. The start position is specified as a percentage position of the total file length, as is the grain length. (Please note, I've realised that there is a mistake in the patch and there should be a divide by 100 object on the length section. I'll get that fixed later..... probably.)

One of the things I will be adding later are a few LFOs that will modulate the length, speed and position of the grains that are being played. The issue with this is that if you choose a section of the sample to use as a grain that starts or ends too close to the start or end of the sample, the LFOs can end up hitting that limit. To get around this I've decided that a grain cant have a starting position in the first or last five percent of the main sample and it cant be longer than four percent of the sample length.

![Basic Grain Player](/a/2010-11-20-patch-a-day-month-day-19-basic-granular-synth/19-GrainPlayer.png)"

The grain player is really just like our sample player abstraction, except that here we use a phasor~ instead of a line. In truth this is a much better way of doing things and I should revisit the sampler to improve it. The length specified is the length of the grain section to play back. Because this is specified in samples, we need to convert it to a frequency to pass to the phasor~. This is done by dividing 44100 by the length value. This value can also be multiplied by the speed value at this point.

The output from the phasor~ is then multiplied by the desired length of the grain and a starting offset added. Pump it into a tabread and everything is go.

As well as adding some LFOs to this I'm also going to be doing some volume envelope control as well as showing how to play grains out of phase to help thicken the sound and also to do some interesting stereo panning. Until tomorrow, I leave you with a piece I made with the previous patch.

[Compulsion](http://soundcloud.com/tasteforreality/compulsion)

[soundcloud][http://soundcloud.com/tasteforreality/compulsion](http://soundcloud.com/tasteforreality/compulsion)[/soundcloud]

