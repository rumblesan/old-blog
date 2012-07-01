---
date: '2011-11-22 22:20:49'
layout: post
slug: patch-a-day-november-2011-day-19-data-structure-basics-part-6
status: publish
title: 'Patch-a-Day November 2011 Day 19: Data Structure Basics (part 6)'
categories:
- Patch-A-Day
- Pure Data
tags:
- data structures
comments: true
---

Arrays in data structures are a little tricky it seems. Not too tricky, but they require a couple of extra objects and like symbols, it seems that you can't have a scalar with just arrays. This is because to modify an array field in a data structure scalar, you need to first create that scalar, and you can apparently only create a scalar using a float sent into an append object. If I've got this wrong then someone feel free to tell me.

Anyway, there are three new objects to use with data structure arrays, setsize and getsize should be pretty obvious, element maybe not so much. Have a look at the patch and I'll go through what's going on.

![Array manipulation in data structures](/a/2011-11-22-patch-a-day-november-2011-day-19-data-structure-basics-part-6/array-data-structure.png)

There are now two templates in the patch, each of which contains a struct. The first struct is called struct 1, it defines a float field called a, and an array field called array1. When defining an array it's necessary to give a third argument which is the name of a struct that will hold the array information. That second struct is held in the second template, is called testarray and has a single field, y.

Two things worth pointing out here. First, you can draw arrays in data windows like we did with the polygons, and like with the polygons, the field y is special. This is the value that will be used to draw the height of the polygon. This actually leads into the second point, the struct that's used to define the array is really just a normal struct, and so can store data in the same way. If you download the repository then there's a second patch called nested structures, where this second array has another float field and a symbol field. This should explain somewhat why the y field is special, because it's just the same as with regular polygons and data structures. In short, a data structure array is actually just an array of other nested data structures.

In the top right of the patch there's an append setup. This is just there so that when the patch loads a new scalar object is created in struct 1. This needs to be done because to operate on the array, we have to have an array in the first place.

Below this is the interesting stuff. First a pointer object is told to traverse the datawindow and then increment onto the first scalar element, the one created above. This goes to a setsize and getsize object which, unsurprisingly, set and get the size of the array. All arrays have a minimum of one scalar element.

The pointer also goes to the element object, which has arguments pointing it to the data structure struct1, and the field array1. This object takes a float in the left inlet and will send out a pointer to that position in the array. It plays the role of the until + counter setup we've previously used to get to specific scalars in a data structure. Bear in mind that you can only get a pointer to a scalar in the array that exists, so better increase the size of the field using setsize.

The pointer from element can be passed to set and get objects which work exactly like they do with normal data structure scalars.

Have a play and investigate, it's pretty much the best way to get a grasp of what's going on here. Once you have it however it should be pretty useful, especially with the preset patches that I will get to tomorrow.
