---
date: '2010-09-02 21:25:09'
layout: post
slug: a-nintendo-ds-drum-machine
status: publish
title: A Nintendo DS Drum Machine
wordpress_id: '27'
categories:
- NDS Homebrew
tags:
- audio
- NDS
- Programming
- sequencing
comments: true
---

So this isn't a SuperCollider post, as may be obvious from the title, but I don't think I'm going to let this be a solely SC based blog when there's plenty of other noisy stuff I do. About 18 months ago I started playing with writing homebrew software for my Nintendo DS. It was a good chance to improve my coding chops and try and learn a bit about the hows and whys of DSP. In the first instance I succeeded, my C/C++ improved pretty dramatically and it very much helped turn me from a hardware based Electronic Engineer into someone much more comfortable and happy with writing code.

Unfortunately things mostly stalled on the second front after I got my Midi sequencer working and then found other things to pursue. However, I'm now revisiting the whole affair and having a reasonable amount of success.



Part of the reason for making a MIDI sequencer was because I had no idea how to use the built in NDS audio libraries, nor how to read WAV files, nor really at that point much idea about how digital audio worked in anything other than a round about way. So offloading the sound generating bits onto Akai, Novation and Waldorf whilst I just got the DS to spit out the notes in the right order seemed a much better idea. I ended up with a fairly versatile and quite fun touch screen sequencer with multiple tracks, multiple patterns per track, the ability to sequence these patterns and also being able to draw Midi CC curves. The final product got a gig at a night a friend of mine put on, where I ended up playing for four hours due to the inability of some other DJs to show up. Thankfully I found that other people were so interested I could simply ask them to watch my stuff in return for letting them play with the DS.

This is the point where the whole thing collapsed because I wanted a bigger screen for more buttons. I built a version for my[ Always Innovating Touchbook](http://www.alwaysinnovating.com/touchbook/), that was written as a Python GUI controlling a Pure Data sequencer patch over OSC. It also worked rather well but lost some of the magic present in the original and so the whole thing gradually died out. At some point in this time I did learn how to read WAV files in C++ and made a small loader but the momentum was gone and not coming back.

Fast forward approximately a year and I found myself wanting a simple drum machine sampler again. Given my considerably improved coding skills I decided now was the time to finish what I had originally started!! I pulled the Midi parts out of the sequencer to give me a bit less clutter, shoe horned in the wave loader code and then got to work wrangling with [MaxMod](http://maxmod.org/), the homebrewed NDS sound library (which I now find out is a bit of a masterpiece of coding, I feel I should also give props to the whole [devkitPro](http://devkitpro.org/) team for making the toolchains and NDS libraries to do all this). Last Saturday was going to be something of an all nighter in which I hoped to get a proof of concept working and actually have some drum sounds coming out of the little white hand-held.

I had it working by about 10:30 pm...... which is awesome as it's now working, but it didn't make for much of a marathon. I implemented a basic voice assignment and stealing system and tested the whole thing by leaving it running for half an hour to see if it was stable. It carried on churning out its little distorted drum sounds merrily and I knew I was onto a winner.

There are a few more steps that need to be finished before the whole thing is ready and part of the reason for writing this post is to list them to help get me to do them.



	
  * Memory management for tracks. Currently there are no limits, which isn't a good idea.

	
  * Correct reloading of sound files. Tied to memory management really.

	
  * Make it reject Stereo samples. It will only play mono samples and playing stereo samples just makes it sound bad.

	
  * Make changing panning and volume of samples available. I might just have hard left and hard right here to make a 2 channel, mono sampler.

	
  * Saving a tracks samples as a soundbank that can be reloaded easily.

	
  * Saving a tracks samples and patterns as a song.

	
  * Add the Midi sequencer code back in.


The code for the original sequencer is up on my GitHub and once this bit is done it will be there as well. I should probably have done the proper thing and made a branch for this version but I didn't think about it when I did it. Will sort it out soon.

Note: In the time between me writing the first draft of this post and me actually posting it I've crossed the first three items off the list. Turns out they were simpler to implement than I thought. Onwards!!!
