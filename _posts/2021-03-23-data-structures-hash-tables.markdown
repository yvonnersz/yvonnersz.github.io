---
layout: post
title:      "Data Structures: Hash Tables"
date:       2021-03-23 21:41:00 +0000
permalink:  data-structures-hash-tables
categories: DSA
tags: data structures, DSA, hash tables
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

## Basics of Hash Tables

Hash tables are data structures that maps key/value pairs for highly efficient lookups. In a hash table, data is stored in an array format, where each data value has its own unique index (key), coupled with a value. Access of data becomes very fast if we know the index of the desired data, which is why hash tables are often used for their O(1) constant time lookup. 

If the number of collisions are high, the worst case runtime is O(N), where N is the number of keys.

We can also implement hash tables as a balanced binary search tree, which will give us an O(log N) lookup time. The advantage of this is potentially using less space.

## Basic Operations 
- Search -- search an element in a hash table
- Insert -- inserts an element in a hash table
- Delete -- delete an element from a hash table

And I believe that's the end of the data structure series!

Until next time,
Yvonne