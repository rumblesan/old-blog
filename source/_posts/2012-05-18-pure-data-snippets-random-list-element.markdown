---
date: '2012-05-18 21:48:48'
layout: post
slug: pure-data-snippets-random-list-element
status: publish
title: Pure Data snippets Random list element
categories:
- Pure Data
tags:
- snippet
comments: true
---

Hey, just a small post, coding some PD and realised that the small snippet I just made to select a random element from a list may well be useful for some people. I think I might start doing more small, code snippet type posts because they're quick and easy to do.

[![random list element](http://rumblesan.com/a/2012-05-18-pure-data-snippets-random-list-element/Screen-Shot-2012-05-18-at-21.43.10.png)](http://rumblesan.com/a/2012-05-18-pure-data-snippets-random-list-element/Screen-Shot-2012-05-18-at-21.43.10.png)

So the section on the right, after the first trigger, takes the list length then calculates a random number between 0 and length 1. The list goes to the split which will send the first section of the split out the left inlet, and the latter section out the middle inlet. This middle output list will have a random element at the beginning so we just trim that off with another split.
