---
date: '2011-01-29 17:35:39'
layout: post
slug: patchwerk-radio-how-it-works-and-how-to-write-patches-for-it
status: publish
title: 'PatchWerk Radio: How it works and how to write patches for it'
wordpress_id: '267'
categories:
- Git
- PatchWerk-Radio
- Programming
- Pure Data
- Python
tags:
- audio
- github
- PatchWerk Radio
- pure data
---

So how exactly does PatchWerk Radio work? What is it doing? How do the loaded patches interact with the main program? How can I write patches that will run on it?

Hopefully by the end of this article I will have answered all these questions and given you all you need to know to go about writing your own patches for PatchWerk Radio. These instructions will probably be updated in the future as more things get added and neatened up, but for the moment they should be fine.



So to start off, a diagram showing roughly what's involved.

![PatchWerk Radio Program Diagram](/a/2011-01-29-patchwerk-radio-how-it-works-and-how-to-write-patches-for-it/PatchWerk-Radio-Program-Diagram.png)"

The Python script is the heart of the whole thing. It's responsible for starting up a PureData sub-process, getting it to load up the master control patch, sending it all the streaming settings, choosing which patches it will load and then fading between them. All of this is done over a network connection between PD and Python and uses a slightly modified version of the [PyPD](http://mccormick.cx/projects/PyPd/) class written by [Chris McCormick](http://mccormick.cx).

The masterPatch is just an ordinary PD patch that deals with the cross fading, the streaming, the dynamic patch loading and the routing of messages between these sections. It has a number of sub sections each of which handle their different tasks.



	
  * The python-interface sub-patch deals with the network communications between the patch and Python.

	
  * The volume-control sub-patch just does the cross fading between the audio of the loaded patches.

	
  * The patch-control section is responsible for loading and closing the chosen patches using the dynamic messaging properties of PD.

	
  * The patch-interfaces are the important ones. This is where the audio from the dynamically loaded patches comes into the master patch and then gets routed to the streaming section. It contains two receive~ objects for left and right channels and the logic to change where these will get their data from. It's also where the messages to the loaded patches from the master patch are routed through.

	
  * The streaming sub-patch contains the oggcast~ object and all the routing to get the settings messages from python and format them correctly. The audio from the loaded patches gets routed to here from where it is streamed to the internet at large.


The audio patches themselves are treated by PD exactly as if the patch were opened from the file menu. This is good because it means that messages and audio data can easily be sent between it and the master without having to do any routing external with JACK for example. The drawback is that we cant just have an object and connect it up using patch cords, nor can we just give it a pre-defined set of send~ objects at the output because PD doesn't like that. As well as that, we have to be careful with how we name objects such as send and receives in case patches interfere with one another.

My solution to this was to use the abstraction arguments that PD has, specifically the $0 arg that gives the unique object number of the encompassing sub-patch/abstraction.

In each of the loadable patches there is an abstraction called patchComs. The audio from the patch is routed into this (There's also a switch~ object hanging off it, more on that later) where inside the audio is connected to two send objects named $0-l and $0-r. There is also a small section featuring a loadbang, an int with a $0 argument and a "send masterCom" object. Here's a picture for those who don't want to go and load it up. The switch~ is outside of this patch hanging off that outlet.

![patchComs abstraction](/a/2011-01-29-patchwerk-radio-how-it-works-and-how-to-write-patches-for-it/patchComs.png)"

When the patch is loaded the unique $0 argument gets sent, via the masterCom send object, to the python-interface in the master patch which sends it on to python. After it loads each new patch python waits for this message and when it receives it, registers that this is the unique id number for the patch. It will then send a registration message back to the master patch which will update one pair of receive~ objects to start getting their audio from the new send~ objects. A similar thing is done with the message sending objects. This is all done inside the patch-interface sections.

![patch-interface abstraction](/a/2011-01-29-patchwerk-radio-how-it-works-and-how-to-write-patches-for-it/patch-interface.png)"

Currently the only message from python to the new patch is one that turns on the DSP processing. Initially the switch~ hanging off the patchComs abstraction stops all DSP processing and is there to try and minimise the effects of a CPU usage spike on the audio. Once the patch is fully loaded and registered the DSP gets turned on.

Once the patch is making noise, Python gets the master patch to fade over to the new output channel, waits until this is done, then it closes the old patch. There are a few other housekeeping things done here such as turning off the DSP in the old patch and changing the receive~ objects to get their input from the dummy sends~. Once this is done it will sleep for ten minutes until it needs to choose the next patch to load. There are a few checks in place to make sure the same patch isn't loaded and that patches register themselves properly, but really everything is pretty simple.

There are a few things that need to be noted before making a patch for PatchWerk Radio. Because the patches are loaded under the same instance of PD, they could possibly interfere with each other, This means that sends and receives should ideally have arguments to make sure that they will be unique within your patch and that abstractions themselves should have fairly specific names if you're using them in your patch.



	
  1. When the Python script is choosing the next patch to load it will pick a random folder from it's given patch directory. Once it has a folder it will **check inside this folder for a patch named main-*.pd **and then load this if it finds it. If it doesn't find it then it will try again so make sure the patch you want loaded follows this naming convention.

	
  2. Because of the way that the close message in PD works, **each main patch must have a unique name**. Currently I'm just naming everything with incrementing numbers in folder names and main patch names and that should be fine for the moment. If it becomes an issue then I'll come up with something else.

	
  3. **Patches need to be totally stand-alone**. They need to start on their own and play on their own. In the future I hope to add the ability for information (weather, stock prices, music scales etc) to be requested from the master patch but for the moment your patch has to do everything by itself.

	
  4. **Patches play for about ten minutes** so bear this in mind. Again, in future I hope to have this be specifiable on a per patch basis bit it's not here yet.

	
  5. **Objects such as send, receive, delay chains and buffers need to use $0 arguments to make sure they're unique.** Otherwise there might be inter patch interference. I need to fix this in some of the patches already in the repository so it's not a horrendous problem so far but better not to do it.


That's really everything there is to it. I still want to do work on the basic infrastructure of the system but that shouldn't affect the design of the patches. For those who are interested in getting involved, I'll point your towards the [patch repository on GitHub](https://github.com/notesandvolts/Radio-Patches). You can either fork it on there and then send me pull requests, or get in contact with me and send me the patches so I can put them in.

Ask questions in the comments in case I've missed anything out. Now I'm just going to spend some time writing more patches, hope you'll come and join me.
