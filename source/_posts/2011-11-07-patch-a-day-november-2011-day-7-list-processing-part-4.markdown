---
date: '2011-11-07 21:38:05'
layout: post
slug: patch-a-day-november-2011-day-7-list-processing-part-4
status: publish
title: 'Patch-a-Day November 2011 Day 7: List Processing (part 4)'
wordpress_id: '349'
categories:
- Patch-A-Day
- Pure Data
tags:
- list processing
- random
---

I had a request from a friend of mine on Google+ the other night for an example patch that would randomise the elements in a list. I was thinking of doing it after the Euclidean Rhythms were finished but I think it fits in well with the rest of the list processing so I decided to write it up this evening. That also gives me a bit more time to neaten up the rhythm generation patch which is nearing completion.

The problem with randomising a list in PD is still that we can't really address specific elements of a list. We can however, split it at arbitrary points, pull out a single element and then rejoin the other sections. If the point at which the list gets split is randomised then we have an effective way of pulling random elements out. Have a look at the below patch to see how this works.

![Random list element chooser](/a/2011-11-07-patch-a-day-november-2011-day-7-list-processing-part-4/random-list-element.png)"

Split the list into two sections at a random point, use another split to pull the first item off the beginning of the second list, then rejoin these two sections of list. This results in a list with one less item and the random item. The randomisation is based off the length of the input list so it will always be in the correct range. If it selects the highest value then the second list section will be 1 element in length and that single element will be popped by the second split. If it selects the lowest, then the first half of the list will be empty (just a bang remember) but it will join fine with the other half.

Now we can do this it's just a matter of returning the smaller list back to the input and storing the randomly chosen item to be joined into a new list.

![Randomise list](/a/2011-11-07-patch-a-day-november-2011-day-7-list-processing-part-4/randomise-list.png)"

Each of the randomly selected items is send to a section of objects that will recursively add them to the previous output values. This gets reset when a new list is entered to make sure there's nothing stored between parsing lists.

The output of the join for the two other list sections is checked, if it's a list it gets sent back to the start for more parsing. If the last element has been selected then this value will be a bang, at which point the joined elements are output and there is no more processing to do.

Hopefully that will prove useful, at least for my friend. Using the stuff in the previous articles it wouldn't be difficult to change this to deal with other sized groups of items if you need it but I'll leave that up to you. I've included a stand alone abstraction of this patch in [the git repository](https://github.com/rumblesan/PatchaDay-Nov-2011) as well so you can just download it if you need it. It's called **ritem**, rather unimaginatively.

If there are any more requests then just ask and I'll have a go at getting them done.


