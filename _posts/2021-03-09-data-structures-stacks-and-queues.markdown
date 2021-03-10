---
layout: post
title:      "Data Structures: Stacks, Queues, and Binary Heaps"
date:       2021-03-09 21:41:00 +0000
permalink:  data-structures-stacks-queues-binary-heaps
categories: DSA
tags: data structures, DSA, stacks, queues, binary heaps
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

Onto the third installment of the DSA series! Today, I'll be going over stacks, queues, and binary heaps.

## Stacks

A stack uses last-in-first-out (LIFO). One useful case to use stacks is for recursive algorithms. Sometimes you need to push temporary data onto a stack as you recurse, but remove them when you backtrack.

| Pros | Cons | 
|----------|----------|
| Allows add/remove so it doesn't require shifting elements around | A stack does not offer constant time-access to the ith-item |

## Queues

A queue uses first-in-first-out (FIFO). In breadth-first search, we use queue to store a list of nodes that we need to process. Each time we process a node, we add adjacent nodes to the back of the queue. This allows us to process nodes in the order they are viewed.

Stacks and queues can be implemented by using a linked-list.

## Binary Heaps

| min heap | max heap |
|----------|----------|
| Complete binary tree where each node is smaller than children. Root is the min element in the tree | Elements are in descending order. |

Here are some key operations for min-heaps:
1. Insert - insert element at rightmost bottom and bubble up the min element until it is in its correct place.
2. Extract the min element - remove element and swap with last element in heap, bubble down the element until it is in its correct place.