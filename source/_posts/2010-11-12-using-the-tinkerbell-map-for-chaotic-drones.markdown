---
date: '2010-11-12 19:13:40'
layout: post
slug: using-the-tinkerbell-map-for-chaotic-drones
status: publish
title: Using the Tinkerbell Map for Chaotic Drones
wordpress_id: '151'
categories:
- Music
- Pure Data
tags:
- algorithmic
- audio
- chaos theory
- FM synthesis
- generative
- pure data
- synthesis
- Tinkerbell map
---

So today I posted a link to my blog on the [Pure Data forum](http://puredata.hurleur.com/) for the purposes of selfless publicity finding other people interested in what I was doing. The response was pretty awesome by my, reasonably small time blogger, standards so to say thank you to those who are visiting and to hopefully keep them coming back for more, I'm finally writing up a bit more about some of my Chaos Theory patches.

On the [Big List Of Chaotic Maps](http://en.wikipedia.org/wiki/List_of_chaotic_maps) that Wikipedia has, the Tinkerbell Map caught my eye pretty much just because of it's name. It turns out to be pretty easy to implement and use, because its only 2D and the equations are pretty simple.



![A 2D plot of the Tinkerbell Map](/a/2010-11-12-using-the-tinkerbell-map-for-chaotic-drones/TinkerBellMap.gif)"

So the first thing to do was to create an abstraction with the equations in. This was a bit easier and neater than for the Lorenz Attractors mostly because there's less of it but also because the equations themselves don't get too complex. Also note, I'm trying out the [QuickLatex](http://quicklatex.com/) plug-in here for doing my equations, which hopefully looks OK.

$ x_{n+1}=x_n^2-y_n^2+ax_n+by_n $



$ y_{n+1}=2x_ny_n+cx_n+dy_n $

These translate pretty easily into this.

![Tinkerbell Map Equation abstraction](/a/2010-11-12-using-the-tinkerbell-map-for-chaotic-drones/TinkerbellEquations.png)"

All the values can be set as creation arguments to make life easier which means that you just need to send a bang in and you get the numbers out. Also having learnt from the Lorenz Equations abstraction just how untidy these things can get I used sends and receives for the feedback. I also added in a reset inlet that just sets the X and Y values back to their original values.

The final patch itself is also pretty simple to look at because all the complex bits are abstracted into here.

![Tinkerbell's Hymn patch](/a/2010-11-12-using-the-tinkerbell-map-for-chaotic-drones/TinkerbellsHymn.png)"

I've used the simpleFM abstractions again to keep things neat. The output values from the patches get multiplied and then used for the frequency and modulation ratio of the FM voices. In retrospect I think I need to spend a bit more time choosing better ranges for this and I suspect this is where most of the work with this current patch lies but I'm leaving it as something to investigate in future. Each map actually controls two different voices with alternating outputs and the results of these are panned hard left and hard right. The idea is that by giving the two mappings slightly different values, over the time frequencies and timbres of the left and right channel will begin to differ and the stereo field will become wider and more interesting.

The rest of the patch is really just a volume control and recording to a file. The output of this is available on Soundcloud here:-

[http://soundcloud.com/tasteforreality/tinkerbells-hymn](http://soundcloud.com/tasteforreality/tinkerbells-hymn)

[soundcloud][http://soundcloud.com/tasteforreality/tinkerbells-hymn](http://soundcloud.com/tasteforreality/tinkerbells-hymn)[/soundcloud]

The stereo separation happens pretty quickly in this version but I'm guessing that with the correct values this could easily be a piece that takes a long time to evolve if you wanted it to.

The patch can be downloaded from here [Tinkerbell's Hymn Patch](/a/2010-11-12-using-the-tinkerbell-map-for-chaotic-drones/TinkerbellsHymn.zip)

The Patch-a-day patch for today will be a bit late. I'm off for an evening of noise with a friend, hopefully this will keep people amused for the moment.
