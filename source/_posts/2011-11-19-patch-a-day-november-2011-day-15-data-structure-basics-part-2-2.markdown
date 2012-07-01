---
date: '2011-11-19 00:16:41'
layout: post
slug: patch-a-day-november-2011-day-15-data-structure-basics-part-2-2
status: publish
title: 'Patch-a-Day November 2011 Day 16: Data Structure Basics (part 3)'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
comments: true
---

I almost think that tonight's patch and last nights should have been rolled together into one post but I've also been thinking that some of these post can suffer from being too long and I'd prefer to have a greater number of smaller, more understandable posts.

This time I'm looking at the set object, but in truth there's really not much too it.

![Setting values for specific data structure items](/a/2011-11-19-patch-a-day-november-2011-day-15-data-structure-basics-part-2-2/setting-specifics.png)

The set object is located at the bottom of the patch and is really just a slightly modified version of the get section. The until object gets given a value, it increments the pointer to that position in the data structure list and then the value can easily be updated. This idea of incrementing pointers to get to specific places in a data structure is pretty important to grasp I feel.

I'm going to do one post on using the graphical capabilities of the data structures next but I'm only planning to spend a single post on it for the moment. Other possibilities to play with I think.
