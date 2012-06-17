---
date: '2010-07-04 23:19:21'
layout: post
slug: the-supercollider-learning-curve
status: publish
title: The SuperCollider learning curve....
wordpress_id: '7'
categories:
- SuperCollider
tags:
- audio
- problems
- Programming
- setup
- SuperCollider
---

...or "How I learnt to stop worrying and get SwingOSC working for SuperCollider on Windows 7"

I've been spending at least a couple of hours over the last day getting SuperCollider back up and running on my new laptop. Previously it was running fine on my, now dearly departed, WinXP laptop, but upon getting it installed on Windows 7, whenever I started it, I was greeted by a **"SwingOSC cannot be started"** error.

Most annoying..... Whilst this didn't stop SuperCollider from working, it did mean that without a fix, I wouldn't be able to control it from other programs using OSC. Also it's just the kind of thing that annoys me.

Some Googling later and it seemed that this was a reasonably regular occurrence over multiple OSes and configurations. Unfortunately, the answers ranged between, use an older version of SC, and installing other Linux packages, none of which worked for me. This was after having done various re-installs of the Java run-time and SC itself.

Thankfully, after a bit more googling I found [http://www.mcld.co.uk/supercollider/eee/](http://www.mcld.co.uk/supercollider/eee/) which, whilst being aimed at getting SuperCollider running on a Xandros netbook, had some useful info about editing the **startup.sc** file. Two extra lines in the relevant places and I have SwingOSC starting up fine.


    
    GUI.swing;
    SwingOSC.program = "SwingOSC.jar";
    g = SwingOSC.default;
    g.boot;
    



With that problem out the way, I can get on with the project at hand. A write up about my adventures making a big Granular Synthesis patch in SC. As well as other of my musical endeavours.

Guy
