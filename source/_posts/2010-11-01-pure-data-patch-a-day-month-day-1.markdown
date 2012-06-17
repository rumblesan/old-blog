---
date: '2010-11-01 20:58:49'
layout: post
slug: pure-data-patch-a-day-month-day-1
status: publish
title: 'Pure Data Patch-a-day Month Day 1: FM Bells'
wordpress_id: '105'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- FM synthesis
- patch-a-day
- pure data
---

So I've decided that November is going to be Patch-a-day month for Pure Data. Every day create a new patch of extend one that I've previously done in the month. I'll aim to use a wide range of the objects available and may even try diving into some of the computer music theory books I have to pull some techniques out. To kick things off I'm going to do some simple FM bells.



![FM Bells](/a/2010-11-01-pure-data-patch-a-day-month-day-1/01-Bells.png)"

This is a pretty simple patch using standard FM stuff but with a bit of a twist. There are three example sounds here, the arguments that get unpacked being:-



	
  1. Base frequency

	
  2. Frequency Modulation ratio

	
  3. Modulation amount

	
  4. Squareness


We chose the initial signal frequency and then multiply this by the frequency ratio, this feeds an oscillator which is then amplified and clipped. We can set the value of the amplification meaning that we can make the signal more like a square wave if we want. Because of the extra harmonics in the square wave the output signal will be more complex and interesting. The Modulation amount controls how much the base frequency is modulated. By carefully choosing values for our Modulation ratio we can get some interesting bell like tones.

The Envelop of this sound is created using the vline object. The output value starts at zero, goes up to one in ten milliseconds and then goes back down to zero over the next eight hundred milliseconds. using the multiple object this envelope signal is actually squared so that the curve is more exponential and sounds a bit better.

So that's one down, 29 left to go. I'm actually going to try and stick to this, seems a good way to just learn a whole bunch of stuff. I'm also going to try and improve the stuff in the separate resource pages. Two links in each is pretty pitiful. Better pull my finger out.

Until tomorrow.
