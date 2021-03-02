## Stacks

A stack uses last-in-first-out (LIFO).

Pros | Cons
----------------
Allows add/remove so it doesn't require shifting elements around | A stack does not offer constant time-access to the ith-item

One useful case to use stacks is for recursive algorithms. Sometimes you need to push temporary data onto a stack as you recurse, but remove them when you backtrack.

## Queue

A queue uses first-in-first-out (FIFO).

In breadth-first search, we use queue to store a list of nodes that we need to process. Each time we process a node, we add adjacent nodes to the back of the queue. This allows us to process nodes in the order they are viewed.

Stacks and queues can be implemented by using a linked-list.

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