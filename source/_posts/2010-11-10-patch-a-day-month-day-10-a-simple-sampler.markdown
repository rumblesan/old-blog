---
date: '2010-11-10 23:54:14'
layout: post
slug: patch-a-day-month-day-10-a-simple-sampler
status: publish
title: 'Patch-a-Day Month Day 10: A Simple Sampler'
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

So I started reading up on the Fourier Transform stuff today, and quickly realised that the knowledge I'd learnt at uni had diminished and I was going to have to do a fair bit more reading than I had anticipated. I also realised that to make most of the FFT patches worth while I'd be needing to analyse external sounds so with that in mind, I'm going to be covering sample playback in PureData. Nothing too taxing to start but I need to be asleep in twenty minutes so hopefully this write up won't take long. As our sample source, I've decided on the most sampled sound in existence, the Amen Break, which will feature throughout these examples, even if it will annoy my most loyal reader.



![Simple Sampler](/a/2010-11-10-patch-a-day-month-day-10-a-simple-sampler/10-SimpleSampler.png)

So fairly simple but very useful, the new object of note here is the soundfiler. This takes a couple of arguments and then loads the chosen file into the chosen array. Here we have the file "amen.wav" and we read it into the array "amen" which is displayed in the graph on the left. Once loaded, the soundfiler outputs how many samples long the file is. We can see that this, roughly seven second, segment of music has 307202 samples in it, which we store in the int object.

To play back the samples from the array we use the tabread4~ controlled by a vline~. We want the tapread4~ input signal to go from 0 to 307201 over a specified time. Given that we know that the sample has a sample-rate of 44100Hz we can work out that 307202 / 44100 = 6.966... seconds, we want the time in milliseconds so we just divide by 44.1 instead to get 6966 milliseconds.  This is used to construct a message that sends the vline~ output signal from 0 to 307202 over 6966 milliseconds and then after a further delay of 6966 milliseconds, goes straight back to 0.

Hit the bang and hear the breaks play.

There's plenty more to do here but I'm tired again so I'll leave it here for tomorrow.
