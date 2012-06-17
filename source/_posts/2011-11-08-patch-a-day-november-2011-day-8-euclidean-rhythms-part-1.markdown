---
date: '2011-11-08 23:51:46'
layout: post
slug: patch-a-day-november-2011-day-8-euclidean-rhythms-part-1
status: publish
title: 'Patch-a-Day November 2011 Day 8: Euclidean Rhythms (part 1)'
wordpress_id: '353'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- euclidean rhythms
- list processing
---

Right, enough list processing for the moment, lets get down to what we were aiming for. Euclidean Rhythms are rhythms generated using an algorithm very similar to [Euclid's Algorithm](http://en.wikipedia.org/wiki/Euclidean_algorithm) for computing the greatest common divisor of two numbers. What it does for us is it means we can evenly distribute a number of hits into a given number of beats and it just so happens that this actually generates some well known drum patterns from various musical styles.

It's worth going and reading [this paper by Godfried Toussaint](http://cgm.cs.mcgill.ca/~godfried/publications/banff.pdf) and this [blog post from Ruin and Wesen](http://ruinwesen.com/blog?id=216) for more in depth discussion but I hope to explain how this works in a fairly simple manner. First up, lets have an example.

We want to evenly spread 3 hits into an 8 beat space, this means there will be 3 beats and 5 spaces. The sequence will be described as lists of ones for hits and zeros for spaces and we'll start off with two separate lists. The diagram below should easily show how the lists are interleaved together until the remained reaches zero or one. This diagram uses columns to denote elements of multiple items.

![Euclidian Rhythm (3,8)](/a/2011-11-08-patch-a-day-november-2011-day-8-euclidean-rhythms-part-1/Euclidian-Rhythm-38.png)"

At each step, you take the current remainder, interleave it with the main list and take any remainder left. You keep interleaving the two lists until the length of the remainder list is one or less, then just read out the list. So above, When we interleave the list of five zeros into the list of three ones, we have a remainder of two. This is greater than one so we interleave this into the main list again and the remainder this time is a single element.

This works just as well if we started with more ones than zeros as well.

![Euclidian Rhythm (5,8)](/a/2011-11-08-patch-a-day-november-2011-day-8-euclidean-rhythms-part-1/Euclidian-Rhythm-58.png)"

After wrestling for a couple of evenings over how to do this in PD, I decided that the simplest way to do it would be to use a combination of the list length matching abstraction and the interleaving abstraction from the previous two days, and then just keep track of the element size of the main list and remainder. The work flow is pretty simple



	
  * Start with two lists of single element items, the main list is ones and the sub list is zeros

	
  * Get the excess elements from the longer list, this is the remainder


	
    * The element size of the remainder is the same as whichever list it came from


	
  * Interleave the main list and the sub list, element by element to get the output list

	
  * Check the number of elements in the remainder


	
    * If it's one or less then join the output list and the remainder to get your rhythm pattern

	
    * If it's greater than one, send the output list and the remainder back through the process



The first thing that's needed for this is a modified list length matching patch and that's what I've built this evening. The previous list matcher would give you out the excess section, but would leave you to externally work out which list it came from and what the element size is. Really, this should be handled inside this patch so that we give it two lists and their element size, and we get out three lists with their element sizes.

![Improved list length matching](/a/2011-11-08-patch-a-day-november-2011-day-8-euclidean-rhythms-part-1/improved-list-splitting.png)"

The patch here does much the same as the previous version but I've moved around the logic a little to try and make things more understandable. I'm using the PD value objects which I discovered the other night and I wish I'd used them sooner. The major change to the behaviour is the section in the middle/right where we compare the number of elements in each list. If the main list is greater in length than the sub list then that's where the remainder will come from, meaning the remainder's element size will match the main lists. If the sub list is longer then the remainder will come from here so it's element size will match the sub list's.

In this way, we now get out the three lists and their element sizes. Tomorrow night I'll tie this into the interleaving and recursion and generate the patterns themselves.
