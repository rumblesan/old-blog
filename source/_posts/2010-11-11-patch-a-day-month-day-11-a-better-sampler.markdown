---
date: '2010-11-11 23:48:04'
layout: post
slug: patch-a-day-month-day-11-a-better-sampler
status: publish
title: 'Patch-a-Day Month Day 11: A Better Sampler'
wordpress_id: '148'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- drums
- patch-a-day
- pure data
- sampling
comments: true
---

So today I'm extending yesterdays patch by adding a few basic controls. Still nothing major but it shows a couple things, speed variation, start offset control and looping. It's pretty crude so tomorrow I'll be rebuilding it in a better form, but have a look at what's here at the moment.



![Better Sampler](/a/2010-11-11-patch-a-day-month-day-11-a-better-sampler/11-BetterSampler.png)

First things first, I've changed to a simple line~ object from the vline~ and now whenever the bang is hit it will automatically set the line~ value to go to zero. Makes things a bit easier to use.

The speed control changes the value we give the line as its second argument. Making this time longer or shorter will make the speed faster or slower respectively.

For the start offset we need to do two things, firstly decrease the number of samples played which we do right at the top. Secondly we actually have to increase the sample number that the playback will start from. This is done by adding a signal to the output of the line at the bottom. Tomorrow I'll go about adding length of playback functionality but I left it out for tonight.

Lastly we have the looping, which is a bit scrappy but works. When the playback time is calculated, we can choose to have this set up a delayed bang by opening or closing the spigot. If we open the gate, the value passes through where it is used to set the length of a delay and then to send a bang into that delay object. The output bang should coincide with the ending of the sample, at which point it will go and start the playback again.

So that's all for tonight. Tomorrow I'll try to turn this all into a useful abstraction but now I need sleep.
