---
date: '2010-11-08 23:51:00'
layout: post
slug: patch-a-day-month-day-8-fun-with-delays
status: publish
title: 'Patch-a-Day Month Day 8: Fun with Delays'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- delay
- generative
- pure data
- random
comments: true
---

So The other night I started playing with delays in Pure Data but was quickly annoyed because they weren't working as I was hoping or expecting. Thankfully, when I came to do some reading today it turns out that it was my fault for using the delread~ object when what i actually wanted was the vd~ object. VD here stands for Variable Delay, and what I wanted to do was to start altering the delay speed with some constantly changing signals. I'm baking up something pretty big that I'll try to have finished soon but for tonight I thought I'd do a brief patch with vd~ and make some noise.



![Fun with Delays](/a/2010-11-08-patch-a-day-month-day-8-fun-with-delays/08-DelayFun.png)

So the hats abstraction makes a reappearance and I'm also using one called blip. This generates clicks and pops by having very short sections of sin waves play, subtle but useful in things like this. These get randomly triggered using the BangRands and a metro. The delay part of the patch is a bit of a mess but revolves around the vd~ and the delwrite~ objects.

The audio gets written to a delay buffer by delwrite~, the vd~ object will read the audio out of it with a delay time based on the signal input to it. This delay time is chosen randomly and changes every so often. When it does the value will smoothly ramp up or down thanks to the line~ which generates some pretty interesting textures and sounds. The sound of the hats and blips are fed to both delays, which are cascaded one into the other.

I want to work some more stuff into here so there are tones and drones as well as the noise. I might try to get to that for tomorrow night. The patch can be found [here](/a/2010-11-08-patch-a-day-month-day-8-fun-with-delays/08-DelayFun.zip).
