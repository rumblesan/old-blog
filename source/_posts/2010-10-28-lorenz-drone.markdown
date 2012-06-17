---
date: '2010-10-28 21:37:21'
layout: post
slug: lorenz-drone
status: publish
title: Lorenz Drone
wordpress_id: '111'
categories:
- Music
- Pure Data
tags:
- algorithmic
- audio
- chaos theory
- FM synthesis
- Lorenz equations
- noise
---

Chatting with a friend the other day, he mentioned that he was currently bored at work waiting to be allowed access to the code he was supposed to be working on. I told him that he should design me an interesting system I could turn into a patch to make generative audio, since I knew that whilst at university he spent some time studying chaos theory and I figured he would know some interesting stuff. He pointed me towards the Lorenz Attractor as an interesting chaotic system that's very easy to implement in code. I've seen pictures of the 3 dimensional plot of the Lorenz equations and they do look pretty cool but I'd never thought to actually do anything with them.



![3D Lorenz Plot](http://en.wikipedia.org/wiki/Lorenz_equations)"

Of course, now I have this blog that I'm trying to keep updated with interesting, algorithmic noise stuff so it seemed like a pretty good chance to spend some time exploring what I could do with the equations.

The quick idea I had at work was to have multiple sets of the Lorenz equations with slightly different starting positions so that their chaotic nature and tendency for paths to drift greatly over time could be used. I also chose to have these control some FM synthesis, because even small changes to the modulation parameters and frequencies can have very noticeable effects on the sounds produced. The final thought was that having a filter present would help to give some more movement to the sounds and that if I was having to iterate through the values with a clock then that itself could be controlled for some interesting effects.

The equations themselves are:-



	
  * **dx/dt = sigma (y-x)**

	
  * **dy/dt = x(rho z) y**

	
  * ** ****dz/dt = xy beta z**


where the usual values are sigma = 10, rho = 28 and beta = 8/3 if you want to get the chaotic behavior, which we obviously do.

I decided to implement the whole thing in Pure Data because it's the language that I'm most comfortable with but I want to make the same patch again in SuperCollider to help contrast working with the two languages and as a learning exercise. Hopefully I'll have that up soon enough. First I had to create the Lorenz Equations in a patch. I'm trying to just stick to vanilla objects for both portability and learning reasons here so while the expr object available in PD-Extended would have made the resulting abstraction much neater to look at, I've pulled it apart into all the multiplies, adds and subtracts. Here is the abstraction with the equations.

![Lorenz Equations Abstraction](/a/2010-10-28-lorenz-drone/LorenzEquationsAbs.png)"

It's important to note that these equations calculate the change in position with respect to time, which means we have to pick a time period to use and we then have to add the calculated value onto the original value. It took me a little while to realise that I'd need to calculate the values in small increments because of this. My calculus skills have faded quite a bit in the last few years it seems. For this reason, once we have the values from the equations we have to multiply it by a small value (I chose 0.01 in the example patch) then add on the previous value. The abstraction I created does all of this and the creation arguments make it simple to use and tweak as needed.

This is the main bulk of the patch, other than this the only other abstraction is a patch for doing some basic FM synthesis. It's based on the simpleFM patch from the MaxMSP tutorials with three inputs, one for the carrier frequency, one that's the harmonicity value and one for the modulation amount. There are three Lorenz abstractions, two of which control the FM synths and a third that controls the resonance and frequency of a low pass filter, as well as having control over the speed of the metro that keeps the patch going.

![Lorenz Drone](/a/2010-10-28-lorenz-drone/LorenzDroneMain.png)"

I was hoping that this would help to add some movement to the sound and it exceeded my expectations massively. Listening to it the sound veers between harsh and smooth and the filter and speed variance means that it can crescendo and diminish with little warning. It's very rough around the edges but for a first attempt I'm very pleased. I fully expect that there will be improvements but for the moment I'll leave it.

The audio from it can be heard here

[soundcloud][http://soundcloud.com/tasteforreality/lorenzdrone](http://soundcloud.com/tasteforreality/lorenzdrone)[/soundcloud]

if the sound cloud player is working for you, otherwise grab it here, [Lorenz Drone Audio](http://www.rumblesan.com/wp-content/uploads/2010/10/LorenzDrone.mp3)

and the patch is available here for those that want it. [Lorenz Drone Patch](/a/2010-10-28-lorenz-drone/LorenzDrone.zip)

Guy
