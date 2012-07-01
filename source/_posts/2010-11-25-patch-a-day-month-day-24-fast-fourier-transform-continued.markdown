---
date: '2010-11-25 00:01:10'
layout: post
slug: patch-a-day-month-day-24-fast-fourier-transform-continued
status: publish
title: 'Patch-a-Day Month Day 24: Fast Fourier Transform Continued'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- FFT
- lessons
- maths
- patch-a-day
- pure data
comments: true
---

Today I'm going to be getting to grips with the idea of windowing when doing FFT processing in Pure Data as well as an example of how we can better view the data we get from the FFT objects. There's going to be a bit of maths and theory sprinkled in as well here again but I'm hoping it should just continue to clarify things.

It should also be noted that I fully expect to be making mistakes in all of this, my understanding of some of it is still shaky so if you spot errors or have questions, please ask. I'm still doing this patch-a-day month for my own benefit as well so having people pick me up on things is welcome.



The first thing I'm going to do is go back to the Complex numbers theory but this time to try and explain why we use them in signal processing. I'm going to be pointing to a few more pages on Wikipedia here so that those who want a deeper understanding can go digging. None of this will be very scary if you can manage basic trigonometry, and it's not strictly necessary to understand all of it, but it's probably better to know it than not.

A complex number is just a number with a real and imaginary part, 3 + 2i for example. We can plot these on an [Argand diagram](http://en.wikipedia.org/wiki/Complex_plane) which is really just an XY grid where the X axis is the real numbers (3,2,1,0,-1,-2 etc) and the Y axis is the imaginary numbers (3i, 2i, 1i, 0, -1i -2i, etc). When a complex number is plotted on the diagram we can imagine it as a triangle in the same way that any other XY point would be and we can see that there is a length associated with it as well as an angle.

For example, on the below diagram we have plotted the complex number -3 + 4i.

Simple trig will tell us that the distance between the number and the origin is root (3^2 + 4^2) = 5 and that the angle theta will be sin-1(4/5) roughly equals 53.1. If I now say that by representing a signal as a complex number we can plot it on an Argand diagram, that the length corresponds to the magnitude of that signal and the angle theta corresponds to its phase shift, hopefully you can see why this starts becoming interesting.

At this point I feel I should point out the formula of [Euler](http://en.wikipedia.org/wiki/Euler's_formula) and [de Moivre](http://en.wikipedia.org/wiki/De_Moivre's_formula), which are pretty much the basis of the above link. I don't want to go too deep here (mostly because the maths is only half remembered) but the eventual end point is that a signal can be represented as an exponential function which, when expanded ends up as a series of complex numbers with Sin and Cos terms. I'm hoping that all this has fallen into place somewhat because if you've got it then you pretty much understand all we need to know for this.

Things should get even clearer when I say that what our rfft~ object is actually spitting out are these pairs of Sin and Cos values. This means that we can go back and modify our previous patch and we can get accurate data to show us the magnitude and phase of all our frequency bins.

![FFT Patch correctly displaying Magnitude and Phase data](/a/2010-11-25-patch-a-day-month-day-24-fast-fourier-transform-continued/24-FFTContinued-1.png)

It's worth pointing out quickly that I'm using the atan~ object from the cyclone library to calculate the phase data here because otherwise there's just too much fiddly coding to get what we need. To try and show this all a little better I've modified it further so that the phase of the oscillator can be changed and the range on the graphs is a little clearer.

![Further modified FFT patch to show phase data more clearly](/a/2010-11-25-patch-a-day-month-day-24-fast-fourier-transform-continued/24-FFTContinued-2.png)

The final thing I will talk about tonight is the idea of windowing and the reasons for it. I've already talked about it and used it with the granular synth so this shouldn't have any surprises. If you look at the frequency plot when you have a frequency that should fit exactly in the bins you can see it spilling over into other bins somewhat. This is because when we pull our 64 bits of data out to analyse we are adding other harmonics into it due to the clipping. The example to give here is that of a square wave, which has many more harmonics than a sine wave. Because we may be taking a sample that is midway through a waveform, we are probably clipping that waveform off at a non zero value, which leads to square wave like edges at the start and end of our sample which can add other harmonics in.

To help counteract this we can envelope the samples as we take them in to smooth off these edges.

![FFT Analysis patch with Hanning Window](/a/2010-11-25-patch-a-day-month-day-24-fast-fourier-transform-continued/24-FFTWithHannWindow.png)

The envelope is exactly one cycle of a sin wave, offset by one and this time it fits into 64 samples, our blocksize. The tabreceive~ object reads exactly one block of data out, matching the 64 sample length, and modulates the output of the oscillator with it. Every block that the rfft object now reads will start and end with a zero value.

Unfortunately, this form of amplitude modulation introduces it's own forms of distortion, volume loss and problems with fast transients. The answer to this is to have overlapping windows that are analysed. Unfortunately, this is going to need to be covered tomorrow as I am now tired and sleepy and wish to go to bed.

I've realised that I haven't really done much that I would consider to be in keeping with Patch-a-day today and yesterday so I'm considering extending the month by a couple of days and then doing my learning properly and writing this FFT stuff up as a proper tutorial. I'll let you know, but right now, crash time.
