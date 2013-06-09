---
date: '2010-07-12 21:22:06'
layout: post
slug: fm-synthesis-a-noisey-hello-world
status: publish
title: FM Synthesis, a Noisey Hello World
categories:
- SuperCollider
tags:
- audio
- SuperCollider
comments: true
---

So finally some code, a basic FM synth that turns on to generate screechy noises and doesn't turn off until you tell it to.  This is the beginning part of a grand plan as it happens but I'll explain that later, first, the code. Apologies for lack of syntax highlighting, I'm planning to write or find a Word-press plug-in that will do it for SuperCollider code but until then it will have to look ugly.



    
    (
    SynthDef('basic-FM',{
    
    arg freq1 = 440, amp1 = 30,
    freq2 = 150, amp2 = 0.5;
    
    var osc1, osc2;
    
    osc1 = {SinOsc.ar(freq1) * amp1};
    osc2 = {SinOsc.ar(freq2 + osc1)};
    
    Out.ar(0,
    Pan2.ar(osc2, 0)
    )
    
    }).send(s)
    )
    
    t = Synth('basic-FM',['freq2', 200, 'amp1', 100]);
    
    t.free;


This is extremely simple, but I feel it hits all the bases to be a reasonable piece of starting code. I'm not planning to explain this in great depth as it's all reasonably easy to find in the docs.

We have a SynthDef, to create a new synth. Within the function definition for the synth there are four arguments that have default values and control one of two SinOsc UGens. Two variables are declared and the SinOsc UGen functions are assigned to these with the SinOsc of osc2 having osc1 as a variable of its frequency. The osc2 variable is then stuck in the middle of a Pan2 UGen and fed into the SynthDefs Out UGen. Send it to the server (make sure you do this, I keep forgetting and it's bloody annoying) and we have a synth ready to be used.

The next couple of lines simple create a synth with a few parameters to override the defaults, assign it to the variable t and then get it playing. Finally, free up t once you're sick of the sounds its generating.

All very simple and very dull...... it could really do with a few other bits to make it much more interesting, and this is where the plan takes shape. Inspired somewhat by Adam Jansch's [SuperCollider-a-day](http://www.adamjansch.co.uk/sc-a-day/) blog, I'm intending to take this piece of code and gradually add on to it until I have something useful, or I get bored. I doubt very much I'll be able to do this every day, there are far too many other shiny things to be playing with, but I will update regularly.

The two nebulous aims for the moment will be to add in some envelope functionality to the synth currently and also to learn about sequencing patterns. There will be other bits along the way, and eventually I'll be working on that big Granular Synth I initially wanted, but for the moment the little FM Synth will strike a nice balance between having lots of sonic possibilities and also being simple enough to modify easily.

Until next time

Guy

**EDIT:** I'm attempting to get some sort of SuperCollider specific syntax highlighting going on but its proving slightly tricky. For the moment it at least looks like code, hopefully soon it will have the right colours in the right places.

**FURTHER EDIT:** SUCESS!! it seems that my poking about has gotten it working. It'll be a couple of days before I have it finished and the colours I want sorted out, but a good start I feel.
