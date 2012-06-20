---
date: '2009-10-30 01:38:00'
layout: post
slug: what-the-hell-am-i-doing-again
status: publish
title: What the hell am I doing again
wordpress_id: '49'
categories:
- Music
- NDS Homebrew
comments: true
---

Well currently I'm trying to work out the easiest way to port the code from the DS Seq to the touchbook. That's the big project for the moment, along with all the other musical activities I seem to have. Essentially the DS specific stuff in the code consists of the timers and the graphics.

Everything else is fairly well abstracted so should just invole some slight rewriting to make it bigger and better. C++ is C++ after all and I actually feel I put the concepts of Object Orientated programming into practise pretty well.

The timers and graphics are a problem tho....

The DS has nice interrupt timers that are very accurate and very fast. I could have a timer running at 2000Hz plus and it would do exactly what I wanted. Turns out that normal computers don't do that and I'm going to be having to do Real Time Clock shenanigans. Should be reasonably easy however. Again, the timers were abstracted well enough that I just need to trigger a single command. The timing itself is just a small, all be it vital, part.

The graphics was always going to be a bigger challenge. So far SDL looks like the best candidate, it's not too tricky, it,s multi platform, the touchbook comes with the libs (perhaps not all but its still a good sign) and it seems to be the most like the DS graphics layout that I've found so far.

So the next plan is to get learning. Oh and also sort out a git hub/google code repository for this. I figure if I just open it up from the start then it will make working on it from anywhere that much easier.
