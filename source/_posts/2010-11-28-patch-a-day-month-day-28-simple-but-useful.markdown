---
date: '2010-11-28 23:43:52'
layout: post
slug: patch-a-day-month-day-28-simple-but-useful
status: publish
title: 'Patch-a-Day Month Day 28: Simple But Useful'
wordpress_id: '229'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- delay
- patch-a-day
---

I wanted to do an interesting post about using periodic  the Mandlebrot fractal to create interesting melodies. Unfortunately a combination of time and the "sheer volume of information I was trying to learn in not much time" conspired to mean that I'm not able to do that. I'll try to get that done soon as well because it looks seriously interesting, (for more info I will point you to [here which has masses of cool stuff](http://claudiusmaximus.goto10.org/cm/) which was posted in the Pure Data IRC room on Freenode).

Anyway, since I'm not able to do that tonight and it's getting late. I'm going to throw together a couple useful little effects with a bit of a run down of how they work. Nothing ground breaking but fairly useful I hope. A basic flanger and a sample and hold controlled filter.

The Sample and Hold filter is a pretty standard piece of kit, used for making all manner of bleepy, bloopy filtery sounds. In combination with a couple of delays there's plenty of opportunity for making an ungodly noise. This should give a good indication of how to make the Sample and Hold part of the patch from a noise source and a snapshot object. In reality I could just use a rand object and it may be slightly more efficient but I don't think it makes a major difference.

![Sample and Hold Controlled Filter](/a/2010-11-28-patch-a-day-month-day-28-simple-but-useful/28-SandHFilter.png)"

The metro periodically bangs the snapshot and we get our noise sample. This gets scaled to a zero to one range and then the bit of maths to the right means we can choose upper and lower bounds for what frequencies we want it to choose. The chosen frequency gets packed into a list so we can feed it to a line to control the band pass filter.

The variables are all easily changeable, I just chose a noise source so the filtering can be easily heard.

The flanger has a little bit more maths to it in so much as we need to generate a triangle wave to control the delay amount.

![A Flanger Effect](/a/2010-11-28-patch-a-day-month-day-28-simple-but-useful/28-Flanger.png)"

By creating a second phasor wave that goes from zero to one and then using the min object to get the minimum value of the two waves we get a triangle. I've multiplied it by two to put it back to the zero to one scale. This triangle wave then gets used to control the delay speed of a variable delay, the idea being that as the delayed signal mixes with the original there will be a comb filtering effect. The speed of the phasor controls how fast the swooshing happens and the length of the delay controls the depth.

I've added in a tabwrite and an array so you can see the triangle wave as well as putting the Karplus-Strong string synth from previously to show how it all sounds on something that isn't noise.

And that's all for tonight I'm afraid. I hope to take this Patch-a-Day month out on a high my covering the Mandlebrot stuff but I'll have to see how much I can learn about what I need tomorrow.
