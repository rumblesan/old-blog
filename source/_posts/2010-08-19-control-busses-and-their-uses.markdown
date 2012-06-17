---
date: '2010-08-19 20:43:14'
layout: post
slug: control-busses-and-their-uses
status: publish
title: Control Busses and their uses
wordpress_id: '23'
categories:
- SuperCollider
tags:
- aliasing
- busses
- FM synthesis
- lessons
- SuperCollider
---

So I'm finally writing this up! The code has been sitting around for about a week now and other stuff has just kept getting in the way. But here it is, finally.

So the first thing I should point out is my new found liking for the SuperCollider documentation. Whilst the parts that fly about on the internet are a bit hassle-some to sift through and can make it difficult to find the answer to the questions you want, the help functionality and documentation within the actual program is really great and very nicely laid out. Many of my questions are now being answered there. And don't I feel like a muppet for doubting it to begin with.

Anyway, onto the code.



Nothing especially complex, a couple of synth defs and then modifying some parameters.

    
    (
    SynthDef('test-Mod',{
    
    arg freq1, amp1, modBus;
    
    var output;
    
    output = {SinOsc.ar(freq1 + In.ar(modBus)) * amp1};
    
    Out.ar(0,
    Pan2.ar(output, 0)
    )
    
    }).store;
    
    SynthDef('Simple-LFO',{
    
    arg freq1, amp1, outBus;
    
    var output;
    
    output = {SinOsc.ar(freq1) * amp1};
    
    Out.ar(outBus,
    output
    )
    
    }).store;
    )
    
    c = Synth('test-Mod',['freq1', 500, 'amp1', 0.5, 'modBus', 3]);
    
    b = Synth('Simple-LFO',['freq1', 200, 'amp1', 100, 'outBus', 3]);
    
    b.set('amp1', 0);
    b.set('amp1', 30);
    b.set('freq1', 1257, 'amp1', 1000);
    b.set('amp1',500);
    b.set('freq1',100);
    
    b.free;
    c.free;
    


The obvious thing to notice is that we're using In.ar(modBus) in the frequency definition of the first synth's SinOsc. This means that the signal coming in through that audio rate bus gets added to the value of the freq1 variable and then the SinOsc spits out what it's told. The second synth is just a simple SinOsc but the bus that its audio is coming out from can be set when we create it. I'm sure the trick here is pretty obvious, when we create the synths we tell the test-Mod that its input modBus is audio bus 3 and we tell the Simple-LFO synth that its output bus is number 3 as well. The output from Simple-LFO will then modulate the frequency of test-Mod.  Quick note, bus 3 was chosen at random, it just needs to be greater than 1, or whatever the last audio output on your system is.

When test-Mod is initially created we get a sine wave at 500Hz, but as soon as Simple-LFO is created we can hear it being modulated and a more dissonant sound is there. The commands after that will either set different amplitudes for the lfo creating differing amounts of modulation or change the lfo frequency resulting in different timbres.

This is a pretty simple way of doing things, it should be noted that there is actually some important stuff I'm missing out, namely the ordering of nodes on the server, but for the moment we won't worry about it. (Also I don't yet understand it, that's probably tackled next.)

Right, next step up. Clearly we can define what buses we want to use manually, but if we're doing it allot then it could become messy to keep track of, thankfully SuperCollider has useful functionality for automating this.

    
    (
    SynthDef('test-Mod',{
    
    	arg freq1, amp1, modBus;
    
    	var output;
    
    	output = {SinOsc.ar(freq1 + In.ar(modBus)) * amp1};
    
    	Out.ar(0,
    		Pan2.ar(output, 0)
    	)
    
    }).store;
    
    SynthDef('Simple-LFO',{
    
    	arg freq1, amp1, outBus;
    
    	var output;
    
    	output = {SinOsc.ar(freq1) * amp1};
    
    	Out.ar(outBus,
    		output
    	)
    
    }).store;
    )
    
    d = Bus.audio(s, 1);
    
    c = Synth('test-Mod',['freq1', 500, 'amp1', 0.5, 'modBus', d]);
    
    b = Synth('Simple-LFO',['freq1', 200, 'amp1', 100, 'outBus', d]);
    
    b.set('amp1', 0);
    b.set('amp1', 30);
    b.set('freq1', 1257, 'amp1', 1000);
    b.set('amp1',500);
    b.set('freq1',100);
    
    b.free;
    c.free;
    d.free;
    


This time very little has really changed, just the addition of variable d and the Bus.audio method. All that happens here is a one channel audio bus is created on the default server. This then gets passed to the synth constructors instead of us stating we're using audio bus 3. SuperCollider will keep track of what buses are in use and which have been freed up and assign what it needs to. We just have to make sure we don't hit the limit of how many buses we're allowed. Simple eh?

The commands are all the same as are the sounds, we just have one less thing to worry about.

The final example will show both, how to assign control buses to synth parameters without having to pass them as arguments, as well as where the limits of control rate buses lie.

This time the code has all changed a little bit.

    
    (
    SynthDef('test-Mod',{
    
    	arg freq1, amp1;
    
    	var output;
    
    	output = {SinOsc.ar(freq1) * amp1};
    
    	Out.ar(0,
    		Pan2.ar(output, 0)
    	)
    
    }).store;
    
    SynthDef('Simple-LFO',{
    
    	arg freq1, amp1, outBus;
    
    	var output;
    
    	output = {SinOsc.ar(freq1) * amp1};
    
    	Out.kr(outBus,
    		output
    	)
    
    }).store;
    )
    
    d = Bus.control(s, 1);
    d.set(700);
    
    c = Synth('test-Mod',['freq1', 500, 'amp1', 0.5]);
    
    c.map('freq1', d);
    d.set(600);
    d.set(300);
    
    b = Synth('Simple-LFO',['freq1', 200, 'amp1', 100, 'outBus', d]);
    
    b.set('freq1', 1257, 'amp1', 1000);
    
    b.free;
    c.free;
    d.free;
    


The first major thing is that the test-Mod synth def now no longer has an argument for the mod-bus. The reason for this is because we can use the map method of a synth object. In this case we map bus d to the freq1 argument of the test-mod synth. Once we've done this we can use the set method of the bus to change the synth's frequency.

If we carry on and create the Simple-LFO synth and tell that to send its output down bus d then we get the FM synthesis again......

But it's not quite the same this time....

The signal is distorted and doesn't sound like the clean FM tones we have gotten in the previous examples. That's because if you look, the bus is actually a control rate bus and not an audio rate. This means that because of the way that control rate signals are calculated within SuperCollider, we are going to get aliasing distortion. Control rate signals are evaluated once per signal block, the default of which is every 64 samples, so we now no longer get the smooth FM synthesis. To map a bus to a synth control the bus needs to be at control rate, (Or at least that's how it appears to me, I'm still learning this) so for slow moving stuff its fine, but for any high frequency changes, unless you want distortion, it's not what you;re after.

Anyway, hopefully that's all been useful, I'm going to start digging into node ordering and stuff in the next few days so the next blog post will likely be about that, once that's done I've decided that I know enough to start going after that granular synth patch I want.

Hooray!!
