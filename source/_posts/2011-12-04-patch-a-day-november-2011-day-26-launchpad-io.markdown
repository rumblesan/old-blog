---
date: '2011-12-04 18:24:56'
layout: post
slug: patch-a-day-november-2011-day-26-launchpad-io
status: publish
title: 'Patch-a-Day November 2011 Day 26: Launchpad IO'
wordpress_id: '421'
categories:
- Patch-A-Day
- Pure Data
tags:
- launchpad
- sequencing
---

I said I'd do this once I'd done a bit more work on the sequencer, but I realised that it's probably a better idea to get this done first as it will make testing much easier. This patch is really just taking the MIDI input from the launchpad, formatting it into messages that are easier to deal with, and then translating our simple messages back into correct MIDI for us to send back out to it. As a quick refresher, here's what the Launchpad looks like.

![Novation Launchpad](/a/2011-12-04-patch-a-day-november-2011-day-26-launchpad-io/launchpad.jpg)"

During these posts, I'll refer to three sections of the button layout. The eight buttons on the top row are the control buttons, the eight down the right hand side I call the mode buttons, and the 8*8 grid is the grid. Explaining that should make it easier to follow what I'm talking about.

The input from the Launchpad for these is pretty basic, but it's not as easy to deal with as it could be, the grid and eight mode buttons all have MIDI note numbers assigned to them, but they're essentially mixed together. Ideally I want to separate the mode button messages from the grid messages, and have the grid messages be in a simple **(X Y value)** format. The control button input is all as midi control messages, which is easy enough to deal with, but they start at value 104 and it's much easier just to deal with 0 to 7.

One other thing to note, the input values from all button presses are either 0 or 127, either as note velocity or controller value. For input I find it much easier to just deal with 0 or 1 for button presses, output we actually need to use certain values to set the colours but that can be simplified easily enough. Here's the patch as it currently looks.

![Launchpad IO](/a/2011-12-04-patch-a-day-november-2011-day-26-launchpad-io/launchpad-IO.png)"

Top left is dealing with grid and mode note in values. Straight out of the notein object I've already converted the velocity values to 0 or 1 and the notein object itself is filtering for midi channel 1. This is the channel my Launchpad appears under in PD though it might be different depending upon what's plugged in. When I turn this into an abstraction, all the channel messages will be an abstraction argument to make integration easier.

The route object specifically selects for the eight note values of the mode buttons and then uses a fairly cludgy way to turn these into 0 to 7 numbers with the on/off value. Anything that isn't one of these numbers is from the grid which can be turned into the XY coordinates I'm after using some basic maths. The layout of the note numbers on the launchpad follows the equation (row * 16) + column, so by dividing by 16 we can get the row number, and finding the modulo remainder of  8 we get the column. These get packed with the note on/off and that's the grid message.

The control messages come from the ctl in object, situated middle top, and the channel filter has to be done externally because of the way ctlin works. The values also come in in the format (value, ctlnumber) which we want to be the other way round, the swap object handles that, then the ctl number has 104 subtracted from it and the data gets packed into a nice simple format to deal with.

The output sections basically do this in reverse. One thing to note is that I've added in a reset control. Sending the launchpad a zero value on control zero will turn off all the LEDs, a useful function to have.

The right hand side is just to take our input messages and convert them into output messages so the patch can be tested with a launchpad. The clr abstraction gives an easy way to set the output velocities/ctl values so we can select the colour we want on the launchpad. Internally they;re pretty simple.

![Launchpad colour abstraction](/a/2011-12-04-patch-a-day-november-2011-day-26-launchpad-io/colour-abstraction.png)"

The creation argument will set a default value, or the right inlet can be used to select and change it. The incoming value gets multiplied by the selected value so note off messages are still zero when they go out. The colours are red low, red full, amber low, amber full, yellow, green low and green full. I've just realised that technically all output to the launchpad should always be the off value (12) due to the internal buffering and so on it has available, I'll need to check that out, but for the moment, have a play around with this if you have a Launchpad and see how it works.

This kind of input filtering and manipulation helps to make life much easier when creating larger apps that interface with MIDI controllers and I hop this abstraction will be pretty useful in future.
