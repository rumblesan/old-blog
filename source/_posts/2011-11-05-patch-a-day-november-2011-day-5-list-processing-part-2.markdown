---
date: '2011-11-05 17:57:06'
layout: post
slug: patch-a-day-november-2011-day-5-list-processing-part-2
status: publish
title: 'Patch-a-Day November 2011 Day 5: List Processing (part 2)'
wordpress_id: '333'
categories:
- Patch-A-Day
- Pure Data
tags:
- list processing
---

Yesterdays post started with some basic list processing in pure data, the patches showed how you could serialise and interleave the lists but there were a few problems and also some missing functionality that we're after. Specifically :-



	
  * when we interleave lists, if one is shorter than the other then the extra elements are still appended


	
    * **a b c** and **1 2 3 4** would become **a 1 b 2 c 3 4**


	
  * we can have larger sub elements


	
    * **a b c d e f** with **1 2 3** could become **a b 1 c d 2 e f 3**



Both of these problems can be easily solved by checking for the output of the list split objects right hand outlet. This will only output anything when the input list is shorter than the number of elements we want to be splitting. So for example, if we have list split 2 and we send in a single item list, that single item will be output from the right outlet. Importantly, if we're splitting single elements off the list and we send in an empty list (same as a bang remember) then we get a bang from this output. This is a much neater way to check when all our elements have been split out. The below patches shows how this works and how we can extend it to easily deal with multi item elements in the list.

![Better list serialising](/a/2011-11-05-patch-a-day-november-2011-day-5-list-processing-part-2/better-list-serialising.png)"

Look at the left hand section where we check the outlet, bang the done output and then send the value to the main output unless it's a bang. Importantly here, if we were dividing the list up into 2 item elements and we had an odd number of elements, the final element would be output from this right outlet. We still want that appended onto the end of our data, but we also still need to trigger that we're done. The easiest way to do this is to say we're done as soon as we have output from this outlet and just to send any values that aren't bangs onwards.

On the right hand side the trigger for the recursion has moved down to after the bang routing and we're also resetting the temporary list store. This is essentially to stop us from running into some tricky timing situations. I advise playing about with this code and seeing what happens if you switch around the order in which the right outlets value gets sent to the output and the resetting of that temp list store. This section can easily deal with any size of elements and any size list input. For a very small selection of objects it's deceptively tricky.

So now we have that sorted, lets get back to our more complex list interleaving.

![Element interleaving](/a/2011-11-05-patch-a-day-november-2011-day-5-list-processing-part-2/element-interleaving.png)"

This looks much the same as the last interleaving patch, the difference here is how it checks when it's done. The two sections that send out the list elements can now deal with arbitrary sized elements and when they've sent out all their elements they will just keep sending out bangs. The section at the bottom that joins the two lists is now responsible for sending the done message and it does this when the output of the list append is a bang. The thing to remember again is that a bang is like an empty list so, if one of the element splitters runs out and starts sending bangs, but the other is still sending elements, then the output of the list append will still be a list item. As soon as both have finished, the output from the append will be a bang and we trigger that we're done. This means that if we gave it **1 2 3 4 5 6 7 8 9** and **a b c d e f g h**, specifying 2 items to an element for the first list and 3 to an element for the second, we get **1 2 a b c 3 4 d e f 5 6 g h 7 8 9**, exactly what we want!

We now have a patch that can interleave two lists and deal with differently sized elements and different length lists. This is is one of the things at which I personally feel Pure Data isn't that great, any other language this would be a few lines of code, but here it's become something of a major effort and there are all sorts of timing issues to contend with. It's one of the trade offs we make for using a graphical patching language  unfortunately, but once you understand it, it's not as daunting as it first seems.

It may also seem confusing at this point why I'm actually building these list manipulation patches, if you read the links in the last post it should hopefully be clear, but if not I''ll hopefully answer all your questions tomorrow night. Come back then for some answer.
