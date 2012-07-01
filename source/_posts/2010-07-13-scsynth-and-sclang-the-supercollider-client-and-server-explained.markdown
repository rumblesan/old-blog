---
date: '2010-07-13 13:50:08'
layout: post
slug: scsynth-and-sclang-the-supercollider-client-and-server-explained
status: publish
title: SCSynth and SCLang, The SuperCollider Client and Server explained...
categories:
- SuperCollider
tags:
- audio
- SuperCollider
comments: true
---

So I'm gradually browsing around the SuperCollider docs and finding where useful information is. One of the gems today has been [this page](http://supercollider.svn.sourceforge.net/viewvc/supercollider/trunk/common/build/Help/ServerArchitecture/ClientVsServer.html), which is a simple explanation of the client and server architecture.

This is something that I already sort of knew, but it's nice to find it in a simple and concise format. The SuperCollider documentation feels, to me at least, overly spread out and requiring far to much digging to get at what a beginner such as myself really needs. This is something I would like to address, but for the moment I feel I'm better off spending my time getting to grips with everything.

I will be starting up a separate page where I will be aggregating the useful and concise information I find. Hopefully it will prove useful to someone.

Anyway, a quick set of bullets about what this helps me understand about SuperCollider.

  * SCSynth doesn't care about the client. All it wants are OSC messages telling it what to do.

  * SCLang is simply a notepad with an interpreter with a network connection.

  * The actual SuperCollider language is simply a nice scripting language, based on SmallTalk that gets turned into OSC messages.

  * Anything can control the SCSynth, you just have to know what OSC messages to send it.

  * With a lib that does the interpreting and the OSC sending, You can create your own client.

Most of this is obvious but, again, I like concise information. I know that the Windows version of SuperCollider involves Psycollider in some way, I'm not yet sure how. Investigation needed, and will report back soon.

Guy
