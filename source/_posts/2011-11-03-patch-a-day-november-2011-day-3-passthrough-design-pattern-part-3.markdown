---
date: '2011-11-03 21:49:17'
layout: post
slug: patch-a-day-november-2011-day-3-passthrough-design-pattern-part-3
status: publish
title: 'Patch-a-Day November 2011 Day 3: Passthrough Design Pattern (part 3)'
wordpress_id: '323'
categories:
- Patch-A-Day
- Pure Data
tags:
- design pattern
- FM synthesis
- polyphony
comments: true
---

Onto day three, and the last day of talking about design patterns for the moment. I'm going to finish off the synth voice bank patch from yesterday by neatening it up, minimising how much code we actually have and also by making the controls a bit more interactive.

By interactive, what I mean here is that when we switch between different voices, the values that the controls display will change to reflect the current settings of that voice. Without this it can become a bit tricky to make changes and will result in value jumps when a control starts from a different value to the one currently in use.

To do this I'll first modify the param abstraction that's used within the synth voice. It needs to be able to return the value for that parameter when we want it, which in this situation will be when it receives a "dump" message. You can think of it a bit like getters and setters in a class object. Have a look below.

![Synth voice with getters and setters](/a/2011-11-03-patch-a-day-november-2011-day-3-passthrough-design-pattern-part-3/synth-voice-control-params.png)

So there's a couple more send objects around the part of our code that does the limit/scaling logic and the param abstraction has the storage and dump objects. When a dump message gets sent to the voice it will dump out the right hand inlet the value for each parameter, prefixed by its name.

Now that all of this is getting sent back to the main patch, to get it changing the control values it's just a matter of reusing our param abstraction and putting in some send objects.

![Control parameter feedback](/a/2011-11-03-patch-a-day-november-2011-day-3-passthrough-design-pattern-part-3/control-feedback.png)

Nothing to it!

The next extension for this is to make a neater abstraction for the controls. Alas I'm running out of time for this evening so I'm just going to point you towards the [git repository](https://github.com/rumblesan/PatchaDay-Nov-2011/tree/master/Day-3_Passthrough-improved_controls) where you can download it and have a look.

tata for now
