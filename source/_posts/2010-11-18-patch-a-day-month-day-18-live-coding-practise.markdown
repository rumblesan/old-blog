---
date: '2010-11-18 20:51:19'
layout: post
slug: patch-a-day-month-day-18-live-coding-practise
status: publish
title: 'Patch-a-Day Month Day 18: Live Coding Practise'
wordpress_id: '184'
categories:
- Live-Coding
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- audio
- generative
- livecoding
- patch-a-day
- pure data
comments: true
---

So This might be a bit of a cop out but I'm currently writing this on Tuesday night under the assumption that I'm going to be busy at the pub on Wednesday evening and looking at arty things on Thursday so I'm allowing a bit of leeway due to time constraints. This evening I decided to have a go at practising some Live-Coding and realised that Once Patch-a-Day month is over, it might be a good idea to start semi regular entries on the subject, perhaps with videos as well. I'd like to do it in languages other than PureData but I'll need some time to get up to speed with them first. Anyway, here's a picture of the patch I constructed tonight and a bit of blurb about how it works.



![Live Coding Practise 16-11-2010](/a/2010-11-18-patch-a-day-month-day-18-live-coding-practise/16-11-2010.png)

The first parts to be built were the three counters in the upper left, duplicate three of them and I've got a sequencer of some sort to build off.

The contents of the click subpatch are shown at the bottom of the picture, just a noise source feeding a vcf~ object which gets triggered by a vline~. Inside the click patches there is a select that triggers of about eight numbers I picked out, roughly spread between 0 and 99. The two click patches also have slightly different frequency peaks and envelope times to get a bit more variation.

The third counter is controlling the drum subpatch. The sound is made by having the envelope from the vline~ control the frequency of the filter, it's not great but it does a reasonably good job of being percussive. I need more practise at making these on the fly I think.

The other bits around here are some more counters which will periodically change the length of some of the first counters. It didn't work quite as well as I'd hoped but the idea is one I'll try to reuse.

The other half of the patch is two delay chains which helped to fill in quite a bit. These were simple to make and I'll be practising making these for future use. I realised when writing this up that i should have set the values in the delwrite~ objects much higher but that's something to remember for next time.

So there's the basis of what I did. I'll keep practising and try to find some videos of other people's performances to show and learn from and eventually start putting my own up.
