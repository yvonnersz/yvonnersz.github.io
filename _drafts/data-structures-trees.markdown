## Trees

Trees are a data structure that is composed of nodes.

Structure of a tree:
- Root node
- Root node has 0+ child nodes
- Each child has 0+ child nodes

* A node is called a 'leaf node' if it has no children.

Trees and graphs are filled with ambiguous details and incorrect assumptions. So here are a few things to watch out for:

### Trees, Binary Trees, Binary Search Trees

Not all trees are binary trees!

Trees | Binary Trees | Binary Search Trees
-------------------------------------------
Suppose you have a tree to represent phone numbers, you will use a 10-ary tree with each node consisting of 10 children | Each node has up to children | All left descendents are less than or equal to all right descendents. * Could have duplicate values, clarify with interviewer!

### Balanced vs. Unbalanced

A balanced tree is 'balanced' enough to ensure O(log n) times for insert and find.

Common types of Balanced Trees:
- red-black trees
- AVL trees

### Binary Trees

#### Complete Binary Trees, Full Binary Trees, Perfect Binary Trees

It is rare in interviews and real life to have a perfect binary tree. Do not assume every binary tree is perfect!!! A perfect tree will have 2^k - 1 nodes, with k being the number of levels.

Complete | Full | Perfect
--------------------------
Every level is filled with the exception of the last node. Filled from left to right | Every node has 0 or 2 children | A binary tree that is complete AND full. 

#### Binary Tree Traversal

You should be comfortable implementing the following traversals.

in-order | pre-order | post-order
----------------------------------
visit left branch, current node, right branch |
visits current node before child nodes. Root is always the first node visited |
visits current node after child nodes. Root is always the last node visited.

#### Binary Heaps

min heap | max heap
--------------------
complete binary tree where each node is smaller than children. Root is the min element in the tree | max heaps are equivalent but the elements are in descending order.

Key operations for Min-Heaps:
1) Insert
- insert element at rightmost bottom
- bubble up the min element until it is in its correct place

2) Extract Min Element
- Remove element and swap with last element in heap
- Bubble down the element until it is in its correct place

## Tries

Tries are variants of an n-ary tree in which CHARACTERS are stored at each node. Each path down the tree represents a word. A * node is used to indicate complete words.

A trie can check if a string is a valid prefix in O(K) time where K is the length of a string.

A trie is used to store the entire English language for quicky prefix lookups. Many problems involving a list of words uses trie as an optimization.

## Graphs

Graphs are a collection of nodes with edges between them. 

Structure of a graph:
- could be directed (one-way street) or undirected (two-way street)
- isolated subgraphs or connected graph
- cyclic or acyclic

### Common Ways to Represent a Graph

1. Adjacency List.
- The most common way to represent a graph.
Every node stores a list of adjacent vertices.

2. Adjacency Matrices.
An NxN boolean matrix where N=number of nodes.

### Graph Search

#### Breadth First Search
- Preferred if we want to visit every node in the graph.
#### Depth First Search
- Preferred if we want to find the shortest path between two nodes.
#### Bidirectional Search
- Used to find the shortest path between a source and distination node. Operates by running simulataneous BFS from each node and when search collides, we have found a path.

BFS and DFS are the two most common ways to search a graph.