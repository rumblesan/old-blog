---
date: '2010-11-15 23:13:22'
layout: post
slug: patch-a-day-month-day-15-rhythm-generator
status: publish
title: 'Patch-a-Day Month Day 15: Rhythm Generator'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- algorithmic
- drums
- generative
- patch-a-day
- pure data
- sequencing
comments: true
---

So day fifteen is here and I am officially half way through patch a day month. I'm actually quite looking forward to a rest after this but I'm learning a whole bunch so I can't complain. Tonight I've got something fairly complex straight off the bat but it's pretty useful so I'm going to show it off. It's a patch to generate dynamic and interesting rhythms and for me at least, the emphasis is on making complex kick drum patterns for rhythmic noise and heavy industrial music. As an aside, I should point out that a big influence on this has been the generative patches of [Chris McCormick](http://mccormick.cx), who you can fine here. I spent a bit of the weekend pulling apart his [Garage Acid Lab](http://mccormick.cx/projects/GarageAcidLab/) patches and they're excellent. Go check him out. Anyway, on to the kicks.



![Kick Drum Rhythm Generator](/a/2010-11-15-patch-a-day-month-day-15-rhythm-generator/15-RhythmGenerator.png)

So there's quite a bit going on here but it's pretty simple to break down. First things, have a look at the section on the left that starts at the trigger object by "Inner loop start" and ends down by the "Inner loop end" comment. We have an until object with a counter that gets started by a value of 6 which feeds into a tabread a bit further down. We also have the two tables on the right, timeprob1 and timeprob2. Forget for the moment there are two tables, we'll come back to them later, the important thing is that the tabread will read the values from these tables based on the output of the counter.

The tables have values between zero and one and when one is read out it's compared to a random number, also between zero and one. If the random number is smaller than the value from the table then the less than object sends out a 1 which the select object turns into a bang. This bang is used to stop the until if its still counting (thanks to the send and receive intstop objects) and it also makes the int object send out the counter value. The until here is responsible for sending out the bangs necessary to move through all these table values up to the maximum of 6 bangs needed. It will be stopped early once we have a hit, however, by the bang in its right inlet.

What this section basically gives us is a way of choosing values between zero and 5, but giving them a weighting of our choice. The final value in the table is greater than 1 so that if nothing else has previously matched then a value of 5 is always sent out. The two timeprob tables give us the ability to change the weighting of the numbers on the fly. The output from this section is then passed to a select statement which has a number of messages with values connected to it.

The idea with this patch is that we are creating rhythms by selecting time intervals as a number of 32nd notes. This is where the tables are being switched so that any time an interval of less than four 32nds is chosen, the weighting of probabilities moves towards the longer intervals and vice versa.

So now go right to the top of that column of objects where we have another bang, trigger, until setup. This time when we bang, the first thing that this all does is to send a message to the drumpattern array. This array is 32 elements long and we set all of them to zero to begin with. The bang will also trigger a message to store a value of zero in the int object to the right of all this. Once this is done we start the until going which will keep going until we tell it to stop because it was started with a bang. The until bangs will send the current stored value in the int out to use as an index when writing to the drumpattern array and also down to be added on to the next selected time interval. This means we have an increasing value as the intervals are added together which, when it reaches thirty-two or greater, will stop the main until.

Hopefully, you've managed to follow all of that. I suspect that in future for large complex patches such as these I should break it down into more pictures to make things more obvious, but not tonight. The result of all this is that the data written to the drumpattern array can be read out by the tabread and whenever there's a once we trigger the drum. I have plans to extend this to add a snare pattern linked with the kick and that may well be tomorrow's patch. We'll see later I suppose.

I'm attaching this patch because it's complex enough that I think it's worth while making it available.

[Rhythm Generator](/a/2010-11-15-patch-a-day-month-day-15-rhythm-generator/15-RhythmGenerator.zip)
