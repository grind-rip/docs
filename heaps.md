# Heaps

A **heap** is a binary tree in which each element has a key (or sometimes priority) that is less than (or greater than) the keys of its children. This property is called the *heap property* or *heap invariant*. Heaps can be used to implement priority queues.

Formally, a heap is an array for which `a[i] <= a[2*i+1]` and `a[i] <= a[2*i+2]` for all i for zero-based arrays. a[0] is always the smallest element (or largest for max-heaps). Heaps are useful data structures because their primary concern is maintaining the heap property. For this reason, problems which are only concerned with the smallest/largest value of a sequence are efficiently handled using by heaps.

* **Min heap**: In a min heap, the value of an element is the smallest for the element values of its subtree. The same property is true for all elements in the subtree.
* **Max heap**: In a max heap, the value of an element is the greatest for the element values of its subtree. The same property is true for all elements in the subtree.

It is possible to implement a heap as a linked list, where each element points to its parent and children, however, in practice, heaps are stored in arrays, with an implicit pointer structure determined by array indices. For zero-based arrays as in C, the rule is that a node at position `i` has children at positions `2*i+1` and `2*i+2`; in the other direction, a node at position `i` has a parent at position `(i-1)/2` (which rounds down in C). This is equivalent to storing a heap in an array by reading through the tree in breadth-first search order:

**NOTE**: A perfect binary tree, a binary tree in which all interior nodes have two children and all leaves have the same depth or same level (the level of a node defined as the number of edges or links from the root node to a node) has a depth of `log(n+1)-1`, where `n` is the number of nodes.

```
    0
   / \
  1   2
 / \ / \
3  4 5  6
```

becomes

```
0 1 2 3 4 5 6
```

## Heapification

If we are presented with an unsorted array, we can turn it into a heap more quickly than the O(nlog n) time required to do `n` `INSERT`s. The trick is to build the heap from the bottom up. This means starting with position `n − 1` and working back to position 0, so that when it comes time to fix the heap invariant at position `i`, we have already fixed it at all later positions. Bottom-up heapification is used in the heapsort algorithm, which first does bottom-up heapification in O(n) time and then repeatedly calls `DELETE-MAX` to extract the largest remaining element.

## Priority Queue

In a standard queue, elements leave the queue in the same order as they arrive (first in, first out). In a priority queue, elements leave the queue in order of decreasing priority: the `DEQUEUE` operation of a queue becomes a `DELETE-MIN` operation (or `DELETE-MAX`) of a priority queue, which removes and returns the highest-priority element regardless of when it was inserted. Priority queues are often used in operating system schedulers to determine which job to run next: a high-priority job runs before a low-priority job even if the low-priority job has been waiting longer.

In the context of algorithm interviews, heaps and priority queues can be treated as the same data structure. A heap is a useful data structure when it is necessary to repeatedly remove the object with the highest (or lowest) priority, or when insertions need to be interspersed with removals of the root node.

## Implementations

| Language | API                                                   |
| -------- | ----------------------------------------------------- |
| Python   | [`heapq`](https://docs.python.org/library/heapq.html) |

## Time Complexity

| Operation           | Big O     |
| ------------------- | --------- |
| Find Max/Min        | O(1)      |
| Insert              | O(log(n)) |
| Delete              | O(log(n)) |
| Heapify<sup>†</sup> | O(n)      |

<sup>†</sup>: Creates a heap out of a given array of elements. **NOTE**: A heap is **not** a sorted array, however, the heapsort algorithm can be used to sort an array that satisfies the heap property.

## Techniques

### Mention of k

If you see *kth smallest*, *k closest*, or *top k* mentioned in a question, it typically means the problem can be solved using a heap. The general approach to solving these problems involves maintaining a max- or min-heap of size k. The kth smallest value is the root of the max-heap. The kth largest value is the root of the min-heap. To retrieve all k smallest (or largest) elements, simply return the sorted heap.

**NOTE**: You can also use the quickselect algorithm to find the kth element in an unsorted array.

### k-way Merge

The k-way merge algorithm is a sequence merge algorithm that takes in k sorted lists, typically greater than two, and merges them into a single sorted list. It can be efficiently solved in O(nlog k) time using a heap, where n is the total number of elements for all k lists.

First, a heap is built using the first element of each list. Given that bottom-up heapification can be done in linear time, this has O(k) time complexity. Next, the smallest element is retrieved from the heap and the next element from the list from which the element was taken is inserted into the heap. This process continues until the heap is empty.

### Two Heaps

Using two heaps, a max-heap and a min-heap, we can retrieve the median of a dataset in constant time. The max-heap is of size n/2 (or n/2 + 1), containing elements less than or equal to the median. The min-heap is of size n/2, containing elements greater than the median. The heaps are balanced such that the max-heap only ever contains one more element than the min-heap. In order to maintain this balance, insertion into either heap that causes the heaps to become unbalanced is followed by a rebalancing wherein the root of the offending heap is removed and added to the other heap. If the heaps are balanced, the median can be calculated from the root of each heap. If the heaps are unbalanced (the max-heap contains one more element than the min-heap), the median is the root of the max-heap.
