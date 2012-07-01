---
date: '2011-11-27 22:39:47'
layout: post
slug: patch-a-day-november-2011-day-22-preset-file-saving
status: publish
title: 'Patch-a-Day November 2011 Day 22: Preset file saving'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- presets
comments: true
---

The preset loader is working pretty well, but at the moment it's limited to only saving presets within one PD "session". If we close and then reopen the program then all our presets are lost. To make this really useful, you need to be able to save the data structure info and have it loaded up next time you start the program up.

Luckily Pure Data allows you to save the data structure information to a file and then read it back in later, and we can use that to make our preset information usable between sessions. Here's the updated preset object.

![Preset data structure files](/a/2011-11-27-patch-a-day-november-2011-day-22-preset-file-saving/preset-file-saving.png)

The patch now has a third inlet that can be used to give clear, file load or file save commands. The clear command is just the initial blank patch loadbang setup that has always been in the patch. This means we can clear all the presets and reload ten blank presets if we want.

The fileload and filesave commands will give a symbol to a makefilename object. This will give us a filename in the format **preset_<name>.pdc** actually saving or loading the data to and from the file is as simple as sending a read or write command to the data window patch. Here I've had to get the $0 value worked into the setup but that's only necessary if your data window uses it.

So now we can save presets between sessions, have multiple abstractions load and save to a single file and can start making some much easier to use performance patches.

One thing to note that I've found. In the file containing the data structure data it has the name of the data window it was saved from. When you reload the data from the file, if the name inside the file matches the data window you load into you'll get a "multiply defined" error. This doesn't seem to cause any issues, but I mention it to stop any confusion.
