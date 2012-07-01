---
date: '2010-11-27 01:26:42'
layout: post
slug: patch-a-day-month-day-26-fast-fourier-transform-finished
status: publish
title: 'Patch-a-Day Month Day 26: FFT based EQ and Delay'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- delay
- FFT
- FM synthesis
- noise
- patch-a-day
- synthesis
comments: true
---

Finally, I have some interesting FFT based patches for you, and they're pretty cool as it happens. Full disclosure, these are pretty much lifted from the [Fourier Analysis](http://www.pd-tutorial.com/english/ch03s08.html) section on [PD-Tutorial](http://www.pd-tutorial.com) which is really worth a good read. These are the two things that interested me the most because they make all sorts of interesting sounds. I'll be including the patches so you can down load and investigate.

First up, a graphical EQ using the Fourier Transform to split the incoming signal into multiple frequency bands. The blocksize used is 512 so we have 256 frequency bands to play with. All that we need to do is create an array of 256 values and and then use a tabreceive~ to pull the data out of the EQ array and multiply the frequency data.

![A Fourier transform based Graphical EQ](/a/2010-11-27-patch-a-day-month-day-26-fast-fourier-transform-finished/26-FFTGraphicEQ.png)

Here you can see the main patch with the EQ array, which I've cleaned it up a bit so the enveloping and FFT stuff are in subpatches. There's a noise source and I've also used some of the FM synthesis stuff from a patch earlier this month. Here's the subpatch doing the FFT parts but there's really not much of a change.

![FFT based Graphical EQ internals](/a/2010-11-27-patch-a-day-month-day-26-fast-fourier-transform-finished/26-FFTGraphicEQSubPatch.png)

It literally is as simple as that! I think it's worth spending a moment to point out how the multiplying together of the audio data happens here however.

The data out of the FFT is, as far as PD is really concerned, exactly the same as all the rest of the audio data. The blocksize in this subpatch is bigger, but all PD sees is a block of 512, floating point values between 1 and -1. The tabreceive~ object will continuously read a block of data from the EQ array, which in this case will be 256 values between 0 and 1 and then the last 256 of just 0 since the array isn't that big. PD will multiply these two blocks together sample by sample, so that the values from our EQ array will change the correct frequency bins.

So with that bit of basics explained, have a look at the spectral delay. This is very simple as well, the only control is delay time, no feedback or dry/wet but it's really not hard to add them in if you want.

![FFT based Spectral Delay](/a/2010-11-27-patch-a-day-month-day-26-fast-fourier-transform-finished/26-FFTSpectralDelay.png)

The main part of the patch looks almost exactly the same as the graphical EQ, the only differences being that the big array is now called Delay, and it's values go between 0 and 100. the subpatch is where the new magic happens.

![FFT based Spectral Delay internals](/a/2010-11-27-patch-a-day-month-day-26-fast-fourier-transform-finished/26-FFTSpectralDelaySubPatch.png)

The data output from the initial Fourier Transform is written to two delay lines, one for each data stream. The tabreceive this time reads the data from the tab, but it then runs it through some basics maths. We are using it to control the variable delay for each frequency bin, but we want to be making sure that the data for a given frequency bin stays in that frequency bin, otherwise we will get pitch shifting (which could be cool but it's not what we're after right now).

To do this we make sure that the value is a whole integer by using wrap~ to get the decimal value of the signal and subtract this from the original number. By then multiplying by 512 we make sure that the delay is always delaying the data to the correct point in a later window. Finally, we can divide by the samplerate to get the delay time in seconds and multiply by 1000 to get the delay in milliseconds (here it's just done in one step). This data is passed to the variable delay objects which then pass it out to the inverse Fourier transform.

Both the patches can be downloaded

[FFT based EQ and Spectral Delay patches](/a/2010-11-27-patch-a-day-month-day-26-fast-fourier-transform-finished/26-FFTEQandDelay.zip)

I recommend extending them as you see fit, there's loads of scope for cool sound making here. Tomorrow I'm going to try and make an FFT based freeze effect and a basic pitch shifter. After that I think I'll leave the FFT stuff which gives me three days to fill with something interesting until the end of Patch-a-day month. I'll ponder it later.
