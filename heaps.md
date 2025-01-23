# Heaps

A **heap** is a binary tree in which each element has a key (or sometimes priority) that is less than (or greater than) the keys of its children. This property is called the *heap property* or *heap invariant*. Heaps are used to implement priority queues.

* **Min heap**: In a min heap, the value of an element is the smallest for the element values of its subtree. The same property is true for all elements in the subtree.
* **Max heap**: In a max heap, the value of an element is the greatest for the element values of its subtree. The same property is true for all elements in the subtree.

It is possible to implement a heap as a linked list, where each element points to its parent and children, however, in practice, heaps are stored in arrays, with an implicit pointer structure determined by array indices. For zero-based arrays as in C, the rule is that a node at position `i` has children at positions `2*i+1` and `2*i+2`; in the other direction, a node at position `i` has a parent at position `(i-1)/2` (which rounds down in C). This is equivalent to storing a heap in an array by reading through the tree in breadth-first search order:

NOTE: A perfect binary tree, a binary tree in which all interior nodes have two children and all leaves have the same depth or same level (the level of a node defined as the number of edges or links from the root node to a node) has a depth of `log₂(n+1)-1`, where `n` is the number of nodes.

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

If we are presented with an unsorted array, we can turn it into a heap more quickly than the O(nlog n) time required to do `n` `INSERT`s. The trick is to build the heap from the bottom up. This means starting with position `n − 1` and working back to position 0, so that when it comes time to fix the heap invariant at position `i`, we have already fixed it at all later positions. Bottom-up heapification is used in the Heapsort algorithm, which first does bottom-up heapification in O(n) time and then repeatedly calls `DELETE-MAX` to extract the largest remaining element.

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

### Mention of K

If you see *Kth Largest* or *K Closest* being mentioned in the question, it is usually a signal that a heap can be used to solve the problem, such as in [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/).

If you require the top *K* elements use a min heap of size *K*. Iterate through each element, pushing it onto the heap. Whenever the heap size exceeds *K*, remove the minimum element. This will guarantee that you have the *Kth* largest elements in the heap.

### Top K Frequent Elements

### Two Heaps

### k-way Merge

## Resources

* [Heaps](http://www.cs.yale.edu/homes/aspnes/classes/223/notes.html#heaps), James Aspnes, Yale University
