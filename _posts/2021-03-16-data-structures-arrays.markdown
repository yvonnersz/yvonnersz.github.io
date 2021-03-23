---
layout: post
title:      "Data Structures: Arrays"
date:       2021-03-16 21:41:00 +0000
permalink:  data-structures-arrays
categories: DSA
tags: data structures, DSA, arrays
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

Hey all! I believe I have two data structures left to talk about so this will be the second last of the series. Today I will be talking about arrays.

The most basic of all data structures, an array stores data in memory for later use. Whenever you’d like to use an array, all you need are the desired indices and then you can access any of the data within. 

The structure of an array consists of:
- index, starting at 0
- elements

and looks like the following:

```
const numbers = [1, 2, 3, 4, 5];
```

## Basic Operations on Arrays
- Get -- returns the element at given index
- Insert -- inserts an element at given index
- Delete -- deletes an element at given index
- Size -- gets the total number of elements in an array

## Pros and Cons of Arrays

### Pros
- Store similar data types.
- Iterations in arrays runs faster compared to other data structures.
- Offers fast O(1) search if index is known.

### Cons
- Allocating more memory than you need can waste memory space.
- The cost of inserting and deleting is high because the elements of an array are stored in contiguous memory locations.

And that is it for arrays! Next week I will discuss hashes.

Until then,
Yvonne