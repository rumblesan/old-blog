---
date: '2010-09-21 15:59:49'
layout: post
slug: a-basic-intro-to-markov-chains
status: publish
title: A Basic Intro to Markov Chains
wordpress_id: '77'
categories:
- Programming
- Pure Data
tags:
- audio
- generative
- lessons
- Programming
- pure data
- sequencing
comments: true
---

So I said I'd get a post on this sorted and here it is. Nothing too taxing, just a basic intro to creating Markov Chains in pure data. I'll post something another day about some interesting ways they can be used but the intrepid programmer and composer can probably work some of that out themselves.



So, I feel that a good place to start this is by explaining what a Finite State Machine is, since a Markov Chain is basically a variation on this. I'll pull a picture from the [wiki ](http://view.eecs.berkeley.edu/wiki/Main_Page)of the [Electrical Engineering and Computer Sciences](http://www.eecs.berkeley.edu/) College at UC Berkley.

![Finite State Machine](http://view.eecs.berkeley.edu/wiki/Finite_State_Machines)

This may well look similar to the diagram of a Graph that I showed in the post on Nodes and Graphs previously. What we have here is a number of states that a system can occupy. The system can move between these states but can only move from one specific state to a number of other specific states. The diagram here has all these state transitions as single direction changes but there's no reason why that has to be the case. The important thing to understand here is that the system can move between these states but only to certain states.


It might be a little obvious but at this point I want to point out that a state can be anything as far as we're concerned. Musically we can have each state represent a note, or a drum sound, and when the system moves into that state the corresponding sound is played. There's plenty of scope for taking it farther than that when you think about it however.

So, we have various different states and our system can transition between them. What a Markov Chain does with this is that we assign the transition from each state to another with a weight, and then the system randomly decides which state to transition to based upon the weighting. As an example, I have drawn a fairly rubbish diagram complete with numbers!!



![Markov Chain Example](/a/2010-09-21-a-basic-intro-to-markov-chains/FSM-Chain-Example.png)

So here we have states A, B and C and the transitions from each state along with the weightings are shown. As an example, the transition from state A to state B has a weighting of 40, state A to state C is 10 and state A back to itself is 50. Values all add up to 100 so it should be pretty easy to work out percentage chances here. It should also be obvious that the chance of moving from state A to state B is not the same as moving in the other direction.

So, hopefully everything so far has been clear, I think it's time to move on to some programming now. I've chosen to do these patches in Pure Data for a couple of reasons, namely, it's free and I feel the graphical layout lends itself well to explaining concepts like this. For anybody who hasn't used Pure Data before, plenty of info can be found at [the main website](http://puredata.info/), but for some really clear help and tutorials, I recommend the [Floss Manuals Pages](http://en.flossmanuals.net/PureData) which are really worth reading. You should still be able to get a good idea of what's going on here anyway. The way I've designed the following patches is not the most elegant or efficient, but it should server to explain things in the clearest manner. First up, the three state Markov Chain above.

![1stOrder](/a/2010-09-21-a-basic-intro-to-markov-chains/1stOrder.png)

The metro at the top left puts out a bang every 750 milliseconds that makes the random object send out a random number between 0 and 99. The weightings for each state now are held in the three message objects marked as the "State Change Probabilities" and depending on what the current state is, the message for a specific state will get a bang and send its list to the unpack object. For our use here, the three states are **0**, **1** and **2,** just because that makes it easier in Pure Data but I'll keep talking about A, B and C.


The bundle of maths in the bottom left is a big perplexing at first but fairly simple in what it does. The value for the state A transition is subtracted from the random value, if we have a remainder of zero or less then we transition to state A. If we have a positive remainder then we subtract the state B transition value, a value less than 1 means we transition to state B, otherwise we transition to state C. Once the new state has been chosen, this information gets sent back to the top so that the new probabilities for the state are used when deciding transitions. The patches used in this post can be found in a zip archive [here](/a/2010-09-21-a-basic-intro-to-markov-chains/Markov-Chains.zip), have a play around and see how it all works.

Now some might have noticed that the patch is referred to as a **First Order** Markov Chain and might then be wondering what this means. In short, the order of a Markov Chain is how many previous states it takes into account. A first order chain will have state transition probabilities based only on the current state whereas a Second Order chain will be based on the current state and the previous state. That is to say, the chance of of transferring from state A to state B will be different if we have just transitioned from B to A than from C to A.

The patch below is based on this idea, we now have nine sets of transition probabilities and it should hopefully be clear how these are selected based on the current state and the previous state. The messy maths part has now just been put into its own sub-patch in the bottom left to clean things up. Another quick note, the two states here are referred to as the current state and the n-1 state. This is just a simple way to reference which states we are talking about. If the current state is n, the previous state is n-1, the state before that n-2 and so on.




![2ndOrder](/a/2010-09-21-a-basic-intro-to-markov-chains/2ndOrder.png)



**0**


That's really all there is to the basics of Markov Chains. I'll revisit this stuff soon with some audio examples and a few other bits and bobs. Until then, go have a play with the patches.
