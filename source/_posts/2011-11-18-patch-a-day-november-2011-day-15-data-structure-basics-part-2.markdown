---
date: '2011-11-18 23:46:45'
layout: post
slug: patch-a-day-november-2011-day-15-data-structure-basics-part-2
status: publish
title: 'Patch-a-Day November 2011 Day 15: Data Structure Basics (part 2)'
wordpress_id: '387'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
---

Apologies for missing yesterday, I was at the London Hackspace for the weekly music hackers meetup that's been gathering steam and I find that now I know a few more people there I quickly get sucked in and don't get around to working on the patches like I should be.

I've also realised that, unlike last time I did the patch a day month, I have a lot more projects and a fair bit more socialising going on. So I think I'm going to not worry too heavily about getting a new patch done every evening and instead just concentrate on getting them done in a timely manner and making them good. That said, "Patch-a-day-ish Month plus some days" doesn't have the same ring to it.

Anyway, onto the patch for tonight. Getting data from specific positions in a data structure list.

![Getting specific values from a data structure](/a/2011-11-18-patch-a-day-november-2011-day-15-data-structure-basics-part-2/getting-specifics.png)"

The left hand side is the template, struct and data window which should be familiar to you now. The right hand section can be used to automatically fill a data structure list with some data. It sets the pointer to the head of the list and sends it to the append object. Then it increments a counter using the until object and gives each of these values to the append as data, quickly filling it up.

The central section is the important part here. It takes an integer and then outputs the value stored at that position in the data structure. To do this, first the pointer object is given a traverse message, setting it so that it points to the head of the list. The until object then sends out the specified number of bangs which trigger next messages, incrementing the position of the list pointer.

Because we only want the specific value and not all the values, the pointer value that comes out at each next message is stored in a second pointer object. These work pretty much like float objects where a value passed into the right inlet is stored but not output. Once the until has stopped the value from the second pointer is output to the get object which puts out our value.

It's worth mentioning the bang object hanging off the first pointer. This is so that if we give a value greater than the length of the list we won't get errors being printed out. When the 'next' messages cause the pointer to hit the end of the list it will output a bang from the right outlet, this is sent to the until to stop it running so we end up just getting the last value.

Next stop is setting specific values in lists, then I'm going to start tackling some of the visual stuff you can do.
