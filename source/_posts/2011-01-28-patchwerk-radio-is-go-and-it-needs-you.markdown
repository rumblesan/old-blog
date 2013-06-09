---
date: '2011-01-28 00:24:37'
layout: post
slug: patchwerk-radio-is-go-and-it-needs-you
status: publish
title: PatchWerk Radio is Go, and it needs YOU!!
categories:
- Music
- PatchWerk-Radio
- Pure Data
- Python
tags:
- noise
- PatchWerk Radio
- Programming
- pure data
comments: true
---

I know I said I'd write this a few days ago, but I decided I'd rather spend a little bit of extra time getting everything sorted so that everything would be up and running when I wanted to explain it all. The short summary is that Radio Drone is now known as PatchWerk Radio, it's all working and running off a VPS server, all the code and patches are on GitHub and, most importantly, you can listen to it right now by going to [http://radio.rumblesan.com/](http://radio.rumblesan.com/)

The website is bare, but you can listen to it from there, or turn your stream player of choice to [http://radio.rumblesan.com:8000/radio.ogg](http://radio.rumblesan.com:8000/radio.ogg)

The system is all run by a python script that starts up an instance of PureData and then dynamically loads generative music patches, letting each play for about ten minutes before fading over to the next. Currently there are only five patches I've built and there's still plenty of stuff I want to do with them, let alone all the other patches that will need to be made.

And this is why I'm going to be recruiting! All the patches currently on there are available on GitHub and I'm going to be using that as a central repository to hold everything. Tomorrow I'm going to write up a spec for how the audio patches interact with the master patch and how everything works (it's really pretty simple)  and then I'm going to start recruiting properly. I'll also be going back to doing regular patches, with the idea being that they will just get added to the main patch folder and help everything grow.

So, [PatchWerk-Radio](https://github.com/rumblesan/PatchWerk-Radio) is where you can get the code to run the server and [PatchWork-Patches](https://github.com/rumblesan/Radio-Patches). Tomorrow I'll explain the workings of it and then there's no excuse.
