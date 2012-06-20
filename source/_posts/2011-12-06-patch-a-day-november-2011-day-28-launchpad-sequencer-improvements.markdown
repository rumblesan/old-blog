---
date: '2011-12-06 21:01:27'
layout: post
slug: patch-a-day-november-2011-day-28-launchpad-sequencer-improvements
status: publish
title: 'Patch-a-Day November 2011 Day 28: Launchpad sequencer improvements'
wordpress_id: '431'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structure
- launchpad
- sequencer
comments: true
---

Just a shortish one today, Yesterday I said that the step sequencer we'd built was mostly working but had a fairly vital flaw, we couldn't actually save values in the data structure because we were getting not on and off messages from the launchpad. There are a few ways to fix this but I think that the way I do it here is the simplest and most flexible.

First things, we only want note on grid messages, that can be fixed with a spigot in the main sequencer patch.

![Sequencer only accepts note on grid messages](/a/2011-12-06-patch-a-day-november-2011-day-28-launchpad-sequencer-improvements/sequencer-nnote-off-grid.png)

Note off messages will now get blocked and won't go through to the track abstractions.

![Track abstraction now checks current value](/a/2011-12-06-patch-a-day-november-2011-day-28-launchpad-sequencer-improvements/track-abstraction-that-checks-current-value.png)

There's a few less objects in the track abstraction now but a few new ones as well. The biggest change is that the input is now actually only a single number. This number is used to calculate the pointer to the step position as normal, but it then gets sent to a get object as well as the set object. The abstraction will now check the current value in the data structure at that step and then update it with the opposite value, so we've successfully toggled the value in the data structure.

It's easy to change this behaviour if needed, you might want to increment it or do something else, that's up to you. Obviously we cant just send in a value for the abstraction to store now but that's also easy to change, or just use the old version.

Anyway, the launchpad can now update the data structure and the sequencer actually sequences if you turn the clock on. Of course some lights on the Launchpad would be good, but that's a task for next time.
