---
date: '2011-11-25 23:35:01'
layout: post
slug: patch-a-day-november-2011-day-21-preset-loading
status: publish
title: 'Patch-a-Day November 2011 Day 21: Preset loading'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- presets
comments: true
---

And now for the patch to load values out of the saved preset and into our settings. This might seem a little under whelming because there's not much to it, but a lot of the work was already done by the infrastructure already in place.

![Preset value loading](/a/2011-11-25-patch-a-day-november-2011-day-21-preset-loading/preset-loading.png)

I made a change to the previous section so that the pointer values won't be calculated until you hit the load or save buttons. Otherwise you're just adding in a bit of needless overhead.

The loading is even simpler than the saving, the preset patch number is selected, the load button pressed and the until object is used to calculate the pointer position. This pointer then gets sent to a get object which retrieves the values we want from our data structure scalar. The values then get sent straight to the gui elements in the above patch.

Simple, but pretty effective.
