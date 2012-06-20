---
date: '2010-11-02 22:59:35'
layout: post
slug: patch-a-day-month-day-2-markov-numbers
status: publish
title: 'Patch-a-Day Month Day 2: Markov Numbers'
wordpress_id: '118'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- generative
- Markov chains
- pure data
- sequencing
comments: true
---

So todays patch is a bit complex straight off the bat but its not too difficult once you see what's going on. I've revisited the Markov chain stuff and this time I'm actually using it to start doing something useful. The whole thing could probably be written better but it was a bit of a rush so I've used a clunky way to solve a timing issue I was having.



The patch looks messy because of all the links going everywhere but really, the middle section is four versions of the same thing.

![Markov Numbers](/a/2010-11-02-patch-a-day-month-day-2-markov-numbers/02-MarkovNumbers.png)

You can think of each of the four middle sections as separate nodes arranged in a ring. When each node fires, it can chose one of two states, when it transitions to one of these states it sends out a value that will change the current output value, and it triggers either the next or previous node on the ring.

The metro will send out a bang which will be sent first to the **gate **receive objects, on the node that has just been triggered, this bang will go through the spigot and open the second spigot. The bang from the metro will then go to the **clock **receive object where if the node had the spigot opened, the bang will go through and trigger the random object to give out a number between 0 and 99. The moses object will see if this is higher or lower than it's threshold and send the number out the corresponding inlet. It gets converted to a bang where it will make the message box send the change value, and it will also trigger the next node.

The change value goes to a simple patch where it will get added on to the current number. This can be fed into plenty of other stuff, but thats for later. I'll definitely be revisiting this soon and hopefully by then I will have cleaned it up a bit.

See you tomorrow.
