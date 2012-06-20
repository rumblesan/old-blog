---
date: '2011-12-07 23:16:57'
layout: post
slug: patch-a-day-november-2011-day-29-launchpad-lights
status: publish
title: 'Patch-a-Day November 2011 Day 29: Launchpad lights'
wordpress_id: '435'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- launchpad
- sequencer
comments: true
---

Sending output to the launchpad is pretty easy. Sending the right output, in a way that's easily configurable and fits in with the standard is a little trickier. I've had more of a read of the Launchpad programming guide and have a better handle on the double buffering and so on and I'll put some of that into practise here. The updates to the sequencer here are, I feel I should point out, as pretty or high performance as they could be. There's definitely a lot more tweaking needed.

One of the things I've found a bit of a problem is sending the large number of update messages to the launchpad. There's a slow down in PD whilst it's going. I don't know if it's due to the MIDI output, or just trying to send a mass list of 64 messages and needing to make the process more efficient but more investigation is needed.

![Step sequencer track with light output](/a/2011-12-07-patch-a-day-november-2011-day-29-launchpad-lights/step-sequencer-with-lights.png)"

This is the updated track abstraction with the output for the light states. The left hand section that updates the data structure will now also send out a message with the new value of the updated step. The right hand sections are for dumping out the state of all the steps in the data structure. This is used when changing tracks as we want to update the launchpad with the new values and clear the old ones. By dumping out the state of all on or off steps we clear the old data and fill the grid with the new. This could be made more efficient by first clearing the grid, then just sending the steps that are on but i decided this is initially simpler to deal with.

![Full sequencer with light state output](/a/2011-12-07-patch-a-day-november-2011-day-29-launchpad-lights/full-sequencer-with-light-state-output.png)"

The main sequencer section has been updated as well to parse the data now being output by the tracks. The objects right at the bottom will take the step messages, convert the step number back into the XY coordinate and change the 1 or 0 value into the correct note velocity for the colour we want. The clr abstraction works differently now just to point out. It takes two arguments, one is the colour value to send out when it gets a 1 input, the second for when it gets a 0 input. I'm following the Launchpad programming guide by sending out a value of 12 for off. This apparently makes it easier to add in double buffering later which might well be necessary.

There's also a small section in the middle at the top that sends out the light on/off messages for the mode lights. The tracklight patch just keeps track of the current track number and, when the track changes, will send out an off message for the old button and an on for the new one.

As I said, there's actually a fair bit of work that needs to happen on this to make it fast enough but it's not bad as a start. I'll probably concentrate on tacking on the drum sounds for the next patch-a-day and then call it finished for the moment.

That will also actually be my last patch-a-day patch for this round. I'm going to be continuing work on this sequencer and I'll be writing more of it up, just not worrying about doing it once a night though heh.
