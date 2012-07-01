---
date: '2010-11-23 23:23:38'
layout: post
slug: patch-a-day-month-day-23-fast-fourier-transform-introduction
status: publish
title: 'Patch-a-Day Month Day 23: Fast Fourier Transform Introduction'
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

OK, so today's entry is going to get a bit heavy on the maths so due warning for those who might not think they're so hot with it. In truth, I'm having to try and dredge an embarrassing amount of knowledge up from my memory. It feels like a long time since learning about this at uni but it's really not, which just shows what happens if you don't use your knowledge. This post will be mostly writing with not so many pictures.

All this possible pain is worth it, however, as being able to use the Fourier transform opens up the possibilities for lots of things. I'm going to be referencing a lot of other material here as I don't want to be having to go in depth on things that other people have explained better than me. I will start off with a collection of some of the more important terms and then have a small patch to try and help explain. I'll start on interesting patches tomorrow, learning to do first.

So the idea of the Fourier Transform is that we take a section of samples from a signal and break it down into the frequency components that are present. The sections all have to have a number of samples in them equal to a power of two due to how the maths works. In PureData by default the audio signals are calculated in blocks of 64. So we can pass these blocks one after the other into our patch, analyse the frequencies in that audio and then process it.

A few terms that will keep cropping up:-

  1. Nyquist frequency

  2. Block size

  3. Imaginary/complex numbers

  4. Frequency bin

The Nyquist frequency is the maximum frequency that we can analyse. In digital audio, the maximum frequency that you can playback is half of the sampling frequency. Our sample rate is the standard 44.1 KHz, so our Nyquist frequency is 22.05 KHz. For more of an explanation [Wikipedia gives a good run-down](http://en.wikipedia.org/wiki/Nyquist_frequency).

The block size is how many samples we're analysing in one go which, as said is 64 by default. Given our sampling frequency this corresponds to about one and a half milliseconds of audio. We will want to change this later on for reasons that will soon become clear.

Imaginary numbers are not really as scary as some might believe. If you can understand XY co-ordinates on 2D graphs and do simple trigonometry then you can deal with imaginary numbers. These are important in Fourier analyses because a frequency doesn't just have a magnitude, but a phase as well. Imaginary numbers are used to represent a harmonic with a particular volume and phase offset from the other harmonics. Pure Data's FFT objects actually give this info out in the form of sin and cos components. This means that a harmonic can be represented as a sin wave component (real part) and a cos wave component (imaginary part). For more information, start at the [Imaginary Numbers page](http://en.wikipedia.org/wiki/Imaginary_numbers) on Wikipedia and go get lost in maths for an hour or two.

The Frequency bins are what we actually get out when we do a Fourier transform, or more specifically, we get a "list of magnitudes for the real and imaginary components of a number of frequency bins equal to the number of samples we are analysing". The first thing to point out is that if we have a block size of 64 samples, then we get a list of 64 values that give the real magnitudes and 64 that give the imaginary magnitudes. These 64 values actually represent a frequency band because the bins are distributed evenly between 0Hz and the Nyquist frequency. With a block size of 64 samples each frequency bin accounts for a range of about 350 Hz, so by changing the block size we can get a more accurate measurement.

It should be pointed out that harmonics that would fall between the frequency bins will be smeared across multiple bins which makes analysis that much harder. All the more reason to use a bigger block size. Of course it's also worth pointing out two more shortcomings. Firstly, the Fourier transform can only accurately measure frequencies where an entire waveform will fit within the block. With our block size of 64 samples, the lowest frequency we can accurately measure is about 690Hz. If we upped the block size to 512 for example then the lowest frequency goes down to about 90Hz. The problem with just making a bigger block size is that it introduces a delay. We have to wait for all of those samples to come to us before we can analyse them which with a block size of 512 means there will be at least an 11 millisecond delay from the first sample being played to the last sample getting analysed. Maybe not so bad but it's worth bearing in mind.

Parts of the above are a bit of a simplification so far but this should be enough to get up and going. I'm going to create a page for PureData resources to go along with the other pages I have on this site and I'll be pointing out stuff that explains Fourier Transforms better than I do.

So, onto a basic patch, this is purely to show you what sort of an output we get from the FFT objects. Hopefully that will suffice and I've given you enough to mull on until tomorrow.

![Fast Fourier Transform introduction patch](/a/2010-11-23-patch-a-day-month-day-23-fast-fourier-transform-introduction/23-FFTIntro.png)

So here we can feed a signal at a chosen frequency into the FFT object. It can either be a freely chosen frequency, or we can pick a frequency that exactly matches one of the frequency bins. The above picture shows a matching frequency which is why there are the exact values for the frequency bins. There may be some confusion as to why there are actually two peaks/troughs on each graph. This is because the Fourier Transform actually gives out twice as many frequency bins as the number of samples we give it but these are actually mirrored about the Nyquist frequency, meaning the upper half aren't any use to us. The rfft~ object will actually get rid of this data and only calculate the parts we want which results in much less CPU loading.

I recommend building the patch and having a play so you can see how the frequencies get smeared when they're not a perfect harmonic. Like I said, there's very little here in the way of a patch tonight but it's necessary to get the rest of what's happening.

I'll leave it here now. Tomorrow will still be involving a bit of theory but if you've grasped what's here it shouldn't be too hard.
