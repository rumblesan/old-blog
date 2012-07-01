---
date: '2011-10-11 23:45:00'
layout: post
slug: imitation-flattery-and-modular-synths
status: publish
title: Imitation, Flattery and Modular Synths
categories:
- Pure Data
tags:
- algorithmic
- generative
- PDRene
- pure data
- sequencing
comments: true
---

A friend of mine has recently taken the leap into modular synths and I'm just a tad jelous.

Interestingly he's decided to go down the route of getting a [CV interface that connects up to the SPDIF output](http://www.expert-sleepers.co.uk/hardware.html) on his soundcard, prefering to go down the route of sequencing everything from Ableton instead of using hardware sequencers. Certainly I can see the appeal but, unsurprisingly perhaps, I'm most interested in all the intricate, generative stuff you could get done with a large modular system.

I'm still thinking of taking the dive myself and turfing out furniture to make way for an ever growing collection of modules and if I eventually do, top of my list will be the [René from MakeNoise](http://www.makenoisemusic.com/RENE.html). Its an interesting piece of kit that bills itself as a Cartesian Sequencer. Essentially you have a 4 by 4 grid and by sending trigger pulses to it the position will move along the x or y axis. There are various modes and other things it will do but that's pretty much the crux of it. For a pretty excellent example of what you can do with this, Richard Devine [makes some fine noise](http://vimeo.com/17350265) using one as the brains of a reasonably sized setup.

Unfortunately, I've not actually got the hardware, so I'll do the next best thing and build something similar in Pure Data.

My take on things will be a tad different but the core principle is still going to be having an X/Y grid and sequencing points on there in a non linear fashion. I built the beginnings of it over the weekend and the code is on GitHub as always. The project is called [PDRene](https://github.com/rumblesan/PDRene) because I'm unoriginal.

So here's a pretty basic patch that gives us somewhere to start from.

![Basic PDRene patch](/a/2011-10-11-imitation-flattery-and-modular-synths/pdrene_basic.png)

A quick rundown of the four sections.

  * The grid of numboxes have been given send and receive names in the form of $0-x-y-in and $0-x-y-out, where x and y are their coordinates starting from 0. So for example, the num with a value of 6 above is $0-1-2. these all send to receive objects in the gridvals subpatch.

  * The gridvals subpatch just collects the output from the numboxes and prefixes their coordinates onto them. The change objects make sure that new coordinates are only output for the x and y values when they change.

  * The until loop and divide/modulus section on the left is just there to fill the grid with numbers.

  * The two counters on the right are used to step through the grid, changing the x or y values as we need.

Nothing too big or clever, the gridvals patch needs to be improved if we're to expand this to bigger grids but it's a good starting point. The output is designed so that you can have two complimentary sequences running at the same time, one taking the x vals, the other taking the y vals. This is how some of the output from the Rene works and it's a pretty good idea.

The next step I'm taking from this is a way to create long running sequences on this. Instead of doing this by sequencing the values themselves, I've decided to have a go at sequencing pairs of values that modify the current position. So if we pick the sequence :-

$ [1,1], [2,-1], [3,3] $

assume that we start at position $ (0,0) $ and that we wrap values (a value of 4 wraps to 0, a vlaue of -1 wraps to 3) then by adding the modifier values onto our current coordinates we get the following sequence :-

$ (0,0), (1,1), (3,0), (2,3) $

Here's the UI of the sequencer, I'll detail the internals in another post.

![PDRene Diff Sequencer ver 1](/a/2011-10-11-imitation-flattery-and-modular-synths/pdrene_diff_seq.png)

This actually expands on the above idea slightly. There are 4 possible pairs of diff values in a sequence and it's possible to choose how many pairs the sequence runs through before repeating and how many times each of the pairs will be used at each step. So here for example, we have a sequence length of three, the first pair has a length of 2, the next of three and the third of three. The diff sequence output in one iteration would be :-

$ [1,2], [1,2], [-2,3], [-2,3], [-2,3], [3,-2], [3,-2], [3,-2] $

so starting from $ [0,0] $ our positions would be :-

$ (0,0), (1,2), (2,0), (0,3), (2,2), (0,1), (3,3), (2,1), (1,3) $

This seems to be a pretty interesting way to generate patterns but I want to do some more investigating. I'll write up another post that quickly details the insides of this sequencer and then move onto some possible uses for this.

I think I'm going to use this to warm myself up to doing another Patch-a-Day month. It's coming up to a year since the last one and I think it warrants doing again. Better get back into the swing of things

