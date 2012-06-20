---
date: '2010-09-29 10:58:02'
layout: post
slug: nodes-graphs-groups-and-positioning-part-2
status: publish
title: Nodes, Graphs, Groups and Positioning (part 2)
wordpress_id: '76'
categories:
- Programming
- SuperCollider
tags:
- audio
- lessons
- Programming
- SuperCollider
comments: true
---

So here is part two of the series on Nodes, Graphs, Groups and Positioning which will have a bit more code than the last one but shouldn't be much trickier to follow. I'll specifically be dealing with Positioning here, and how some Nodes need to come after other Nodes to get the results you want.

We'll start off with the Simple-FM synth that I've used previously, it's very uninteresting but will be good for explaining what we're doing.

    
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
    
    t = Synth('basic-FM',['freq2', 200, 'amp1', 100]);
    
    )


It's fairly dissonant because we're going to be putting this through a Low Pass filter and I want it to be obvious when the sound is changing.

Our Low Pass filter code looks like this:-

    
    (
    
    SynthDef('LPFilter',{
    
    arg freq = 1000, inBus, outBus = 0;
    var filter;
    
    filter = {LPF.ar(In.ar(inBus), freq)};
    
    Out.ar(outBus,
    Pan2.ar(filter, 0)
    )
    })
    
    )


There isn't really much to it, we have a Low Pass filter UGen around an In UGen so it will filter whatever comes in through the audio bus with the cutoff frequency set by the freq variable. Lets put it all together to start things working. We need to modify the FM synth to send its output to an audio bus so we can pipe it into the filter but otherwise not much changes.

    
    (
    SynthDef('basic-FM',{
    
    arg freq1 = 440, amp1 = 30,
    freq2 = 150, amp2 = 0.5,
    outBus = 0;
    
    var osc1, osc2;
    
    osc1 = {SinOsc.ar(freq1) * amp1};
    osc2 = {SinOsc.ar(freq2 + osc1)};
    
    Out.ar(outBus,
    Pan2.ar(osc2, 0)
    )
    
    }).send(s)
    
    SynthDef('LPFilter',{
    
    arg freq = 1000, inBus, outBus = 0;
    var filter;
    
    filter = {LPF.ar(In.ar(inBus), freq)};
    
    Out.ar(outBus,
    Pan2.ar(filter, 0)
    )
    }).send(s)
    
    )
    
    d = Bus.audio(s, 1);
    t = Synth('basic-FM',['freq2', 200, 'amp1', 100, 'outBus' d]);
    f = Synth('LPFilter',['freq', 1000, 'inBus', d]);
    
    f.set('freq', 300);


........ if you run and you don't hear anything, don't worry, you shouldn't be.  Let's go through what's happening here. We have two Nodes, the basic-FM synth and the LPFilter, and the references to these Nodes are stored in the **t** and **f** variables. Both of these Nodes are in the Global Group because we haven't told the server to put them anywhere else. We would probably expect that, as we create the filter node after the synth node, everything would be peachy but clearly it's not quite that simple.

When we create a new synth, there are a few arguments that we miss out, so they take their default values. One of these is called the _addAction_ and we can use it to specify the position in the group that new Nodes take in relation to other Nodes. The default for this is _addToHead_, so despite us creating the nodes in the order we want, because the Filter Node is created after the synth Node, it will be added to the head of the group it's in.

There are a couple of ways we can fix this. Obviously we can change the addAction and I'll get to this in a moment.

A simple solution would be to reverse the order that the nodes are created in, and if you try it out you'll hear that it works. Have a play with changing the frequency of the filter as well once its working.

We can also manually change the ordering of the nodes. After running the above code with the synth first, use

    
    t.moveBefore(f);


or

    
    f.moveAfter(t);


to reorder the nodes. There are a number of messages for node reordering. Have a scour through the docs for more on this.

In the long run, the addActions seem to be the best way to create and keep the order of nodes once we start getting complex. The syntax doesn't really add much into what we have and it means that we can easily set the order of lots of Nodes with relation to each other. The full list of arguments for the Synth.new method are:-

**Synth.new(defName, args, target, addAction)**

Where target is a synth or server and add action specifies what we want to do. In this case, we can update the section of code where we create our synths and the audio bus and enclose the whole lot in brackets so we can create it in one go and have the addAction correctly specify the ordering.

    
    (
    d = Bus.audio(s, 1);
    t = Synth('basic-FM',['freq2', 200, 'amp1', 100, 'outBus', d]);
    f = Synth('LPFilter',['freq', 10000, 'inBus', d], t, 'addAfter');
    )


The addAction for the filter synth tells it to position it after node t which means our signal chain is in the correct order and we get sound.

For more info on this, the place to check out is the documentation on [Order of Execution](http://supercollider.svn.sourceforge.net/viewvc/supercollider/trunk/common/build/Help/ServerArchitecture/Order-of-execution.html). It gives more examples and expands on the add actions and some of the other things I've shown. The next and possibly final instalment of this series of posts will be about direct Node messaging where we do away with the niceties that the SuperCollider language functions give us and just send direct OSC to Nodes.

Keep playing
