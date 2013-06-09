---
date: '2010-10-05 21:41:22'
layout: post
slug: sequencing-basic-events-in-pure-data
status: publish
title: Sequencing Basic Events in Pure Data
categories:
- Music
- Pure Data
tags:
- algorithmic
- generative
- Programming
- pure data
- sequencing
comments: true
---

So one of the things I've been thinking about recently is how to sequence complex musical structures but without everything sounding like a mess. Markov chains can help with this to some extent by making the output a bit more ordered but they can become unwieldy if you're trying to deal with many states and weighting them by hand.
The solution I'd like to try is to have multiple, higher order Markov chains with a smaller number of states which won't sequence single events, but groups of events.



In this case a single event would be a note or a drum sound, whereas the group could be a chord, a drum fill or a tune. For my purposes, I'm going to concentrate on drum patterns and our group of events is going to be a sequence of hits that could be anything from a single hit up to a full bar of sequenced drums. This system is going to involve two things, the first will involve showing how we can sequence events simply in Pure Data, the second will be the addition of the second order Markov chain from previously so we can use that to control everything.

To do our sequencing I've decided to use the pipe object in PD in combination with a list held in a message box. The message takes the form of event and delay time pairs. The pipe object is used to delay any message passed into the left inlet by a number of milliseconds specified, either as an object creation argument, or a float passed into the right inlet. In our case, the event/delay pairs go through an unpack object so the event goes in through the left and the delay value in the right. This patch is a very simple example.

![Basic1](/a/2010-10-05-sequencing-basic-events-in-pure-data/Basic1.png)

I chose to modify this slightly more so that within a group events are scheduled with respect to the previous events. Have a look at the following patch.

![Basic2](/a/2010-10-05-sequencing-basic-events-in-pure-data/Basic2.png)

As an event/delay pair is unpacked, the delay value gets added to the previous delay value. in our example patch, the list is "1 0, 2 100, 3 100" meaning the 1 will fire through straight away, the 2 will be delayed 100ms and the 3 will be delayed 100ms after the 2. The pipe just thinks of it as being delayed by 200ms in total. I decided to do this because I feel it makes more sense to me to create everything relative to each other, maybe you feel the opposite so change as needed. It certainly makes the patch a little more complex and requires more design decisions in future so it might be worth it.

I'm going to edit this patch a little more to add in multiple event groups and make sure things run correctly. The two main problems with the current system are that the delay needs to be reset to zero at the beginning of each group, and we need to have a way of signalling that the group has finished. The first is important, the second we can work around in a couple of ways. To start, here is the patch with multiple groups.

![ThreeGroups](/a/2010-10-05-sequencing-basic-events-in-pure-data/ThreeGroups.png)

The three message boxes at the top can be used for selecting either group 0, 1 or 2. The float from these is passed to a trigger object which sends out a bang to reset the delay, then sends the float out to a route object which bangs the relevant group. the event/delay messages then pass through the system in the usual way. Simple.

To signal when the group finishes I cheated a little bit, basically by just not bothering. Here I've joined the second order Markov chain to the event sequencer.

![MarkovControlled](/a/2010-10-05-sequencing-basic-events-in-pure-data/MarkovControlled.png)

The metro on the Markov chain is set to 300ms and since none of our audio events are longer than that, there isn't really a need to say when we've finished. In fact we don't really have to keep all the event groups under 300ms, the pipe object can deal with them overlapping but we'll keep things simple for the moment. A further modification to this could be to have a specific event number that would be a re-trigger for the Markov chain. In this way we could set it going ourselves, and then once an event has finished, it would cause the Markov chain to move to the next state. This would mean that the timing of the state changes would not have to be regular, possibly leading to some interesting results. I might come back to this at a later date once we have some sound being generated.

So one final change I'll make is being able to change the tempo and keep everything relatively in time. In this case all we do is replace the delay values in the event group messages with fractional float values. We then have a number box which sends its value both to the delay and (via send/receive objects) to a multiply object. The fractional values coming out of the unpack will get multiplied by this and then get sent to the pipe.

![TempoRelative](/a/2010-10-05-sequencing-basic-events-in-pure-data/TempoRelative.png)

This won't change the delay given to events already in the pipe, but otherwise everything will keep in time after it's settled. It's also worth noting that if people have access to Max MSP then you can use the nice timing system within to do this more neatly. I might port this patch over as well just to show some of the extra useful things Max gives. All of these patches can be found in [this zip file](/a/2010-10-05-sequencing-basic-events-in-pure-data/Event-Sequencing.zip) for those who want to play around.

I'm planning on going back to SuperCollider for the next tutorial and I'll be using that to build some drum sounds with the intention of then doing a further post on how to get PureData controlling SuperCollider over OSC. It's going to be a bit of learning for me so I'll aim for the end of the week. There's also a plan to create a single page with links to other useful Algorithmic and Generative composition stuff, as well as general PureData and SuperCollider information. I'll try to get that started sooner and it will just update as and when.

All the best
