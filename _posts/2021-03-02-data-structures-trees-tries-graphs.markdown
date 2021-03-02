---
layout: post
title:      "Data Structures: Trees, Tries, and Graphs"
date:       2021-03-02 21:41:00 +0000
permalink:  data-structures-trees-tries-graphs
categories: DSA
tags: data structures, DSA, trees, tries, graphs
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

Welcome back to the next of the DSA series! 

## Basics of a Tree

Trees are a data structure that is composed of nodes.

The structure of a tree looks like so:
- Root node
- Root node has 0+ child nodes
- Each child has 0+ child nodes
* A node is called a 'leaf node' if it has no children

When it comes to problems involving trees and/or graphs, the problems are filled with ambiguous details and incorrect assumptions. Some of the few things to watch out for are:
1. Tree vs. Binary Tree vs. Binary Search Tree
2. Balanced Tree vs. Unbalanced Tree - A 'balanced' tree is enough to ensure O(log n) time for insert and find, eg. red-black trees and AVL trees.

### Trees, Binary Trees, Binary Search Trees

Do NOT make the assumption that all trees are binary trees!

| Trees | Binary Trees | Binary Search Trees |
|----------|----------|----------|
| Suppose you have a tree to represent phone numbers, you will use a 10-ary tree with each node consisting of 10 children | Each node has up to two children | All left descendents are less than or equal to all right descendents. |

#### Binary Trees

Binary trees can be complete, full, or perfect. It is rare in interviews and real life to have a perfect binary tree so do NOT assume every binary tree is perfect!!! A perfect tree will have 2^k - 1 nodes, with k being the number of levels.

| Complete | Full | Perfect |
|----------|----------|----------|
| Every level is filled with the exception of the last node. Filled from left to right | Every node has 0 or 2 children | A binary tree that is complete AND full. |

#### Binary Tree Traversal

You should also be comfortable implementing the following traversals:

| in-order | pre-order | post-order |
|----------|----------|----------|
| Visits left branch, current node, right branch | Visits current node before child nodes. Root is always the first node visited | Visits current node after child nodes. Root is always the last node visited. |


## Basics of a Trie

Tries are variants of an n-ary tree in which CHARACTERS are stored at each node. Each path down the tree represents a word. A * node is used to indicate complete words. A trie is used to store the entire English language for quicky prefix lookups. Many problems involving a list of words uses trie as an optimization.

A trie can check if a string is a valid prefix in O(K) time where K is the length of a string.

## Basics of a Graph

Graphs are a collection of nodes with edges between them.

A graph:
- could be directed (one-way street) or undirected (two-way street)
- isolated subgraphs or connected graph
- cyclic or acyclic

The most common ways to represent a graph is by:

1. Adjacency List - where every node stores a list of adjacent vertices.
2. Adjacency Matrices - an NxN boolean matrix where N represents the number of nodes.

### Graph Search
1. Breadth First Search - Preferred if we want to visit every node in the graph.
2. Depth First Search - Preferred if we want to find the shortest path between two nodes.
3. Bidirection Search - Used to find the shortest path between a source and destination node. Operates by running simulataneous BFS from each node and when search collides, we have found a path.

BFS and DFS are the two most common ways to search a graph.