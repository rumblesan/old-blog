---
date: '2010-07-17 16:15:19'
layout: post
slug: simple-sequencing-of-synths
status: publish
title: Simple Sequencing of Synths
categories:
- SuperCollider
tags:
- audio
- lessons
- sequencing
- SuperCollider
comments: true
---

So I've spent a bit of the last couple of days reading "[A Practical Guide to Patterns](http://supercollider.svn.sourceforge.net/viewvc/supercollider/trunk/common/build/Help/Streams-Patterns-Events/A%20Practical%20Guide/PG_01_Introduction.html)" by **H. James Harkins **which is part of the SuperCollider docs and it has really helped me to better understand some of the major ways in which allot of stuff works. Mostly to do with patterns, but also about how synths are actually used within the environment. I definitely recommend it, but don't get worried if you get lost not too far in, it's a bit mind boggling after a while.


First things first, I've modified the previous code example. The simple FM synth now has a basic volume envelope created by multiplying the output signal by a Line UGen which goes from one to zero over a second and a half. This also has a **doneAction: 2** there, which means that once the line has hit zero the synth gets freed up on the server. Secondly, the send(s) has been changed for a store. This is so that when the SynthDef is sent to the server, information about what controls it has are stored in a library of descriptors. The reason for both of these things will become clearer later.

```
(
SynthDef('basic-FM',{

    arg freq1 = 440, amp1 = 30,
    freq2 = 150, amp2 = 0.5;

    var osc1, osc2, output;

    osc1 = {SinOsc.ar(freq1) * amp1};
    osc2 = {SinOsc.ar(freq2 + osc1) * amp2};

    // done action added which
    // frees synth once it is finished
    output = osc2 * Line.ar(1, 0, 1.5, doneAction: 2);

    Out.ar(0,
    Pan2.ar(output, 0)
    )

    // store used instead of send so that
    // synth def is caved into the library
}).store;
)

t = Synth('basic-FM',['freq2', 200, 'amp1', 300]);

t.free;
```

For the moment if you run the code then, after sending the SynthDef across to the server, every time you evaluate the Synth creation line you will hear a single FM pulse which will trail off over a second and a half. If you evaluate t.free before this has finished then the sound will end as expected. If you try and do it once the sound has stopped, however, then the server will throw you back an error. This is because the synth has already freed itself up thanks to the doneAction command of the Line and so it isn't there any more to be freed.

When I was first looking into this, it greatly confused me as to why this might be needed. See, I'm used to thinking of objects in programming as being major chunks of code that won't be created and destroyed all too often (Slightly naive I know but still). You create an object and then you modify its attributes and run its methods and that's what it's there for. To my mind a synth in SuperCollider was something that was going to be created once and then modified to play different notes and sounds. I wasn't really too sure how this worked but that's what I assumed. Thankfully the Guide to Patterns clarified things quite a bit and the upshot is that this isn't quite how things work. In some cases it is, but not all the time, and not in the first example I'm giving.

A brief overview of the Objects involved with Sequencing in SuperCollider is probably quite useful. There are Patterns, Streams and Events (There are also things called Routines, they work a bit like Streams but are slightly different, I'll get to them another day maybe) . Each of these objects plays a different part in basic sequencing. Coincidently, apologies if anybody who knows what they're talking about feels I've got some of this wrong. This is how I currently understand it but please let me know if there are corrections needed.

### Events

Events are essentially just one step in a given sequence. Think of it as one note or chord, played on a synth with a given duration and various other parameters that define what that synth should be doing at this moment in time.

### Streams

A Stream is where the events come from. When a Stream is queried it will send return the next event. Once that's been dealt with, query again and get the next one.

### Patterns

Patterns are inside streams, when you query the stream it will look at the pattern inside and work out what the next event should be. Patterns are linked to specific parameters so a Stream with multiple Patterns for multiple parameters will return an Event with values for multiple parameters.

Basic pattern sequencing of a synth can be summerised like so.

  1. A SynthDef is created, it has some number of arguments and has some form of doneAction

  2. This is sent to the server

  3. The PBind UGen is used to create a stream, one of the arguments for this will need to be an instrument

  4. The PBind also needs to have arguments that are the patterns for each parameter you want to sequence

  5. Once the stream is created, start it playing using the play method

  6. The stream gets queried, returns the first Event, creates a Synth on the server, sets it playing using the parameters in the event and then waits for the length of the specified duration

  7. Once the duration has elapsed the Stream gets queried again and the next event played

  8. The synth should free itself up thanks to the doneAction meaning that the server doesn't run out of resources as more synths get created

The code below is a basic example of this.

```
(
SynthDef('basic-FM',{
    arg freq1 = 440, amp1 = 30,
    freq2 = 150, amp2 = 0.5;

    var osc1, osc2, output;

    osc1 = {SinOsc.ar(freq1) * amp1};
    osc2 = {SinOsc.ar(freq2 + osc1) * amp2};

    // done action added which
    // frees synth once it is finished

    output = osc2 * Line.ar(1, 0, 1.5, doneAction: 2);

    Out.ar(0,
    Pan2.ar(output, 0)
    )

    // store used instead of send so that
    // synth def is caved into the library
}).store;

)

(
b = Pbind('instrument', "basic-FM",
'freq2', Pseq([500, 400, 300, 200], 4),
'dur', 0.5);
)

b.play;
```

Playing this through you should get a pattern of four notes, decreasing in pitch and repeating four times, with an interval of half a second between each. It might be fairly obvious what's happening but lets have a look anyway.

The global variable **b** is used to hold the stream object. The PBind UGen has an instrument argument which tells it to use our basic-FM synth, the freq2 argument is given a Pseq UGen and the dur argument gets a value of 0.5. Clearly the instrument arg is telling the stream what synth to use to play the events and the dur arg sets the duration of these events. The Pseq here is what's making our notes change. This is a pattern that takes a list of values, a number of times to loop through it and also an offset (not used here). When the stream is queried for the first event, assuming no offset the Pseq pattern returns the first member of the list. Once this event is done with, the Stream is queried again and the Pseq gives it the next member. This carries on until the number of loops has run but can be set to keep playing by giving it an inf value.

An important point here is to go back to the change from send(s) to store. The PBind needs to know what parameters a synth actually has available. These are stored in a SynthDescLib unless you're sending your SynthDef to the server with send. If you do this then the server will be able to create Synths but the information about it won't have been entered into the library and so might cause issues with PBind. Using store makes sure that the description is entered into the library and everything works happily. A Quick note, store is actually the description filing version of load(s) and add is the equivalent of send(s).

This is really all there is to basic sequencing, create a stream using PBind and give it arguments specifying the synth, the parameters and the patterns for those parameters then let it run. For more in-depth stuff have a read of the Patterns Guide for some of the ways of nesting, joining and manipulating the myriad of patterns available with SuperCollider. My next piece is probably going to be exploring patterns a bit more as I feel there's allot of ground to cover without getting to far beyond what I can learn.

