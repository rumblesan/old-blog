---
date: '2010-11-06 16:34:52'
layout: post
slug: patch-a-day-month-day-6-generative-drum-sequencer
status: publish
title: 'Patch-a-Day Month Day 6: Generative Drum Sequencer'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- drums
- generative
- patch-a-day
- pure data
- sequencing
comments: true
---

Back to some sequencing today, no sounds yet with this, I'll have them tomorrow. This patch is a pretty simple drum sequencer with a bit of randomness in it that should hopefully keep things interesting whilst not being overly complex to modify. One of the things I'm realizing now that I'm trying to do more generative stuff is that randomness is great and all, but it needs to be tempered with a degree of regularity as well, otherwise the results can tend to just be a mess unless you're lucky. Hopefully I'll be able to balance the two nicely as I extend this over the next few weeks.



![Generative Sequencer](/a/2010-11-06-patch-a-day-month-day-6-generative-drum-sequencer/06-GenerativeSequencer.png)

The section at the top is the metro and counter as well as a few other bits so that once the counter hits 32 it resets as well as resetting when the metro is restarted. From here the step number is passed to four different sections. Each section will control a different type of drum sound, Kick, Snare, Open and Closet Hi-Hat and then Clave or Cowbell. The select objects are used to determine which beats the sound should be played, with the hat section (third along) the mod object is used so that the sel object's list doesn't have to be so big.

The BangRand object is a small abstraction I created just to keep things a bit neater.

![Bang Rand Abstraction](/a/2010-11-06-patch-a-day-month-day-6-generative-drum-sequencer/BangRand.png)

All this has is a rand object that feeds a moses object. The argument of the abstraction sets the divide argument of the moses object so that the choice of output is weighted by it. some of the bangs from the select objects will go straight to the sounds, some are fed through this abstraction to create double hits, delayed hits or alternate sounds for the hat section.

Tomorrow I'll add in some drum sounds to this. I've had the patches already made for a little while and will give a quick intro of how they work later, but tomorrow will just be about getting this making some noise.

See you then
