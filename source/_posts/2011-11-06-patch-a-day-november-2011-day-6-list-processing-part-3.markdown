---
date: '2011-11-06 23:16:26'
layout: post
slug: patch-a-day-november-2011-day-6-list-processing-part-3
status: publish
title: 'Patch-a-Day November 2011 Day 6: List Processing (part 3)'
wordpress_id: '344'
categories:
- Patch-A-Day
- Pure Data
tags:
- euclidean rhythms
- list processing
comments: true
---

More list processing today I'm afraid. I'm still working out how to properly transfer the Euclidean Rhythm equation to vanilla PD and I'm getting closer, but I keep finding there's different problems to do with list parsing to overcome, which is great as far as me having things to write about goes, but I'd quite like to get to the point where I can make some music soon.

Tonight's post is a bit of a short one because I'm knackered after the weekend. The problem is that the we need to find out what the remainder of two lists will be when they're interleaved. The interleaving patches created last night will deal with this gracefully, but when generating the rhythm patterns we don't actually want this to happen. We need to pull the remainder off and then re-interleave this with the output.

To further complicate matters, the remainder is dependant on the size of the elements we are dealing with so our patch needs to take this into account. Lets start off with the simplest case first.

![List length matching](/a/2011-11-06-patch-a-day-november-2011-day-6-list-processing-part-3/list-length-matching.png)"

The list length objects calculate the lengths for each list, the min object is used to find which of these is the smallest and then both lists are split by this value. On the list with the smallest length the middle outlet of the split object will send a bang, on the longer list we get the excess elements.

It's still necessary to make this deal with lists where we have different element sizes and at the moment if the two lists are the same length then there won't be anything output for the excess. Both of these need fixing and the following abstraction does just that.

![List length matching with elements](/a/2011-11-06-patch-a-day-november-2011-day-6-list-processing-part-3/list-length-matching-with-elements.png)"

As soon as you start dealing with multi item elements, things get a bit trickier. It's times like this I wish that PD had better data structures for doing this sort of thing. This works in much the same was as the first version, but I've split everything out to make it a bit neater.

Top left is all the input parsing and making sure the data gets sent through in the right order to stop there being timing issues.

The two sections on the right are where the number of elements in a list and the split values are calculated. This deals with lists that have incomplete elements, i.e. the list **1 2 3 4 5** with an element size of two should be three elements, **(1 2), (3 4), (5)**.

The number of elements in each list is calculated, these values are compared and the smallest chosen, this is then converted from an element number back into an item number for each list and then they're split.

The bottom left just makes sure the output comes out correctly, with a bit of logic to deal with even lists and the possibility of two bangs from the list splits for excess values.

Come back tomorrow where I might actually be making some patterns... if I can wrestle the maths into place.
