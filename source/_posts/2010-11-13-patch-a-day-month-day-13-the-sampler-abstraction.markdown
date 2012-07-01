---
date: '2010-11-13 12:52:10'
layout: post
slug: patch-a-day-month-day-13-the-sampler-abstraction
status: publish
title: 'Patch-a-Day Month Day 13: The Sampler Abstraction'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- Music
- patch-a-day
- pure data
- sampling
comments: true
---

So here it is, a bit earlier than usual because I'm going out tonight so needed to crack this out now. This patch is an abstraction for playback of samples with variable pitch, start and finish offsets and looping. There are still improvements that could be made to it, making use of abstraction arguments for example, but it's at a stage where it's pretty useful.



![Sampler Abstraction](/a/2010-11-13-patch-a-day-month-day-13-the-sampler-abstraction/13-SamplerAbstraction1.png)

So only a couple changes really from the last version. I'm now using more send and receive objects to keep things neat and using the $0 argument to make sure that messages sent stay within the abstraction. Same goes for the array I'm using to keep the sample data in. The start and finish offsets are done in a similar way, just modifying the number of samples that will get played back, but I'm now having the start point saved in an int object and then sent to the line whenever the sample is reset. Currently it's being a bit funny however. The speed of the playback should stay the same for shortened samples but it isn't, I'll need to improve that once I've figured out why.

The looping is now much neater as well. When the sample gets started, as well as the line~ object playing back the samples there is another line feeding an equals object. This equals gets the value of where the line is aiming for so when the sample has finished playback line output equals the final value and the equals sends out a 1. The select picks this up and then sends out a bang. Open the spigot and this bang will get sent to re-trigger the sample. It's nice, easy and neat.

The file loading is a little more complex now. I wanted it to be possible to just send a filename to the abstraction and for it just to load it. To do this I had to build the message for the soundfiler up using list append and prepend objects. The route list object is there because after using the list objects there is a "list" element at the beginning so the route strips this off.

That's really all there is to it, not quite finished but a pretty good start. I'll be using this for stuff in the future most likely so it will get updated as and when. Now, off to a friends birthday for me.
