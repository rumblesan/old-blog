---
date: '2010-11-29 22:31:22'
layout: post
slug: patch-a-day-month-day-29-a-nice-cup-of-drone
status: publish
title: 'Patch-a-Day Month Day 29: A Nice Cup of Drone'
wordpress_id: '232'
categories:
- Live-Coding
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- drone
- FM synthesis
- generative
- livecoding
- patch-a-day
- pure data
- synthesis
---

I continue to wrestle somewhat with the Mandlebrot set but I don't really feel I'm closer to getting anything useful done with it. As I couldn't think of anything else of great use to do tonight I had another live coding practise, this time aiming for some interesting drone scapes, which I reckon I managed pretty well. I'm not really sure how much explanation I can give this tonight so I'll talk a little bit about it and then give you the patch to play with.



![A drone patch done as live coding practise](/a/2010-11-29-patch-a-day-month-day-29-a-nice-cup-of-drone/29-EveningDrone.png)"

Much of this is pretty rough and ready, and it's very clear in the audio that it was clipping in lots of places. The part that helps to keep this all ticking over is the multiple sample and hold sections at the top. A single bang gets slightly delayed a few times to trigger snapshots off the same noise source. The results of this get multiplied and increased to fit into reasonable ranges and then fed to lines. The metro will cause this to trigger every four seconds and help keep things moving.

The squarevoice abstraction is simply a rough and ready square wave patch with a control to change the duty cycle of the wave.

![A squarewave voice abstraction](/a/2010-11-29-patch-a-day-month-day-29-a-nice-cup-of-drone/29-SquareVoice.png)"

I also put a volume control inside to make things a little easier.

I've literally just taken a few of these and connected them together so that they intermodulate one another. There are a couple of controls for changing the frequency of some of them or the frequency of other oscillators that modulate them. I also put in two delay lines that feed signals that modulate other sections. I actually found that when i started switching parts off by setting frequencies to zero, the delay lines kept making things happen. Listen to the last minute or so of the audio to see what I mean.

Sound sample can be found here if the player doesn't work.

[http://soundcloud.com/tasteforreality/cluster](http://soundcloud.com/tasteforreality/cluster)

[soundcloud][http://soundcloud.com/tasteforreality/cluster](http://soundcloud.com/tasteforreality/cluster)[/soundcloud]

And the patch is available for those that want it.

[Chaotic Drones patch](/a/2010-11-29-patch-a-day-month-day-29-a-nice-cup-of-drone/29-ChaoticTones.zip)
