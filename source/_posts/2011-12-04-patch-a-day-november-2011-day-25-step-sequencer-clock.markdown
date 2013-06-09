---
date: '2011-12-04 14:02:05'
layout: post
slug: patch-a-day-november-2011-day-25-step-sequencer-clock
status: publish
title: 'Patch-a-Day November 2011 Day 25: Step Sequencer Clock'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- launchpad
- sequencer
comments: true
---

OK, carrying on from yesterdays patch, lets get the stepping and clock for the sequencer.

![Sequencer clock and output](/a/2011-12-04-patch-a-day-november-2011-day-25-step-sequencer-clock/sequencer-clock-and-output.png)

The setup here is really pretty simple, but there's a couple small things to note. I'm routing for clock and reset messages, just to make things obvious when you;re controlling the sequencer. The reset message gives the pointer a traverse message which resets it to the head of our list of scalars. The clock message will trigger a next message to be sent to the pointer which will then send it's value to the series of daisy chained objects. This will cause all of them to output their values and they can be seen printed out to the console.

The trigger object is there because of how the pointer deals with coming to the end of a list. The pointer will output a bang, upon receiving a next message once it has already output the last list element. we want that final bang to send it back to the beginning, and then immediately output the first list element. To do that, when the pointer sends out its bang, it first triggers a new traverse message, and then triggers another next message, meaning the first step values get sent out.

Next I'm planning to neaten this up a bit, and then we can start dealing with Launchpad input.
