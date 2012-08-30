---
layout: post
title: "Programming is good for the soul"
date: 2012-08-30 22:00
comments: true
categories: [Programming]
---

In the past couple of months I've found I'm drifting away from my usual audio hacking and concentrating more on just programming for the sake of programming.
Speculation leads me to believe this is down to me having a chance to learn a bunch of cool new stuff and generally just wanting to be a better software engineer.
This is just a quick roundup of what I've been up to and the projects I've been creating.

[Diddy-VM](http://rumblesan.com/diddy-vm/)
--------

This is just a really basic Virtual Machine I wrote because I've not written one before. Eleven instructions, very basic memory model, no stack or registers and both Python and C implementations. I've written a simple assembler program so writing code for it can be done more easily but it's really very limited. Did the job as a learning exercise though.

[dotfiles](https://github.com/rumblesan/dotfiles)
---------

Not really a programming project, but I've started having an active go at improving my workflow and an important part of that was to sort out a good bash environment. Having it on github means I can easily share it between home, work and any remote servers and I can keep track of what I'm testing out with it.

[Cuttr](https://github.com/rumblesan/cuttr)
--------

Having gotten Glitchr working I decided to have a go at using Scala for some image processing. Cuttr will (once it's all finished) allow you do define mathematical functions and apply them to the image, either as a whole or as separate colour layers.
It started with the idea being just to algorithmically cut them up but extended somewhat once I realised how simple it was.

[Mandelbrot](https://github.com/rumblesan/mandelbrot)
------------

Every programmer should be able to render a Mandelbrot fractal, this is mine. Written in C, using SDL to display it and allows zooming and outputting to PNG. The code is actually reasonably neat as well!

[notes.txt](https://github.com/rumblesan/notes.txt)
-----------

Based along the same lines as the very minimal and very cool [todo.txt](http://todotxt.com/), this is a tiny command line app written in bash that allows me to quickly take notes. It's pretty much functioning at the moment but I'm wanting to extend it with the ability to upload the notes to Evernote as well, once I've figured out what the hell their API is doing.

So that's some of what's been consuming my time recently, there are a handful of other smaller projects but none are in the sort of state where they're of much interest. I do have some plans to start some SDL + OpenGL graphical experiments but there's a bunch of maths I need to relearn first. Better get my nose in some good books.

