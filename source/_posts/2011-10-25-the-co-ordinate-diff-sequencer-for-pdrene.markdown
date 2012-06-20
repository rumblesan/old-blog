---
date: '2011-10-25 20:15:58'
layout: post
slug: the-co-ordinate-diff-sequencer-for-pdrene
status: publish
title: The Co-ordinate Diff Sequencer for PDRene
wordpress_id: '308'
categories:
- Pure Data
tags:
- algorithmic
- generative
- PDRene
- pure data
- sequencing
comments: true
---

So in the previous post I mentioned I'd do a more in depth look at what's going on inside the Diff Sequencer I've created. For a bit of a recap, [check out what I said there](http://www.rumblesan.com/?p=302).

So the Diff Sequencer is basically a way of sequencing pairs of numbers that are used to modify the X/Y coordinates of the current position on the grid. There are up to four pairs in a sequence and the sequencer will loop through these. Furthermore, each pair has a step value which is how many clock pulses that pair will be output for.

Lets jump straight to the internals to pick it all apart.

![Diff Sequencer internals](/a/2011-10-25-the-co-ordinate-diff-sequencer-for-pdrene/pdrene_diff_sequencer1.png)"

Most of the work is done by the pair of counters in the top left. The upper one counts up to the step number for the current pair and when it overflows it triggers the next counter to move along one more value in the sequence. The groups of objects in the top right are for externally changing the sequencers settings.

The interface between the UI and the counters is done using semi-colon sends from message boxes. The pair-value numboxes all have receive names in the format $0-#-x-set and $0-#-y-set where # is the pair number from 0 to 3. They all send to the $0-x-out and $0-y-out receives. When the counters move onto

The values are output each clock cycle and the whole thing will just keep going round. Settings, lengths etc can be modified as it runs.

Pretty simple really.

EDIT: only noticed last night that the image was extending out of the central div!! fixed now, but I should pay more attention
