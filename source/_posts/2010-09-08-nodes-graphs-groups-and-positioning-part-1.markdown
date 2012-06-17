---
date: '2010-09-08 12:03:49'
layout: post
slug: nodes-graphs-groups-and-positioning-part-1
status: publish
title: Nodes, Graphs, Groups and Positioning (part 1)
wordpress_id: '24'
categories:
- SuperCollider
tags:
- code
- lessons
- SuperCollider
---

So I've been reading up more on this, as I feel it's one of the last major things to get my head around before fully understanding SuperCollider.  The premise is pretty simple but I found there's an awful lot of depth to it if you start diving in. For this reason there will be a couple of parts to this, I'm guessing two or three.

The basics is where we'll start and, thankfully, they aren't to taxing. There won't be much code in this post but there should be a fair few diagrams to help visualise everything.



To begin with, I'll introduce the four big words I used in the title.

**Nodes, Graphs, Groups and Positioning.**

The three of these are all quite strongly tied together but have slightly differing meanings depending on whether you're looking at the maths, or at SuperCollider itself. In the mathematical sense, a Graph (not in an x-y diagram sense) is essentially a number of vertices joined by edges. This creates a network that can be used to do various things, the [wikipedia article](http://en.wikipedia.org/wiki/Graph_%28mathematics%29) is very good at explaining some of this and infact I'll lift a picture from it here quickly.

![Mathematical Graph](http://en.wikipedia.org/wiki/Graph_%28mathematics%29)"

SuperCollider uses graphs internally when dealing with Synths that it is running to calculate in what order the functionality of the UGens should be happening. It is doubtful the user will have to deal with this themselves.

Nodes and Groups are something that you will deal with often if you use SuperCollider. A Node can be a single Synth or a Group on the server. A Group can be a collection of Synth Nodes and/or more Group Nodes.

    
    
    t = Synth('basic-FM',['freq2', 200, 'amp1', 300]);
    


The above code for example is us creating a Synth and storing a reference to it in the variable t. The reference we are actually storing is the ID of the Node on the Server so when we run commands that refer to a synth, we're actually just sending messages to that Node.

To make it easier to control and manage multiple Nodes, they can be collected into a single Group which makes life much easier when having to think about Positioning.

Positioning isn't really that difficult to get your head around. If we have a synth, and the audio from that goes through an effect, then the sound out of the effect is dependant upon the sound out of that synth. We need to make sure that SuperCollider calculates the synth's audio so that the effect can modify it. If we were to create the synth first and then the effect then the effect node would come after the synth node by default but it's not always such a good idea to rely on this, especially not if things get complicated. I'll be covering how you can tell SuperCollider what order things should be in in a later post, I'm just trying to get through the idea that this is important to think about but not too complex. A picture from the documentation on [Order of Execution](http://supercollider.svn.sourceforge.net/viewvc/supercollider/trunk/common/build/Help/ServerArchitecture/Order-of-execution.html) might make things a little clearer.

![Order of execution diagram](http://supercollider.svn.sourceforge.net/viewvc/supercollider/trunk/common/build/Help/ServerArchitecture/Order-of-execution.html)"

It is also worth mentioning here that ordering works much the same for Groups as it does for Nodes. We can have a group of nodes that all represent synths and this group is positioned before an effect node so that the output from the synths is calculated and mixed together, before going to the effect.

So, to round everything up, a quick overview in bullet point format.



	
  * The SuperCollider server keeps track of Synths and Groups as Nodes

	
  * A Group is a collection of Nodes itself

	
  * The internals of a Synth Node will be a Graph of UGens created from the SynthDef

	
  * The Nodes will have an order and this can be set and changed

	
  * A Node that is dependant upon the audio from another Node must be placed after it


Part two should have some more code examples, probably something simple involving a synth and an effect and I'll aim to start getting the code examples up on Github.
