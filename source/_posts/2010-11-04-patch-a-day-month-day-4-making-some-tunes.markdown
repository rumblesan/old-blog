---
date: '2010-11-04 23:23:40'
layout: post
slug: patch-a-day-month-day-4-making-some-tunes
status: publish
title: 'Patch-a-Day Month Day 4: Making some Tunes'
wordpress_id: '123'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- audio
- generative
- Markov chains
- patch-a-day
- pure data
- sequencing
---

So today we actually get Pure Data making some noise at us by combining patches from days two and three. Since that's not an especially difficult task to complete I've extended the whole thing as well with some extra bits to make everything a bit more musical. The problem with our patch is that we don't actually have any control over what notes are going to be played, just what the interval between them will be. Whilst this makes it easier to have a small number of states have a large range of notes, it doesn't necessarily make for good music.



![Markov Tunes](/a/2010-11-04-patch-a-day-month-day-4-making-some-tunes/04-MarkovTunes.png)"

The first thing to notice is that there's a pretty big mess of stuff at the bottom of the patch. This is something that should be pretty simple but I've not spent time refining it so its ugly. There's a counter made of a float and an addition object, every time a new interval is chosen this counts up, when sixteen intervals have gone through it closes the gate, blocking the sixteenth choice, resets the note to sixty and the interval change to zero. The note then gets sent out and everything carries on as normal. This way we retain some control over the starting point of the tune that will be played so things don;t go wondering off too much.

The second addition is the scaler subpatch and this is really what makes the whole thing not sound rubbish.

![Scaler Patch](/a/2010-11-04-patch-a-day-month-day-4-making-some-tunes/ScalerPatch.png)"

Inside we have two tables, major and minor, which hold interval data for the major and minor scales. The incoming note value gets run through the mod 12 object, the output of this is then used to look up the corresponding value in the chosen table. The mod value is subtracted from the original note value and the new value added on. This way all the notes that come through will only be notes on the A major or Minor scale. To change the key it would be necessary to add a value to the beginning and then subtract this at the end, which I haven't done yet but will soon. This patch is going to turn up quite a bit from now on.

Finally the output of the scaler patch goes to the mtof object which converts our midi number into a frequency to feed to the synth.

Anyway, ramen time now, I'm hungry. Have fun playing with the patch until tomorrow
