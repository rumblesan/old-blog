---
date: '2011-11-02 20:24:47'
layout: post
slug: patch-a-day-november-2011-day-2-passthrough-design-pattern-part-2
status: publish
title: 'Patch-a-Day November 2011 Day 2: Passthrough Design Pattern (part 2)'
wordpress_id: '319'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- delay
- design pattern
- FM synthesis
comments: true
---

On to Day 2! Carrying on from where I left off yesterday I've got two example patches that should give you a good idea of how you can use the passthrough pattern in real situations and how you can extend the idea.

In the last post I mentioned that it can be useful when dealing with controllable parameters within a patch. We want to separate the part of the patch that deals with parsing the input control data, and the part of the patch that actually does the processing.

First up, have a look at this abstraction for a delay effect.

![Passthrough delay effect example](/a/2011-11-02-patch-a-day-november-2011-day-2-passthrough-design-pattern-part-2/passthrough-delay-example.png)"

The section in the top centre with the border is the internal of the param abstraction, to the left of them there's the daisy-chained group of them that will parse the mix, time, and feedback parameters. You'll also see that there's a route object routing for delay. If we had a number of effects patches daisy-chained then we'd want to be able to specify parameters in this object and this allows us to do it.

Below that we've got the part of the abstraction that deals with limiting our values between our chosen max and min and also use the line~ object to convert them to audio rate messages. The mix parameter we're actually converting into two separate audio rate signals, one that controls the dry audio volume and the other to control the wet audio volume. These will crossfade between the two giving us good control.

Finally the section on the right is the delay effect itself. It's actually pretty minimal and this is helped by having separated out all the control signal parsing and creation. Instead there are just a handful of send~ objects which makes more much neater code.

It' worth noting that this patch itself adheres to the passthrough design. There is a data bus for all the control data, with anything not routed to the delay being passed onto the next object in the chain, and the audio itself passing through as well. it would be very easy to chain a number of these together and control them with not much effort, which is of course the idea here.

For a more useful example of that, this next patch has a bank of synth voices which can be independently or collectively controlled and use a poly object to share the incoming notes between them. It's a bit scrappy but should illustrate the point well.

![Passthrough synth bank example](/a/2011-11-02-patch-a-day-november-2011-day-2-passthrough-design-pattern-part-2/passthrough-synth-bank.png)"

The top right has the numboxes that set the values for our four controls as well as the ability to send notes to the voices. All the lists sent out through here get prefixed with the synth voice name. The small section to the left of this with the vertical radio bar is the voice chooser. We can choose a specific voice to send control messages to or we can use "all" to collectively change a single parameter on all the voices at the same time.

The far left group of objects uses a poly object to spread any incoming notes amongst the four voices. There are extra objects here that are pretty much just to deal with how poly works, it might be better to use a counter here but it servers well for illustrative purposes and is probably more flexible if you want to do more complex stuff.

Below all of this is the bank of voices and it should be easy to see here how this design pattern results in a lot of flexibility whilst having very neat code.

Here's the insides of the voice abstraction. It's a pretty basic FM synth that should be familiar to anybody who has looked at many of the patches I've made.

![Synth bank voice abstraction](/a/2011-11-02-patch-a-day-november-2011-day-2-passthrough-design-pattern-part-2/passthrough-synth-bank-voice.png)"

Like the delay abstraction the message parsing, control value scaling and DSP sections are split apart. The route object that checks for the synth voice also checks for an "all" element at the start of the list which is how we can modify the parameters for all the voices together.

These two patches should have given you a good indication of how the passthrough design can be used to make concise, neat and logical patches that make problems like dealing with control messages or voice sharing easier.

Here it's been used for both the control parameter parsing and organising the voices. Tomorrows post is going to neaten this synth bank patch up a lot and also show how continued use of the passthrough design can make it easier to make an interactive control interface where the values displayed will change to reflect the voice chosen.



Also I'll point out that all the patches for this Patch-a-Day month will again be going into a Github repository. You can find it all at [https://github.com/rumblesan/PatchaDay-Nov-2011](https://github.com/rumblesan/PatchaDay-Nov-2011)


