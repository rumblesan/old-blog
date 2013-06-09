---
date: '2011-11-19 14:05:38'
layout: post
slug: patch-a-day-november-2011-day-17-data-structure-basics-part-4
status: publish
title: 'Patch-a-Day November 2011 Day 17: Data Structure Basics (part 4)'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
- polygons
comments: true
---

Drawing basic polygon shapes with the data structures is actually pretty easy it turns out. This is one of the things that had confused me the first time I looked at it but having spent the morning reading up, it turns out it's not that tricky. Have a look at the patch below first of all and then I'll run through what it does.

![Drawing polygons with data structures](/a/2011-11-19-patch-a-day-november-2011-day-17-data-structure-basics-part-4/drawing-polygons.png)

The top left section with the border is the contents of the template1 subpatch. There's a struct which defines eight float values, and a filledpolygon object with a bunch of arguments, most of which match values in the struct. Looking at the main patch, the collection of objects here will fill the data window with some number of struct1 objects. These objects will have random numbers for six of their eight values, with the other two, x and y, defaulting to zero.

The filled polygon object is what does all the work here. It tells PD that in the datawindow we want to draw a polygon with a certain number of points, a specific centre colour and a border with a specific colour and thickness. The argument order is :-

  1. Internal colour in RGB value. 60 here means 060 which translates to medium green

  2. Border colour in RGB. 1 here means very dark blue

  3. Border width in pixels

  4. List of points to join as (x,y) coordinates

In this patch, the coordinates are actually values stored in the struct. This means that any polygons drawn will have three edges, with points at (xa,xb), (ya,yb), (za,zb). Hit the message box with the 5 in it and have a look at the data window. You should see something like this,

![Polygons in data window](/a/2011-11-19-patch-a-day-november-2011-day-17-data-structure-basics-part-4/polygons-in-data-window.png)

Five green triangles with black borders, each of them representing a scalar in our data structure. The cool part about this is that if the patch is locked, when you can select one of the points on a triangle and move it around this will affect the data in the struct. Using this it's possible to create some quite interesting user interfaces and ways of more simply manipulating complex data sets. To see the values of the scalar that defines the shape, right click on it and select properties.

One last thing to point out. In the struct there are two float values called x and y. These are actually special and are used to set the overall position of the shape. Unlock the patch, select a shape and then move it around. This will only affect the x and y values, not the position values.

Hopefully you've grasped everything that's happened so far with the data structures, if not go back and have a read of the previous posts. I've actually found learning the polygon drawing stuff to be quite interesting so I might come back to it at some point. For the next couple of days though I want to start building a data storage and preset system. It's something that should end up being pretty useful and I've been meaning to get to it for a while.
