---
date: '2009-04-03 13:01:00'
layout: post
slug: midi-step-sequencer-for-ds
status: publish
title: Midi Step Sequencer for DS
categories:
- Music
- NDS Homebrew
- Programming
comments: true
---

Well the project that has kept my evenings busy and my girlfriend mildly annoyed is soon to be released...I think. And seeing as I can't remember if I've explained already (and can't check the block thanks to work blocking it) I'll explain everything here.







A MIDI enabled Nintendo DS based sequencer.







Currently featuring 4 tracks, each track with 7 patterns and a pattern sequencer. Patterns are 8 notes by 16 steps.







Specific midi notes can be set for each pattern note, patterns and midi settings can be loaded and saved and there is a follow mode displaying the pattern currently being played for a particular channel so you can edit it as its playing.







Top DS screen is used to display information on playing/active tracks, BPM, global step position and which notes are being triggered.







MIDI output is done via the DSBrut serial card currently.










There are still some things that need to be sorted, I want to add the DS Midi Interface library so people dont have to have the DSBrut, I need to come up with a reasonable way of handling sending midi note off messages and having a variable note length. There are a few GUI bits to properly sort as well but most of the needed functionality is done.










I'll update a bit later with more stuff and hopefully some idea of when it will arrive. All the code will be freely available as well so people will be free to mess with it and improve.



