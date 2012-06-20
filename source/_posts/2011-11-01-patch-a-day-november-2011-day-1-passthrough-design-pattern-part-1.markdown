---
date: '2011-11-01 19:55:00'
layout: post
slug: patch-a-day-november-2011-day-1-passthrough-design-pattern-part-1
status: publish
title: 'Patch-a-Day November 2011 Day 1: Passthrough Design Pattern (part 1)'
wordpress_id: '315'
categories:
- Patch-A-Day
- Programming
- Pure Data
tags:
- design pattern
- pure data
comments: true
---

I'm planning to spend the first few days of this week going over a design pattern I've found myself using in various ways. For anybody who is unsure what a Design Pattern might be I'd recommend checking the [Wikipedia Page](http://en.wikipedia.org/wiki/Design_pattern) which gives a pretty reasonable answer. For those who don't want to make the jump, the first sentence sums it up pretty well.


> A design pattern in architecture and computer science is a formal way of documenting a solution to a design problem in a particular field of expertise.


So what I'm going to be explaining here is just a simple idea you can use in your pure data patches that can help solve a variety of problems. One of the major problems (at least in my opinion) with patching languages like PD is that things can get pretty cluttered and hard to follow. This may be how you like to work and it's certainly not a bad thing but I prefer to try to keep things neat and to compartmentalize sections of a patch in a logical fashion.

At this point I want to mention this article from [Creative Applications](http://www.creativeapplications.net/theory/patch-schematics-%E2%80%93-the-aesthetics-of-constraint-best-practices-theory/) which talks a lot about this and covers a bit of the same ground. I'm planning to go more in-depth but this is a really good article for getting your head around some of this.

Anyway, onto the first example. The design pattern I want to talk about is one that I call the Passthrough. The above article mentions daisy chaining patches together vertically, so the data output of one flows into the next and the passthrough is sort of a logical extension of this.

Each patch has a control bus and a data bus:-



	
  * Control messages flow through the patches and are routed into the correct patches using a route object with abstraction arguments.

	
  * Data output from a patch will flow into the main data bus and the messages will all be output from the outlet of the last patch




A Diagram will make this a bit easier to understand.




[![basic passthrough design](/a/2011-11-01-patch-a-day-2011-day-1-passthrough-design-pattern-part-1/passthrough-basic.png)](/a/2011-11-01-patch-a-day-2011-day-1-passthrough-design-pattern-part-1/passthrough-basic.png)
    Basic Passthrough example




The section on the left, surrounded by the black border, is the internals of the passthrough-abs abstraction. The right inlet/outlet is the control bus and the left inlet/outlet the data bus. Each abstraction has two arguments, one sets what the route object is looking for, the other is its output value. When a number is sent into the right inlet it will be sent to the route object in all of the abstractions. If the number sent matches the route argument then a bang will be sent out its inlet. This will cause the value in the symbol object to be sent out the data bus outlet. This data will pass through all the abstractions below the one triggered, but it will not affect them, eventually going to the list trim (to remove the symbol element at the front of the message) and then get printed.




If we send in multiple numbers then all the relevant abstractions will be triggered but the data will still only come out one outlet. This sort of pattern can help simplify the data routing of a patch. A simple extension to this is to add an "all" option that will output the value of every abstraction.




[![basic passthrough with all option](/a/2011-11-01-patch-a-day-2011-day-1-passthrough-design-pattern-part-1/passthrough-all.png)](/a/2011-11-01-patch-a-day-2011-day-1-passthrough-design-pattern-part-1/passthrough-all.png)
    Basic Passthrough with all option




This idea can be made more useful when combined with send objects as a good way of getting control data to where it's needed in a patch without having lots of patch chords all over the place. This is something I've seen used in the [SSSAD patch save module](http://puredata.hurleur.com/sujet-1531-sssad-save-module) and also the [rjlib libraries](https://github.com/rjdj/rjlib) and is originally what made me start thinking about this pattern.






![Passthrough with sends](/a/2011-11-01-patch-a-day-2011-day-1-passthrough-design-pattern-part-1/passthrough-send.png)






In this case, the s-passthrough-abs only has the control bus with the data bus having been replaced by a send object. The value that we are routing for is in this case being used both in the route object and the send object and we are also passing in the main patches $0 value as an argument. The $0 value is prefixed onto the send name so that it stays within the scope of just this patch. When a list in the form of "name value" is sent down the control bus it will be routed by the correct abstraction and the value will be sent to the corresponding receive object.




This may seem a little confusing to begin with, but imagine if this patch was part of a delay effect, and that instead of the names one, two, three and four, we instead had delay, feedback, mix and pan. We could use the abstractions to parse the input control messages and then send the values to the correct place in our patch. The section of the code dealing with the audio processing could be kept separate from this and would just need receive objects in the correct places. This would result in much neater and more logically structured code.




So I'm going to leave it there for tonight. I'm planning on spending the next two nights going into this in greater detail and with some more "real world" examples of how this can be pretty useful. After that I intend to get back into the algorithmic stuff so come back then if that's what you're after.
