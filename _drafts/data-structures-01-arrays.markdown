The most basic of all data structures, an array stores data in memory for later use. An array is the simplest and most widely used data structure. Whenever you’d like to use the array, all you need are the desired indices, and you can access any of the data within.

```
const numbers = [1, 2, 3, 4, 5];
```

The structure of an array consists of:
- index
- elements

## Basic Operations on Arrays
- Get -- returns the element at given index
- Insert -- inserts an element at given index
- Delete -- deletes an element at given index
- Size -- gets the total number of elements in an array

## Advantages and Disadvantages of Using Arrays

### Pros
- Store similar data types.
- Iterations in arrays runs faster compared to other data structures.
- Offers fast O(1) search if index is known.

### Cons

- Allocating more memory than you need can waste memory space.
- The cost of inserting and deleting is high because the elements of an array are stored in contiguous memory locations.