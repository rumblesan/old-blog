---
date: '2010-10-12 16:03:53'
layout: post
slug: drum-sounds-in-supercollider-part-1
status: publish
title: Drum Sounds in SuperCollider (Part 1)
categories:
- Music
- SuperCollider
tags:
- drums
- Music
- Programming
- SuperCollider
- synthesis
comments: true
---

I feel it's about time I tried to build something useful in SuperCollider since up until now I've mostly just been making examples. Synthesising drum sounds seems like a good place to start and it will also give me something to use when showing how to get Pure Data and SuperCollider interacting over OSC. The focus will be on making the sounds and not so much on how to control them so it will just be single synth instances that make a noise when they're created and then free themselves. This is going to be a two part post again with the Kick and Hat sounds covered here as a starter, and the Clap and Snare sounds covered in a later post since they were marginally more complex and it wouldn't hurt to have a few basics first.

I'll be sticking to the basic and obvious electronic drum sounds for the most part. It isn't pushing any boundaries for new and innovative methods but I'm more interested in learning the necessary skills to get SuperCollider to do what I want. I plan to create these now and then revise them gradually later down the line so with that in mind, I'll be creating 808 and 909 style sounds where the main focus will be on a kick, a snare, open and closed hi hats and a clap, probably with a couple of other bits thrown in for good measure. These won't be accurate reproductions of Roland's drum sounds, just taking some basic techniques for analogue synthesis and applying them to SuperCollider. Some of the info here has come from the Sound on Sound synth secrets articles which are a really amazing source of knowledge and deserve a good read.

So, first up we have the kick, which has two parts to it that are both very similar. The obvious bass section of the sound as well as the percussive click at the beginning. We will generate the drum sound and the initial click separately using a sine oscillator and a noise source respectively which are each modified by separate envelope generators. This is a fairly simplistic way of synthesising drum sounds but this serves well enough to be useful.
The bass portion of the sound will be handled by a SinOsc tuned to 60 Hertz. Obviously we need to shape this so that it dies out relatively quickly and a Line UGen will serve as a volume envelope. The Line has a doneAction so that once the envelope has finished the synth will free itself and we can trigger it again if needed. The below code shows how all of this fits together. It's quite verbose but should be easily understandable, Oscillator multiplied by Volume envelope.

```
(
SynthDef('kickdrum', {

    var osc, env, output;

    osc = {SinOsc.ar(60)};
    env = {Line.ar(1, 0, 1, doneAction: 2)};

    output = osc * env;

    Out.ar(0,
        Pan2.ar(output, 0)
    )

}).send(s);
)

t = Synth('kickdrum');
```

Adding the click at the beginning involves basically the same process but with a noise source. We'll put a Noise UGen through a Low Pass Filter UGen to make it sound more like a thump and then use a second Line UGen with a much quicker decay. It's important to note that there isn't a doneAction here, we don't want the synth to free itself up before the bass envelope has finished otherwise the sound will be clipped off. If in future we have variable length envelopes involved here then we're going to need to change how this works but it will do for the moment.
We combine both of these and the end result is a reasonable bass drum sound that while not great, works well and can easily be improved later.

```
    (
        SynthDef('fullkickdrum', {

        var subosc, subenv, suboutput, clickosc, clickenv, clickoutput;

        subosc = {SinOsc.ar(60)};
        subenv = {Line.ar(1, 0, 1, doneAction: 2)};

        clickosc = {LPF.ar(WhiteNoise.ar(1),1500)};
        clickenv = {Line.ar(1, 0, 0.02)};

        suboutput = (subosc * subenv);
        clickoutput = (clickosc * clickenv);

        Out.ar(0,
            Pan2.ar(suboutput + clickoutput, 0)
        )

    }).send(s);
    )

    t = Synth('fullkickdrum');
```


With that done it's on to the Hi Hats. This works much the same as the click sound from the bass drum but we have a slightly different volume envelope decays and different filtering on the noise. The difference between an open and a closed hat here will just be the length of the decay, everything else remains the same for each. Again the Noise UGen is low pass filtered but this time we let more of the higher frequencies through. We also filter it through a High Pass Filter UGen after that so that we get less thump and more of a mid range emphasis. I've chosen some values that I feel are fine here but there's plenty of scope for tuning. We could probably just use a single Band Pass Filter but I feel this gives a degree more control over the sound. The volume envelope is again created using a Line UGen, with the open hat having a longer decay than the closed hat. I've created the two as separate synths here but they could easily be combined into a single one with controls.

```
(
SynthDef('openhat', {

    var hatosc, hatenv, hatnoise, hatoutput;

    hatnoise = {LPF.ar(WhiteNoise.ar(1),6000)};

    hatosc = {HPF.ar(hatnoise,2000)};
    hatenv = {Line.ar(1, 0, 0.3)};

    hatoutput = (hatosc * hatenv);

    Out.ar(0,
    Pan2.ar(hatoutput, 0)
    )

}).send(s);

SynthDef('closedhat', {

    var hatosc, hatenv, hatnoise, hatoutput;

    hatnoise = {LPF.ar(WhiteNoise.ar(1),6000)};

    hatosc = {HPF.ar(hatnoise,2000)};
    hatenv = {Line.ar(1, 0, 0.1)};

    hatoutput = (hatosc * hatenv);

    Out.ar(0,
    Pan2.ar(hatoutput, 0)
    )

}).send(s);
)

o = Synth('openhat');
c = Synth('closedhat');
```

So that's it for this part like I said, the next part will be the Clap and the Snare sounds at which point we'll have most of the stuff we need for a basic drum kit. This will be an ongoing thing, gradually having more sounds added and existing ones improved so it should become a genuinely useful piece of code. Part 2 coming soon

