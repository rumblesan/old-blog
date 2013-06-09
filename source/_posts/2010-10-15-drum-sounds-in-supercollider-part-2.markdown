---
date: '2010-10-15 17:54:06'
layout: post
slug: drum-sounds-in-supercollider-part-2
status: publish
title: Drum Sounds in SuperCollider (part 2)
categories:
- Music
- SuperCollider
tags:
- audio
- drums
- Music
- Programming
- SuperCollider
comments: true
---

So Part two of the Drum Sounds in SuperCollider series, and we're going to be making a snare and a clap. Not necessarily a realistic snare or clap, but reasonable enough to go with the rest of our kit. It will be mostly the same combinations of simple oscillators, noise sources, filters and envelopes as previously but joining them in slightly different ways. Again, the S[ynth Secrets articles](http://www.soundonsound.com/sos/allsynthsecrets.htm) are  great to read for some in depth info and good ideas on this sort of stuff, so I'll link them again.



The snare circuit for the 808 actually functions in a similar way to our full kick drum. There are the same two parts, one a resonant filter based drum sound and the other an enveloped noise source. Obviously the drums are tuned to a higher frequency and the noise is differently filtered to give a better snare effect, but otherwise we could take our full kick, change some of the frequencies we chose and we'd be in the right area.

But reusing the same concepts would be a little boring so I've decided on another route. When a real drum is hit, the actual sound of it is a spectrum of different frequencies, some of which die out very quickly and others that sound for longer. In many ways it could be thought of as a bell, the difference being that with a drum the higher frequencies die out almost straight away and its the much lower register tones that carry on longer. That burst of higher frequencies at the beginning are what's responsible for the attack of the drum sound, which is why our full kick has the brief noise burst.

So what we really want in a drum sound is a brief hit of higher frequencies with the lower frequencies taking longer to decay. And to do it, we're going to use a simple envelope to modify the frequency cutoff of a filter. We need a sound source with a wide frequency content and whilst we could use a noise source for this, choosing a square wave will give us more options for tuning and shaping the sound later. Low Pass Filter sweeping down with a Pulse UGen as the source is the plan.

Again, a Line UGen will work fine as our envelope but this time we need it to control a frequency with a large range, not the volume with a 1 to 0 range. SuperCollider makes everything pretty easy for us in this respect because we can just plug UGens in where we want and use them like we would other variables. Our Low Pass filter wants to know what it's filtering and at what frequency, we want the sweep to start around 1 KHz and decrease to something just above 0 Hz. We just plug our Line UGen in where the LPF frequency argument is, multiply it by 1000 and add 30 to the result. We'll put a volume envelope around this as well which will have a longer decay so that the lower frequencies can carry on a bit. That will also have a doneAction so that the synth frees up after it's played and then we're basically finished. The code for the complete drum sound looks like this.

    
    (
    SynthDef('snaredrum', {
    
    var drumosc, filterenv, drumoutput, volenv;
    
    filterenv = {Line.ar(1, 0, 0.2, doneAction: 0)};
    volenv = {Line.ar(1, 0, 0.6, doneAction: 2)};
    
    drumosc = {Pulse.ar(100)};
    drumoutput = {LPF.ar(drumosc,(filterenv *1000) + 30)};
    
    Out.ar(0,
    Pan2.ar(drumoutput * volenv, 0)
    )
    
    }).send(s);
    )
    
    t = Synth('snaredrum');


Reasonable enough sounding I think for what we need, I've picked the values by ear but change them if you want.

The snare part of the sound is again going to be similar to the high hat, but I'm filtering the noise with a bandpass filter to get the right range for a snare and a low pass filter to differentiate it from the hats a bit more. A relatively simple volume envelope used and then mixing that with the drum sound gives us our finished snare.

    
    (
    SynthDef('snaredrum', {
    
    var drumosc, filterenv, volenv, drumoutput, snaposc, snapenv, fulloutput;
    
    drumosc = {Pulse.ar(100)};
    filterenv = {Line.ar(1, 0, 0.2, doneAction: 0)};
    volenv = {Line.ar(1, 0, 0.6, doneAction: 2)};
    drumoutput = {LPF.ar(drumosc,(filterenv *1000) + 30)};
    
    snaposc = {BPF.ar(HPF.ar(WhiteNoise.ar(1),500),1500)};
    snapenv = {Line.ar(1, 0, 0.2, doneAction: 0)};
    
    fulloutput = (drumoutput * volenv) + (snaposc * snapenv);
    //fulloutput = (drumoutput * volenv);
    
    Out.ar(0,
    Pan2.ar(fulloutput, 0)
    )
    
    }).send(s);
    )
    
    t = Synth('snaredrum');


Finally, it's on to the clap. I'm not so pleased with how this one has turned out, but it shows off what I wanted so I feel that I'll finish this article and then improve it later. A clap sound is much like the snare sound we had earlier but a single clap on it's own can sound a bit drab. When recording claps, it's much better if they can be layered, and better still if there is a slight timing difference between all the claps to help it sound fuller. Roland tackled the problem by having a volume envelope that had multiple peaks in quick succession and then modulated a noise source with this but I couldn't get that to sound quite right. Instead I'm using the Fill functionality of the Mix UGen with an EnvGen to effectively mix multiple single clap sounds with different start offsets.

The EnvGen takes an array of envelope values and another array that has the times required to move between them. If we have the first two values set to zero then we can use a variable for the change time and control the time it takes for the clap to sound. We can create some quite complex envelopes using this but here we will just use it to have an offset before a simple line envelope.

When using the Mix UGens Fill functionality, we give it a number and then a function. It will fill an array of however many elements we specify with the results of the function and then mix that array down into one channel. If we specify an argument within this function, then the Mix will automatically increment it by one every time it goes to fill a new array element. What this means is that we can have the first time value in the EnvGen be multiplied by this arg, and each array element will have a slightly longer start offset than the last. In this way we can mix multiple single clap sounds and give them a degree of time separation. I think they're should be a neater way to do the code but I've not quite gotten to grips with all the syntax. Another thing to learn and update in future i guess.

    
    (
    SynthDef('clap', {
    
    var claposc, clapenv, clapnoise, clapoutput;
    
    clapnoise = {BPF.ar(LPF.ar(WhiteNoise.ar(1),7500),1500)};
    clapenv = {Line.ar(1, 0, 0.6, doneAction: 2)};
    
    clapoutput = {Mix.arFill(7,
    {arg i;
    EnvGen.ar(
    Env.new(
    [0,0,1,0],
    [0.01 * i,0,0.04]
    )
    ) * clapnoise * 0.5
    }
    )};
    
    Out.ar(0,
    Pan2.ar(clapoutput * clapenv, 0)
    )
    
    }).send(s);
    )
    
    t = Synth('clap');


I've chosen different frequencies for filtering the noise source again to make it sound different from the other noise used in the rest of the kit. I still think the clap sound needs to most work but it gave me a chance to show how the Mix Fill and EnvGen can be used together so it's OK for now.

So that finishes our basic set of drum sounds for the moment. The next step is going to be integrating Pure Data and SuperCollider over OSC so that we can have one control the other and actually make some music. I'll need to do a bit of investigation on the best way to make that happen
