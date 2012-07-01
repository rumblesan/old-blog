---
date: '2011-01-10 17:32:44'
layout: post
slug: radio-drone-taking-shape
status: publish
title: Radio Drone taking shape
categories:
- Programming
- Pure Data
- Python
comments: true
---

I'm definitely going to have to come up with a better name than "Radio Drone". It sells the whole thing a bit short I think. I'll carry on using it as the working name for this project until it's actually ready to publicly unveil but a re-branding is needed.

Anyway, my weekend was taken up with plenty of programming and there is some amount of structure appearing from out of the murk. I have a new [repository up on GitHub](https://github.com/rumblesan/Radio-PD) that holds the code and I'm managing to get back into Python despite the rust that develops in the six month breaks I seem to have between using it.



So far I've modified the PyPD library so that all communication happens over one port that can be set when Pure Data starts up. Previously the use of the netreceive object meant that the communication port had to be fixed, which was a bit of a speed bump. Modifying the interface abstraction to use the netclient object from the pd-extended MaxLib and a bit of a change to the Python has fixed this.

For the foreseeable I'm also going to be sticking with my plan to have a master patch that does all the cross fading and streaming. Unless testing shows that this is problematic, which I don't expect but that's why I'll be testing.

Lastly, everything will be connected using Jack. It's solid, easy to use and means that the individual patches don't have to have any extra stuff other than the python interface abstraction. I've written a python class that can start the jack daemon and wraps the command line binaries so that Python can more easily connect and organise programs. The PyJack library seemed a little overkill for what I wanted but may well still be used eventually but for the moment I'm trying to keep things simple.

There's still plenty to implement and I need to do lots of testing to make sure it's solid but it's out in the open now and being worked on. I suppose that I'm going to have to start looking into the server side of it soon and see if I can comfortable get this thing running on a Virtual Server. If push comes to shove I suppose I can just rent a proper dedicated box but I'd like to keep costs down for the moment.

In other news, I realise that I didn't get a patch made for Friday like I said I would. I feel that this is kind of offsetting that but at the same time I feel a bit bad. I'll try to get something out in the next couple of days to make up for it. I actually received a copy of [this book on Music and Mathematics](http://www.amazon.co.uk/gp/product/0199298939/ref=oss_product) today so I'll have a look through it later and might try and pull something from it to use.
