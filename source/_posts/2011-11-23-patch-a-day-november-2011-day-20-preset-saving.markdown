---
date: '2011-11-23 22:29:19'
layout: post
slug: patch-a-day-november-2011-day-20-preset-saving
status: publish
title: 'Patch-a-Day November 2011 Day 20: Preset saving'
wordpress_id: '401'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- preset control
comments: true
---

Preset saving, done the simple way.

Well, maybe not that simple, this isn't some magical system that can be used like MaxMSP's autopattr system, but it should give a fair degree over the saving, loading and control of presets in PD. I've dug out the synth voices patch from Day 3 again and I'm going to be modifying the control abstraction so that that also stores the presets. This should again show that a nicely arranged and abstracted patch is a good thing which allows you to modify and extend without messing things around. Have a look at the main section of it.

![Control abstraction with presets](/a/2011-11-23-patch-a-day-november-2011-day-20-preset-saving/control-abstraction-with-presets.png)

All that's actually added here is a couple of extra control, a loadbang to set the preset number and a small subpatch called preset. It's the internals of this that are what's interesting.

![Preset saving patch](/a/2011-11-23-patch-a-day-november-2011-day-20-preset-saving/preset-saving-patch.png)

First things first, the section on the right is there to create the ten scalars we'll be saving our preset values in. At the moment this clears the window on start up and creates ten new scalars. This isn't really that useful if we want to have our presets saved with the patch itself, but this is just temporary while we build it so ignore it for now.

The data template and data window patches are contained here, both with names to make sure they're unique throughout the patch. The data structure has a float field for each of the settings we're saving (and an extra one here called number which isn't actually needed, I just forgot to take it out). The right hand inlet of the patch takes in the preset number, i.e., the position we want to save our values at. This value gets sent to a trusty bang into until into next into pointer setup so that as the preset number choice changes, the set object will always be saving to the correct place.

The clever bit here is that we're able to reuse the param objects from the previous patch. As values on the controls are updated in the control abstraction, those values are now also sent into these param objects as well. When the save button is pressed, it makes these objects dump out their values, these are fed into the set object making sure to keep the order of execution right. Hey presto, preset saving! Really not much to it.

Tomorrow (or maybe Friday night) I'll show how the presets can be loaded back out.


