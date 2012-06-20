---
date: '2010-02-20 15:01:00'
layout: post
slug: clusters-non-musical-ones-at-that-for-the-moment
status: publish
title: Clusters, non musical ones at that (for the moment)
wordpress_id: '58'
categories:
- Povray
- Programming
- Python
tags:
- cluster
- Povray
- Programming
comments: true
---

So the other week I started getting a bit burnt out on music and decided a change was in order, at least for a while. So I went and started playing around with my friend [PovRay](http://povray.org/) again, a free ray tracing program.

After getting to grips with it and realising that, thanks to a lot of new maths knowledge since I last used it 5 or so years ago, it was an awful lot of fun. The only issue is that I very quickly started creating images that took quite a while to render. This event quite happily coincided with my finding a source of surprisingly cheap rack-mount servers so I decided that the obvious thing to do would be to make a render farm!!

I realise that this is perhaps overkill, and the answer is really to just make images at smaller resolutions and put up with the time it takes, but I like the idea of having a big bank of servers that are my own, and if I want to do animations (which I do, more on this later) then a bank of servers is a good investment.

The plan is now very much in motion and sitting on the coffee table in front of me I have 5 2U rack mount servers, each with an AMD64 3000+ CPU and a gig of RAM. Not the highest spec machines but cheap and useful. These are now encased in a nice 10U ABS plastic rack case and looking very swish. After some failed attempts to install Ubuntu Server on them the other night (Always MD5 check your ISO files, or at least the important ones) I'll be re attempting later today. I also have a LinkSys WRT54G router with the open [DD-WRT](http://www.dd-wrt.com/site/index) firmware. this will be used to hook the cluster up to my home network with some [client mode](http://www.dd-wrt.com/wiki/index.php/Client_Mode_Wireless) magic.

Ideally I'd like to have another box to sit on the subnet with the cluster to act as a master task giver and file storage area but I've not yet found a suitable device for a cheap price. I may well pick-up a broken net-book soonish however.

As far as how I'm going to split the tasks up, there's really not going to be much magic. Povray can be run via the command line and has the useful ability to only render part of an image.
This means that a simple python script can SCP the .POV files over to each node in the cluster, get them to render a section, SCP the section of the image back and put the image together once all the pieces are done. With animations the process is even simpler because individual frames can be rendered by each machine, meaning the script doesn't have to go about splitting and joining images.

Python scripting will start properly next week, for the moment I'll just have my work cut out for me getting Ubuntu installed and checking all the servers work. Unfortunately in the process of delivery, DHL gave the package a hefty bump and some of the cases were warped where the handles on the front dented. A bit annoying but not too much of an issue.

As you can see, everything looks fine from the front.


[![](http://3.bp.blogspot.com/_AvMGnA-mpis/S3_oNkSbkbI/AAAAAAAAACE/--OINm3r71c/s400/DSCN4739.JPG)](http://3.bp.blogspot.com/_AvMGnA-mpis/S3_oNkSbkbI/AAAAAAAAACE/--OINm3r71c/s1600-h/DSCN4739.JPG)


The bits of tape on the front are the node names, Horse-Head, Crab, Eagle, Pelican and Tarantula. In keeping with my Star themed network naming convention I named them all after different nebulae. It seemed appropriate.

Guy
