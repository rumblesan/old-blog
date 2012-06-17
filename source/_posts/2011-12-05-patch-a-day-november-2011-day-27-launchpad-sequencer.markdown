---
date: '2011-12-05 21:41:41'
layout: post
slug: patch-a-day-november-2011-day-27-launchpad-sequencer
status: publish
title: 'Patch-a-Day November 2011 Day 27: Launchpad sequencer'
wordpress_id: '426'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- launchpad
- sequencer
---

Right, time to hook the launchpad up to the sequencer. I've modified the Launchpad IO abstraction to neaten it up and make it actually deal with output and input. The sequencer patch has been changed so that incomng grid messages are converted to a stop number and the mode buttons select the track number to update and the main clock is now on the outside.

Let's run through them and I'll explain a bit about what's going on.

![First launchpad sequencer](/a/2011-12-05-patch-a-day-november-2011-day-27-launchpad-sequencer/first-launchpad-sequencer.png)"

The sequencer is now the steps abstraction and the first argument tells it how many steps we want to have. The basic metro clock is still there, entirely unchanged. The launchpad_io abstraction now takes the channel as an argument as well. All simple and a bit dull.

![Improved launchpad IO](/a/2011-12-05-patch-a-day-november-2011-day-27-launchpad-sequencer/improved-launchpad-IO.png)"

The launchpad IO now just deals with outputting the MIDI in messages and sending the MIDI out messages. All IO goes through a single inlet or outlet and all messages are prefixed with either grid, mode or ctl to show where it's from or going to. There's also the reset option available which sends the clear message.

![Updated step sequencer](/a/2011-12-05-patch-a-day-november-2011-day-27-launchpad-sequencer/step-sequencer.png)"

The step sequencer now has a bit more functionality. It takes the input direct from the launchpad and pulls out the grid and mode button messages. The mode messages control which track we are updating and do that by pre-pending the track name onto the front of the grid message. The tracks then route for this as they do normally. Note the spigot on the mode section, this is there so that only button on messages get through. We don't actually care about button off messages here so we just stop them coming through.

The grid messages are converted from their XY format into a single value that gives the step position. At this point it may be clear that there is a problem with the current setup. The grid buttons also have button up and down messages coming through, so when we press a button the **1** value gets stored, but as soon as it's released the **0** is stored over the top of it.

For the moment I'll let you think about how you might solve this, tomorrow I'll show you how I do it.
