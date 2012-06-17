---
date: '2009-11-20 15:17:00'
layout: post
slug: state-of-the-sequencer
status: publish
title: State of the sequencer
wordpress_id: '51'
categories:
- Pure Data
tags:
- Programming
- pure data
---

So the realisation that coding C++ on the Touch book was going to be tricky has meant I've been looking at better (read as easier) ways to create the sequencer.

Pure data has therefore been decided upon for initial work. The differences from MaxMSP became pretty apparent when I found out about Data Structures and how complex and useful they are. A little bit of work and understanding later and it's all falling into place. Tonight I should be able to have a working abstraction to create multiple drum sequencer tracks.

One other thought that has occurred to me is that whilst Pure Data is good for all this, the GUI really leaves a lot to be desired. With this in mind my plan will be to just create the data structures and sequencing in PD and have these be accessible via OSC, then to create an OSC based GUI in something like pyGame.

Interesting times afoot I reckon

Guy
