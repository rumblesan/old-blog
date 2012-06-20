---
date: '2011-11-21 21:15:56'
layout: post
slug: patch-a-day-november-2011-day-18-data-structure-basics-part-5
status: publish
title: 'Patch-a-Day November 2011 Day 18: Data Structure Basics (part 5)'
wordpress_id: '395'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
comments: true
---

Ok, not quite done with data structures yet. I realised that I should probably go over how you store symbols and arrays in a data structure. Tonight it's a quick post on symbols, I'll try to cover all of arrays tomorrow.

The first thing to know is that storing symbols in a data structure is almost, but not quite like, storing floats. You can't actually use the append objects to create a new scalar with a symbol directly. You instead have to create the scalar, then set the symbol element once it's made. This feels really kludgy to me and I'm going to be doing some investigating to see if there's something I've missed. But this appears to be the way it's done.

![Storing symbols in a data structure](/a/2011-11-21-patch-a-day-november-2011-day-18-data-structure-basics-part-5/storing-symbols.png)

The struct we're dealing with defines a float and a symbol. I realised that you need to have a float as an element in the struct because otherwise I can't see a way to create a new scalar. The set object can only update values, not create new scalars. So the append object is used to create some scalar entries in our data structure. The set object can then be used to update the values for our symbol.

Notice that there's now a -symbol flag there. This means the set object will accept symbols BUT can only accept symbols. There would need to be two different set objects now, one to set the value of a, the other for b.

The get object still works exactly the same, the outlet for a sends out its float, b sends out it's symbol.

I realised that symbol storage is actually pretty important, mostly just so in a preset storage system you can give names to the presets. The array storage I'm still working on at the moment though it's not too much more complex. Patches will be with you tomorrow.
