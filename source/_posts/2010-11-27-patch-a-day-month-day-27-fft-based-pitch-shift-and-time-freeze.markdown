---
date: '2010-11-27 18:22:23'
layout: post
slug: patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze
status: publish
title: 'Patch-a-Day Month Day 27: FFT based Pitch Shift and Time Freeze'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- delay
- FFT
- FM synthesis
- patch-a-day
- pure data
- sampling
comments: true
---

Following on from yesterdays two useful FFT based patches, I have another two for you today. The first is actually really simple but quite useful, an pitch shifter that will shift sounds you send through it up. It's definitely not clean or accurate but it could well make for some cool patches when combined with other things.

The second is a time freezer patch. This has quite a bit in common with the granular synth stuff from before but this time we're replaying a block of FFT data. It's possibly more interesting just to see the implementation, which is by no means necessarily the right way to do this, but it works pretty well.



![A basic pitch shifter based on FFT](/a/2010-11-27-patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze/27-FFTDirtyShift.png)

The main patch of the pitch shifter is really very basic. The only change is that we have a number box getting 128 added to it, going through an int to make sure it's a whole number and then being passed to a shift object. This patch works by using a very short delay to shift the frequency bins along so that lower bins take the place of higher bins. The +128 is there because the effect doesn't start happening untill the delay is a minimum of 128 samples. I think this might be to do with the minimum delay allowed by delay objects in PD but I'm really not sure.

![FFT based pitch shifter internals](/a/2010-11-27-patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze/27-FFTDirtyShiftSubPatch.png)

Really all that is happening here is that the FFT data is delayed going into the inverse FFT object. By delaying by values that are less than a blocksize length we get a shifting up effect.

The time freeze has much more going on with it. What we need to do is store a block of FFT data and continuously replay this back through the inverse fft object. I chose to do this using a tabwrite~ that records the sample block when the freeze is turned on and then switches the input to the inverse fft to be a pair of tabreceive~ objects.

![FFT based Time Freeze sub patch](/a/2010-11-27-patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze/27-FFTTimeFreezeSubPatch.png)

When the freeze is turned on the sel 1 will bang the tabwrites to record the FFT block. The second toggle chooses between the normal signal or the tabreceives. pretty simple but quite effective.

![FFT based Time Freeze](/a/2010-11-27-patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze/27-FFTTimeFreeze.png)

The main patch is just using a variable delay to turn the freeze on a bit after the FM synth triggers are clicked. Click them once to play the first half of the FM tone and then again to stop the freeze and get the tail run off. On it's own this isn't so great but it's a basic building block of lots of interesting stuff. I plan to implement some stuff like this in the Granular Synth once I get a chance.

Anyway, the patches can be downloaded here for people that want them.

[FFT based pitch shift and time freeze](/a/2010-11-27-patch-a-day-month-day-27-fft-based-pitch-shift-and-time-freeze/27-FFTPitchShiftandFreeze.zip)

I think for the last three days of Patch-a-day I'm just going to do some basic tutorials on Pure Data specifics. For example, how to use abstractions effectively, and some of the useful GUI stuff that it does. Depends a bit on how much time I have tomorrow I think.
