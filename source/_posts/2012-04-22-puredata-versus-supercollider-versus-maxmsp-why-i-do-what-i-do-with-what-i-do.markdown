---
date: '2012-04-22 01:08:03'
layout: post
slug: puredata-versus-supercollider-versus-maxmsp-why-i-do-what-i-do-with-what-i-do
status: publish
title: PureData versus SuperCollider versus MaxMSP (Why I do what I do with what I
  do)
wordpress_id: '451'
categories:
- Musings
tags:
- Max/MSP
- pure data
- SuperCollider
---

So I got an interesting couple of questions in the comments for the last post. Many thanks to Joe for asking some good questions, as well as giving me a reason to get off my arse and write something. I'll repeat it here for everyones ease.


> _Hi_

I actually came across your blog/web page via various discussions on the Pure Data forum, which naturally I followed up and enjoy reading. However, I noticed in one of your earlier posts (on your own blog) the mention of SuperCollider. Naturally, since I came from the Pure Data forum, I’m a PD fan, like many out there. But reading your remarks about SC I’m interested to ask what is the difference between the two programs? Is it worthwhile (a personal choice of course) looking into both programs, or in fact is one enough and it’s all a matter of interfaces?

Oddly enough I notice that you do your ‘models’ in PD, probably because it’s freely available, or is that not correct.

Thanks for the posts, I’m trying to hang in there, but since there’s no real order easy to complicated etc I often find myself out of my own depth. I also have to say I sometimes try to understand the importance of certain ideas in connection with the results. But in the final picture who cares, it’s very interesting and I’m learning as I read your posts.

_Thanks in advance_.

Joe


I wrote a reply back in the comments but I think it's worth expanding on some of these questions with a bit more space to talk. Also on Thursday night at the London Hackspace I got to hear two members of the Birmingham Laptop Ensemble (_BiLE_) give a talk about the work they did and their thoughts on working with SuperCollider.

So, what do I feel the differences between SC and PD/Max are and why have I gone down the visual patching route.

Essentially, it does just boil down to being typed code versus visually patched code. Both have their strengths and weaknesses but really for me it's just that I prefer the do audio work in a visual language. I generally think that it can be much easier to see the flow of data through a patch, especially if you're not a programmer which is why I think that Pure Data has a much nicer learning curve that SuperCollider. That said, if you find yourself wanting to do anything involving dynamic object creation or needing large banks of voices then SC does make it much just because it is written code.

My advice? Try both. and as many other programs as you can. They're all good for something and ultimately, it's more about work flow than anything else in my opinion.

So as to why I do everything in PD and not Max/MSP, partly, yes the cost is one reason. Not because I don't think that Max is worth it because it really is, more just because I want to make the barrier for entry as low as possible.

The other reason is that I believe that there's less happening in PD, so the learning curve is again that bit shallower. You'll generally find yourself having to build abstractions for things that come as built in objects in Max but I think it's an advantage in some ways. The less objects you have to remember, the quicker you can get going and if you need something regularly then it's good practise to turn it into an abstraction.

I always liken the PD to Max view as being similar to C vs C++. PD and C are like a subset of Max and C++, they're more minimal, require more building and aren't as nice looking, but the language itself is pretty small and very versatile.

Make of that what you will.


