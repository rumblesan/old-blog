---
date: '2011-11-13 16:29:20'
layout: post
slug: patch-a-day-november-2011-day-11-basic-sequencer
status: publish
title: 'Patch-a-Day November 2011 Day 11: Basic Sequencer'
wordpress_id: '366'
categories:
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- euclidean rhythms
- sequencing
---

Generating patterns is all well and good, but we actually have to be able to play them back. I'm going to start off with a basic sequencer and combining the Euclidean Sequence generator into a sequencer voice. To begin with I'm just going to do this with tables. I've got a plan for some time next week to start getting into the PD data structures stuff again which will make it possible to create much more powerful sequencers but there's no need to go getting overly complex yet.

![Basic sequencer](/a/2011-11-13-patch-a-day-november-2011-day-11-basic-sequencer/Basic-sequencer1.png)"

Starting on the left, I'm reusing the list serialisation patch here from the first list manipulation examples I did. A list comes in, it's length gets stored in a variable and used to resize the table, a counter gets reset to zero and then the list gets serialised. As each list element gets sent out, it triggers the next number from the counter. These are used with the tabwrite object to write the data into the sequence table.

On the right hand side there's the table object which just stores the data. I haven't bothered using $0arguments here to make this abstraction safe yet but I'll do that later. Below that there's a pretty typical metro/counter setup that reads the values out of the table. At the moment the counter will just keep going and reset itself once it hits the length of the current sequence and the sequence can be changed whilst it's running. This may not be desired behaviour, depends on what you're doing.

Adding the Euclidean pattern creator abstraction into this is now really easy.

![Euclidean rhythm sequencer](/a/2011-11-13-patch-a-day-november-2011-day-11-basic-sequencer/Euclidian-rhythm-sequencer.png)"

Really really easy.

At the moment the erhythm abstraction will generate an output pattern whenever one of the input values changes, which isn't quite in keeping with PD convention of hot and cold inlets but personally I think it's a little more useful here. Again, it depends what you're after and shouldn't be difficult to change.

The next step is to turn this all into a single abstraction and then make a full drum sequencer with it. I think that I'll get that done now and post it and then take a bit of a break for the rest of today. I know I'm still one patch behind but I'll catch up on Monday night. Then I need to start getting into the data structures again.
