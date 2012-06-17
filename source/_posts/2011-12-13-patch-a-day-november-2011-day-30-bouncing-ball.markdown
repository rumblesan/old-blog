---
date: '2011-12-13 22:07:31'
layout: post
slug: patch-a-day-november-2011-day-30-bouncing-ball
status: publish
title: 'Patch-a-Day November 2011 Day 30: Bouncing Ball'
wordpress_id: '438'
categories:
- Patch-A-Day
- Pure Data
tags:
- equations
- maths
- modelling
- physics
---

For the last (very late) patch of the month I've decided not to do any more with the sequencer, but to go off on a bit of a tangent and create a simulation of a bouncing ball. It's not the most thorough physical model, and there are a couple of issues with it, but it gives a pretty good idea of how to go about taking mathematical equations and transferring them over to PD.

This patch will model dropping a ball from a chosen height and simulating how far it falls or rises within fractional lengths of time. The downwards direction gets changed to an upwards direction on the bounce but the co-efficient of elasticity (bounciness) can be changed to decide how much energy is lost when this happens.

I'll be using two equations here.

$ x = \tfrac{1}{2} at^2 + v_ot + x_o $

$ v = at + v_o $

These are two of the standard _suvat_ equations of motion. The first says that in a given amount of time $ t $, the position of an object will be its current position $ x_0 $ plus its velocity at the beginning of that period $ v_0 $ multiplied by the time, plus half its acceleration $ a $ multiplied by the time period squared.

The second says that the velocity of an object after time $ t $ is equal to its velocity at the start of that period $ v_0 $, plus its acceleration multiplied by time.

In the patch below I've broken the model down into three parts, one for the first equation, one for the second and then another part that checks when we've hit the bottom.

![Bouncing ball patch](/a/2011-12-13-patch-a-day-november-2011-day-30-bouncing-ball/bouncing-ball-patch.png)"

At the top there's the metro to run the patch and some setup. There are five variables here and I'm storing them in value objects.



	
  * The time period

	
  * The initial starting height

	
  * The current velocity

	
  * The acceleration due to gravity

	
  * The bounciness




It's worth pointing out here to remember that gravity is a negative value. This patch assumes that positive velocity is up, and as gravity is always pulling down it's negative.


This patch works with a relative time model instead of an absolute one. We're calculating the relative change in height since the last calculation, not the overall height since we started. This means that the velocity change also needs to be calculated relative to the last velocity. This is done by the left hand collection of objects which calculate the second equation. The section gets given the sample length and multiplies this by the acceleration to get the change in velocity. This gets added to the current velocity to give us the new value.

The middle section calculates the values for the first equation. It takes the current velocity and multiples this by the sample length then adds on the $ \tfrac{1}{2} at^2  $ part. It adds this to the current height value to get the new height value. When the patch starts, the velocity will be negative as the ball is travelling down, so decreasing the height.

The final part on the right hand side checks to see when the ball hits the ground. When the height is < 0 it reverses the velocity and multiplies it by the bouncyness. On the way back up the velocity will gradually decrease due to the effects of the negative gravity, and eventually it will stop and come back down. Assuming the bouncyness was a less that 1 value, the ball won't reach the same height, so the time until it hits will decrease.

There are a few issues with this model, mostly around the the section that checks for the bounce. The height will actually go negative for one iteration and only go back up again on the next calculation, after the velocity has been reversed. This can cause issues when the height gets very small and ideally there needs to be something smarter here to work it out.

Also if the sample time is too large then there is a lot of unstable behaviour so it's best to keep it to values around or below 0.1.

That said, this serves pretty well as an example so should teach you the basics of doing this sort of physical mechanical modelling.



But no1 that's it for Patch a Day month 2011. I'll make sure that all the example patches are in the repository for downloading and I'll leave it at that for now. There will be more PD stuff going up here, I'll make sure I;m better about it than last time.


