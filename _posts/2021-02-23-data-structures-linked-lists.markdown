---
layout: post
title:      "Data Structures: Linked Lists"
date:       2021-02-23 21:41:00 +0000
permalink:  data-structures-linked-lists
categories: DSA
tags: data structures, DSA, linked lists
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

## Basics of a Linked List

A linked list is a type of data structure that represents a sequence of nodes. The structure of a linked list consists of nodes, where each node is composed of data and a reference to the next node in the sequence.

The first node is called the head and the last node is called the tail. If a list is empty, the head is a null reference.

## Pros & Cons

Pros
1. Efficient insertion or removal of elements from the beginning of the list in constant time.
2. Nodes can be easily added/removed without reorganizing the entire data structure.

Cons
1. If you want to find the kth element in the list, you have to iterate over k elements.
2. Search operations are slow because random access is not allowed. You have to start from the first node.
3. Uses more memory than arrays because of the storage of pointers.

## Basic Operations and Complexities

| | Access | Search | Insertion | Deletion
|-------|-------|-------| ------- | ------- |
Time | O(n) | O(n) | O(1) | O(n)
Space | O(n)

## Types of Linked Lists:
1. Singly linked list: each node points to the next node.
2. Doubly linked list: each node points to the next and previous node.
3. Circular linked list: tail points to any other node before it, forming a loop.
