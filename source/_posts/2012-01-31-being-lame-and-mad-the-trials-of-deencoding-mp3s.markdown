---
date: '2012-01-31 22:08:00'
layout: post
slug: being-lame-and-mad-the-trials-of-deencoding-mp3s
status: publish
title: Being LAME and MAD, the trials of de/encoding MP3s
categories:
- C
- Music
- Programming
tags:
- audio
- Programming
- slow radio
comments: true
---

Reteaching myself C has been a pretty good exercise and, for the most part, has been good fun. A little frustrating at times, but there's lots of stuff that's just falling into place and it's generally making me feel much smarter.

This feeling stopped when I started trying to deal with MP3s....

Encoding with libLAME isn't too taxing thankfully. It took me a little bit of getting used to but I'm now happily reading WAV files, stretching samples and then pumping out MP3 files at the end. Encoding, however, is a different matter.

I'm using libMAD and I'm still finding it more than just a bit taxing to understand. I suspect that this is more likely my lack of knowledge than the library itself's fault but to be honest, that just makes it that little bit more annoying.  On the plus side, it really does make me appreciate how easy all these high level scripting languages make things.

Anyway, enough of my whining, As far as SlowRadio is concerned, the project is steadily cruising along and things are looking pretty good. Thanks to some help from Paul I've been able to get a program that mostly recreates his algorithm. I haven't put in any of the onset detection but tbh I'm saving that for a bit later when the other sticky bits are done.

Once I can successfully read in MP3s the next step will be to wrestle with libshout and libcurl so I can go spreading my merry noise across the InterBlag.

Just got to keep moseying along, and keep track of all these buffers right?
