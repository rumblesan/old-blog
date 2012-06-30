---
layout: post
title: "Glitchr up and running"
date: 2012-06-30 23:14
comments: true
categories: [Glitch, Art]
---

A little while ago I wrote a python script that opened up JPEG files, parsed the binary data, messed around with it a bit and gave you back some really interestingly glitched images. I'd intended to do some other things with it but it just got put on the back burner.

I resurrected it about a week ago and thanks to Michael Helmick's [TumblPy](https://github.com/michaelhelmick/python-tumblpy) library I've now got it pulling images from and then re-uploading to Tumblr.

You can check out the images at [rumblesan.tumblr.com](http://rumblesan.tumblr.com/) and the project site is at [rumblesan.com/glitchr](http://rumblesan.com/glitchr)

I want to improve the way the glitching happens at the moment. Currently it's just the quantization tables that get played with but there's plenty of other things that can be done. Also it tends to be quite aggresive glitching and I'd like to make it a bit subtler.

Something to play with either way. At least now it's running it'll be easier to mess around with

