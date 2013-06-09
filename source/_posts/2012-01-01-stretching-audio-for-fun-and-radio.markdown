---
date: '2012-01-01 21:57:44'
layout: post
slug: stretching-audio-for-fun-and-radio
status: publish
title: Stretching Audio for Fun and Radio
categories:
- C
- Music
- Programming
tags:
- audio stretching
- DSP
- FFT
- radio
comments: true
---

Over the past two weeks, whilst taking some much needed time off from work, as well as enjoying the festive seasonal cheer I spent some time brushing up on my C skills. Part of the reason for this is because I'm embarking on a long running project involving pic chips, modular synths and actual hardware will need to get back to some good old fashioned embedded C. My other plan was to start on an idea I've had for a while and decided since it would involve quite a bit of DSP, I'd do it in C and use it as a learning exercise.

By now most people should have heard the [Justin Bieber 800% slower](http://www.youtube.com/watch?v=QspuCt1FM9M) "remix" that flew around the internet a little over a year ago. It uses [Paul's Extreme Sound Stretch](http://hypermammut.sourceforge.net/paulstretch/) to slow the song down without affecting the pitch, turning a fairly trite pop song into a truly amazing slab of monolithic, ambient noise. Essentially the program just takes many overlapping windows of audio, calculates the frequency spectrum using an FFT, randomizes the phase value for each frequency bin and then does the inverse FFT. There's a little bit more magic to it than that, but that's essentially it.

I've decided to create a radio station, much like PatchWerk Radio, that will download CC licensed audio from the internet at large, stretch the songs, and then stream them back out. To help matters along, Paul's Stretch is [open source software](https://github.com/paulnasca/paulstretch_cpp) so I've been able to dig into the internals and find out how it all fits together. At the moment the code is up on github and can be used to stretch audio and write it out to a new file. It doesn't sound quite as good as Paul's version because there's a bit more DSP voodoo in his that I haven't yet implemented but I'll be getting on with that in the next couple of days.

Once I have that sounding good, the next step will be to get on with the audio finding and downloading, then interfacing it with shoutcast/oggcast. Given how quickly I've managed to hammer everything out so far I don't think it's too far off.
