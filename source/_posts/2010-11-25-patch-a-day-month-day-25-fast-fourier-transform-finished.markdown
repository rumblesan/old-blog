---
date: '2010-11-25 22:56:04'
layout: post
slug: patch-a-day-month-day-25-fast-fourier-transform-finished
status: publish
title: 'Patch-a-Day Month Day 25: Fast Fourier Transform Finished'
wordpress_id: '210'
categories:
- Music
- Patch-A-Day
- Pure Data
tags:
- audio
- FFT
- lessons
- maths
- patch-a-day
- pure data
comments: true
---

Right, this will be the last post in patch-a-day month detailing the ins and outs of the Fourier transform. After this I'm just going to carry on building the patches assuming you can deal with FFT in Pure Data, feel free to ask questions if there are still things that aren't clear tho.

I'm planning on collecting the content of these articles into one big "FFT How-To" because I feel that the other FFT articles around the internet don't get the right balance between the maths, the audio and how it actually works. Maybe I'm wrong and I won't write anything useful but we'll see.



Last night I mentioned that we would want to change the block size and overlap the Hanning windows and tonight I'm actually going to show how to do that. Pure Data itself actually handles both of the above things itself with very little effort from us which is nice. To change the blocksize we use for the FFT we actually have to change the whole blocksize being used, which sounds tricky, but actually is done using the block~ object. We create a subpatch and put a block~ object inside and with the first argument we can specify what we want the blocksize to be, bearing in mind it has to be a power of 2. I'm going to be using 512 here.

The block object is also responsible for doing the envelope overlapping and we can specify how many envelopes we want to have with the second argument in the block object. I'll be using 4 overlapping envelopes in this patch. Once we have a subpatch with the block, we just move the Fourier transform stuff into the subpatch and everything works.

![Fourier Analysis Subpatch with larger blocksize and enveloping](/a/2010-11-25-patch-a-day-month-day-25-fast-fourier-transform-finished/25-FFTAnlysisSubpatch.png)"

So there are three things to point out here, one is that we're actually just doing the inverse transform straight away. I'm not doing any processing of the Fourier data, just turning it straight back into audio for the moment.

The second is that the output is also being enveloped again.

The third is that there's a divide by 768 there which possibly isn't expected. This is there to normalise the output of the transform and also to counteract the increase due to the overlapping of the envelopes. The output of the Transform will always have a gain increase equal to the blocksize. in this case we need to divide by 512 because that's our blocksize. With four overlapping envelopes we have an increase in gain 1.5, so to normalise the outgoing audio back to the same volume as the incoming we can just divide by (512 * 1.5) = 768.

If you want to see that the output is the same as the input then here is the full patch.

![Complete FFT example patch](/a/2010-11-25-patch-a-day-month-day-25-fast-fourier-transform-finished/25-FFTFinished.png)"

It's actually possible here to see the delay caused by doing the transform if you look at the offset between the waves in the bottom panes.

I'll leave that there for tonight so that these three posts stand alone as a tutorial of sorts. Tomorrow I'll get to some of the cool things you can do with this and hopefully we can just hit the ground running.
