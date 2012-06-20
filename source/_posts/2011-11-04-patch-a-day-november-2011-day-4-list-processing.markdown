---
date: '2011-11-04 22:47:13'
layout: post
slug: patch-a-day-november-2011-day-4-list-processing
status: publish
title: 'Patch-a-Day November 2011 Day 4: List Processing'
wordpress_id: '327'
categories:
- Patch-A-Day
- Pure Data
tags:
- euclidean rhythms
- list processing
- maths
- pure data
comments: true
---

This title may sound a bit dull but I've got some good intentions in mind so keep reading.

Yesterday I started reading up on how Euclidean Rhythms are created, I won't go into too much detail here yet as there are a few stepping stones first but for those who want to jump straight to it there's [this paper by Godfried Toussaint](http://cgm.cs.mcgill.ca/~godfried/publications/banff.pdf) and then a [blog post from Ruin and Wesen](http://ruinwesen.com/blog?id=216) which give most of the information you need. I had a look around to see if somebody had done this with Pure Data but it seemed most people had used or created externals. Whilst I'm not against using externals to do things, I wanted to try and make a Euclidean Rhythm generator in vanilla PD, because I'm a glutton for punishment pretty much.

A bit of research later and it's clear that this is going to need some interesting list manipulation to get the results we're after. Essentially the process involves interleaving the elements of a list in a fashion that's actually a bit tricky to do with PD because of it's non dynamic nature.

For this reason, this post and probably tomorrows will be all about list processing in PD. I've actually been learning quite a few things that in retrospect I'd consider to be the basics so I think it bears pointing them out as well for those that might not be so comfortable with PD's lists.

A couple quick things,



	
  * a list is a collection of data elements that has a **list** element at the front


	
    * **list 1 2 c d 5**

	
    * **list a b c**

	
    * **list 1.1 4 c**


	
  * if a list starts with a float or int then it doesn't have to have "list" at the front


	
    * **1.1 2.2 3.3** is the same as **list 1.1 2.2 3.3**

	
    * **a b c** is not the same as **list a b c**

	
    * **a b c **is undefined. some objects will treat it as a list, some won't


	
  * a bang is the same as an empty list




With these things in mind, lets have a look at the first patch that just simply takes a single list and serialises it into separate elements.






![List serialiser](/a/2011-11-04-patch-a-day-november-2011-day-4-list-processing/list-serialise.png)"




The output from this would look like :-





> 

>     
>     main: 1
>     main: 2
>     main: 3
>     main: 4
> 
> 






Nothing spectacular but what we're doing here is pretty important for the rest of this. The list split object here is used to pull off the first element of the list we feed in. This value comes out the left hand outlet, the rest of the list comes out the middle outlet and is stored in the second list object. When the first element is printed out it sends the rest of the list back into the split and in this manner we recursively pull the next element off the list, eventually printing them all out one by one.

Scaling this idea up a little it can be used to interleave two lists together. By that I mean that we can join two lists so that they are merged into one another, with the single elements from each list following the other. Probably best to explain with an example, if we have **1 2 3 4 5** and **a b c d e** then after the process we would have **1 a 2 b 3 c 4 d 5 e**. That's exactly what the next patch does.

![List interleaver patch](/a/2011-11-04-patch-a-day-november-2011-day-4-list-processing/list-interlever1.png)"

This patch talks about main list and sub list. To follow on from the above example, main list is **1 2 3 4 5** and sub list is **a b c d e**. The top left is just a bit of logic to make sure the sub list is in place before the main list starts the process running. The two groups of objects in the top centre are the list split feedback loops that serialise a list. These are setup so that a bang message can be sent to the get-next receive objects to get the next element. Also there's a route bang and a send $0-done. When there are no more elements in the main list we assume that everything is finished and the lists are interleaved.

The section in the middle at the bottom joins the main and sub list items into one list, sends that to the final joining section, and then sends the bangs to get the next two items. The section on the right gets the join item pairs, recursively joins them to make one list and then when it recieves the done signal it outputs it.

There are a couple of problems with this patch thought, that I'll fix tomorrow night but explain now in case someone wants to try and solve them themselves.



	
  * if the main list is shorter than the sub list then elements get missed off

	
  * if the sub list is shorter than the main list then the last sub list element is repeated

	
  * we can only join single elements, not pairs or other numbers




I still haven't quite worked out if I will be able to generate Euclidean Rhythms with these objects so if it turns out I can't then these will just be a series of articles on list processing in Pure Data (still useful in places, but maybe not so much fun). I'm hoping though that I can get it all sorted and start making some excellent generative drums. Time will tell I suppose.
