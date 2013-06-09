---
date: '2011-11-16 23:15:54'
layout: post
slug: patch-a-day-november-2011-day-14-data-structure-basics-part-1
status: publish
title: 'Patch-a-Day November 2011 Day 14: Data Structure Basics (part 1)'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
comments: true
---

Starting at the beginning with data structures. There's a lot to take in, but it's pretty cool once you get down to it. I found the old patches I wrote when I was getting to grips with it all the first time round which is pretty helpful but this time I'll actually write things down heh.

First up, you can think of Data Structures in PD as lists of items, where each list has a specific name, and the items they contain can be floats, symbols, arrays, or a list of other data structures. To navigate around these lists you use pointers, which literally just point to a position on the list.

When creating a patch that uses data structures, there are three parts that really make the structure. These are a template, a struct and a datawindow. The template is a subpatch that contains a struct. The struct defines what data the structure contains and the datawindow will contain the data.

The data is stored as an ordered list of scalars, where a scalar would contain an entry for each of the values defined in the struct. The lists are navigated by using pointers, one of the PD data types, that literally just point to a single scalar in the list.

Lets have a look at a patch to try and clear some of this up.

![Basic data structure](/a/2011-11-16-patch-a-day-november-2011-day-14-data-structure-basics-part-1/basic-structure1.png)

In the top left are the three objects that make up the data structure. The template1 subpatch contains a single struct object. The struct defines a structure called struct1 with a single field, the float a. The datawindow1 subpatch has no objects in it. One thing to note at this point, the name of the struct has to be unique throughout PD otherwise you'll get an error being thrown, the same goes for the datawindow.

Now that the data object has been constructed, we need to add some data to it and we can do this using the append object. This takes a pointer into its rightmost inlet and then the values to store are entered using the other inlet. Append is given the name of the struct that it will be modifying and also an argument for each value in the struct we want to modify. If you have a struct with multiple values then you don't need to modify all of them.

The pointer object gets given a message to tell it which datawindow it's pointing to and then a bang to get it to output the value of its current pointer. When we first initialise it with a traverse message the pointer will point to the head of the list. This isn't actually a scalar but is the position in front of the first scalar element so any value appended to it will get added after this. The pointer goes to the append object to tell it where it will be appending the values.

Sending the pointer a next message will get it to move to the next scalar in the list, to begin with that will result in an error because there aren't any other values, but if there were it would mean we could append after any position in the list.

The append object will increment the pointer it has itself, so all that's needed is to send it the pointer then send whatever values we want to store in the left inlet.

To retrieve them you can use the get object. This works in a similar way to append with the arguments tell it what struct and what values it's dealing with and the pointer telling it which scalar to retrieve. This time it's necessary to step through manually and you can do that with next.

Here's an example of how easy it is to extend this to more float values if you want.

![Data structure with multiple values](/a/2011-11-16-patch-a-day-november-2011-day-14-data-structure-basics-part-1/multiple-values.png)

Not sure I'll be able to get another post out tonight unfortunately, relearning this stuff has been a bit of a crash course and took longer than I expected. Either way, I know the direction I'll be heading with this over the next few days so I shouldn't have any problems working out what I want to patch.
