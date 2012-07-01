---
date: '2010-07-11 23:51:20'
layout: post
slug: devices-settings-strangeness
status: publish
title: Devices Settings Strangeness
categories:
- SuperCollider
tags:
- audio
- SuperCollider
comments: true
---

So I have SuperCollider working on my laptop, happily running under Windows 7. This in itself has been a bit of a learning curve, however, and this evening whilst helping a friend get his setup working, also on Win7, I discovered another confusing behaviour.

An important part of the whole process was getting the sound punted to the correct audio device. I have a reasonably decent USB ASIO sound card I use when I want good quality, but for just sitting around I find that the [ASIO4ALL](http://www.asio4all.com/) drivers are pretty good at giving me a low latency and good stability.

To get SC to use this, I found that its necessary to edit the **startup.sc** file again and un-comment a single line:-

_s.options.device_("ASIO : ASIO4ALL v2");_

This can also be sent to SC manually, before booting the server.

I'm yet to find the simple way to get SuperCollider to dump out what devices are available. I'm sure there is a way, but currently I have to see what it says when the server boots up. Mostly I'll be using ASIO4ALL untill I get something a bit more dedicated and probably *nix based.

With this in mind I set about helping a friend of mine get everything running on his machine, he'd had it throwing errors and was starting to look into Chuck and MiniAudicle because SC wasn't working. I decided that I'd help, because having someone learning at the same time as I was would be pretty helpful. He is also on Win7 and uses ASIO4ALL so I told him of the above tweak.

Turns out that ASIO4ALL isn't always for all. No sound from SC, or in fact anything else. Other sound drivers seemed to have issues as well, even after reverting to Microsoft Soundmapper devices, there was still no sound. At this point I felt fairly dis-heartened, thankfully my friend persevered, and we discovered a funny thing. When using the SoundMapper drivers, if there was no mic activated/plugged in, then SC would throw an error and not boot. as soon as the mic was there, it was all fine.

The upshot seems to be that you need to have some input channel going into SC for it to work. ASIO4ALL handles this itself, but if you're using the standard Microsoft Sound Mapper device, you need to make sure you have your laptop mic enabled, or a mic plugged in to your desktop.

I'm pretty sure there's work arounds and things to make this all simple but I don't know what they are yet. I'll dig around the help files and forums more.

Many thanks to Tonehog for figuring out what was going on with his system so I could put this up here. Hopefully someone will find it useful.
