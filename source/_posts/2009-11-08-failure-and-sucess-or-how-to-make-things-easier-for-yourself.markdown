---
date: '2009-11-08 18:18:00'
layout: post
slug: failure-and-sucess-or-how-to-make-things-easier-for-yourself
status: publish
title: Failure and Sucess, or "How to make things easier for yourself"
categories:
- Pure Data
comments: true
---

It seems that creating your own cross compiling tool chain is somewhat tricky, especially if you're Windows based. It also seems that sometimes you're better of not trying to deal with the heavy stuff and getting bogged down in technical details. To shorten this lesson down, don't try to be more clever than you need to be when other people have kindly done it for you.

To this end, I have put on hold the idea of porting the DS Seq code to the Touch book. I still need to release the code for the sequencer since I feel that it was actually a reasonably decent piece of work, I might get it out every now and then again.

Instead, in a revelation that I must thank my friend Ben for, I realised that actually if all I want to do is control drum machines and synths via MIDI, I don't really have to be so low level about it and so I went looking for something a bit friendlier.

I have found that there is a version of Pure Data that has been modified specifically to work on Non-Floating point type processors such as the ARM chips found in iPods, many mobile phones, PDAs and mostly importantly, the Touch book. It is aptly titled Pure Data Anywhere (PDa) and can be found here http://pd-anywhere.sourceforge.net/

The process of getting it working was none too easy and I'm finding that this seems to be a pretty regular thing with Linux. Thanks to a bug that exists between the version of Tk that is in the Angstrom Package repository (version 8.4) and the version of XWindows on the touch book (version unsure currently but reasonably new) I wasn't able to get things to run.

Best part of two days later and having compiled and installed the newest versions of TCL and Tk from source (a learning experience) as well as the newest PDa and all is working.

Now I just need to learn how to use this crazy cousin of Max....
