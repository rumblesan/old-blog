---
date: '2010-11-09 21:30:53'
layout: post
slug: patch-a-day-month-day-9-more-fun-with-delays
status: publish
title: 'Patch-a-Day Month Day 9: More Fun with Delays'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- delay
- FM synthesis
- generative
- patch-a-day
- pure data
- sequencing
comments: true
---

So I've extended the patch from last night with a few more sounds and another delay section in the chain. I think I'm going to leave this as it is for now and try to start on something else tomorrow. I've also put some audio up on SoundCloud for those that want to hear this and the extended patch is again download-able. This can turn out some quite interesting sounds sometimes and I'm quite pleased with it.



![More Delay Fun](/a/2010-11-09-patch-a-day-month-day-9-more-fun-with-delays/09-MoreDelayFun.png)

The image of the patch is pretty big now so click on it to see everything. I spent some time cleaning it up so it's a bit easier to follow and figure out.

The bell sounds are pretty much the same as the stuff seen previously, I modified them to have a longer attack and ran them through a low pass filter to take the edge off. The RandBangs and delay objects help to limit the number of bell sounds that get through so the whole thing doesn't get swamped by them.

The extra delay section is controlled by a very slow LFO which is the combination of two sin waves, the frequencies of which are randomly chosen at the startup of the patch.

Now for the sounds, let's try the SoundCloud widget again and if that doesn't work then go to [http://soundcloud.com/tasteforreality/delaycation](http://soundcloud.com/tasteforreality/delaycation)

[soundcloud][http://soundcloud.com/tasteforreality/delaycation](http://soundcloud.com/tasteforreality/delaycation)[/soundcloud]

The patch can be downloaded here

[More Delay Fun Patch](/a/2010-11-09-patch-a-day-month-day-9-more-fun-with-delays/09-MoreDelayFun.zip)

Tomorrow I've decided I'm going to try and have a play with some of the Fourier transform stuff that Pure Data has. I've got a couple ideas to try so it should keep me busy for a few days.
