---
date: '2011-01-03 21:03:02'
layout: post
slug: drones-python-jack-and-windfarms
status: publish
title: Drones, Python, JACK and Windfarms
categories:
- Music
- Pure Data
- Python
tags:
- pure data
comments: true
---

Thanks to a bank holiday today, I was able to swap going to work for other, more productive activities. As well as playing Super Meat Boy and improving my speed runs in Mirror's Edge, I actually sat down to start working out how I can get Radio Drone working. The downside of this was that the only Linux machines I have are my rack mount servers which, while very capable, sound like vacuum cleaners. Thankfully I only needed one of them on but it started grating after an hour or two.

I do have a plan now though.

Thanks to the [PyPD package](http://mccormick.cx/projects/PyPd/) made by Chris McCormick, It's possible to have python start up and control an instance of Pure Data. Combining this with the Python JACK package should mean that I can have a python daemon that will start up separate instances of PD with a chosen patch, dynamically connect these to a streaming system and happily mix between them.

That's the theory at least, in practise I spent much of my time wrangling with installing the correct packages on my Linux box. I think it might be necessary to have a third instance of PureData that does the streaming and mixing but I need to do some more investigation. In any case, it's nice to be off to some sort of start.

I'm also glad that I'll be able to reuse some of the code from my Python Render Farm scripts to make the daemon. really it's just a case of sitting down and designing the infrastructure now.......

In other news, the rhythmic noise EP is taking shape so should be out the door sooner rather than later. I'm also hoping to have a new patch up this week which will be the first of many I hope. I figure that sticking to a weekly patch cycle is enough to keep me thinking but without the slight mental overload that I had in November.
