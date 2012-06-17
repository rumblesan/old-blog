---
date: '2010-11-13 00:53:14'
layout: post
slug: patch-a-day-month-day-12-karplus-strong-strings
status: publish
title: 'Patch-a-Day Month Day 12: Karplus Strong Strings'
wordpress_id: '158'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- patch-a-day
- pure data
- synthesis
---

So, as regular readers might have noticed, I am not extending my sampler but am instead doing some synthesis. The reason for this is that I just spent an excellent couple of hours at a friends house making noise and discovered how to get my delay pedal to make string sounds. This reminded me of something called [Karplus-Strong synthesis](http://en.wikipedia.org/wiki/Karplus-Strong_string_synthesis) and when I got home I wanted to try it out in Pure Data.

Turns out it works, really very well, so I decided I'd write it up for tonight since I've done it and it's cool.



![Karplus-Strong String synthesis](/a/2010-11-13-patch-a-day-month-day-12-karplus-strong-strings/12-KarplusStrongString.png)"

For something surprisingly basic this does a really good job, the principle behind it is that you have a very short delay with a high feedback and a filter in the feedback loop. You send a brief pulse of noise into the delay chain and the output sounds very much like a string. It turns out that this is actually a pretty good model of how a real string behaves and that there are quite a few variables that can be played with to vary the sound.

With the patch above, there are a number of messages that you can click. When the message is sent into the trigger object a bang is sent out to turn on the noise source and a delayed bang is set up to turn it off. At the same time, the float value sets the output of a signal which in turn sets the delay of the vd~ object. The noise passes into the delwrite~ object and the chain starts itself off.

Changing the feedback will change how long the string sounds for, the filter frequency will change the timbre and the length of the noise pulse will change the attack and timbre characteristics. The eight frequencies I've chosen roughly play out a Major scale but they've only been tuned by ear.

Have a play around, and read up on the theory on the Wikipedia page if you want to get a good grasp. And if you're sitting around for a sample player abstraction then I'm afraid you have to wait until tomorrow afternoon when I will get to it. I just thought this was too cool to not talk about.
