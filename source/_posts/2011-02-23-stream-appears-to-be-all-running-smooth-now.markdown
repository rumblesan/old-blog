---
date: '2011-02-23 08:12:15'
layout: post
slug: stream-appears-to-be-all-running-smooth-now
status: publish
title: Stream appears to be all running smooth now
comments: true
---

It seems that there was (perhaps still is) a bug that causes the Python process controlling PureData to crash out. PD will keep running but because all the new patch choosing and cross-fading is controlled by python it will then just keep playing the same patch indefinitely.

Initially I suspected it was something to do with updating the META info in the stream when a new patch is loaded but even after turning that off last night it still seemed to be happening. Thankfully the patch seems to have been running fine through last night and after turning proper logging back on (really shouldn't have turned it off) I think I'll be ready if it does reveal itself again.

So hopefully anybody who's been listening has heard at least something they like and want's to get involved. Just drop me an email if you do.
