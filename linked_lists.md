# Linked Lists

A linked list is a data structure where elements (often called nodes) are connected in a sequence, with each node containing both data and a reference (or "pointer") to the next node in the sequence. A linked list is used to represent sequential data, however, unlike arrays, its objects are not contiguous in memory.

Each node has:
1. `data`: The value being stored
2. `next`: A reference pointing to the next node
3. `prev` (Optional): A reference pointing to the previous node (for doubly linked lists)

The first node in the list is referred to as the *head*. Its `prev` points to null (for doubly linked lists) denoting the start of the list. The last node in the list is referred to as the *tail*. Its `next` points to null denoting the end of the list. For circular linked lists, there is no *head* or *tail*, since all nodes point to a next (or previous) node.

Linked lists are among the simplest data structures after arrays. While not efficient for many purposes, they excel in specialized applications like stacks, queues, and deques, since insertions and deletions next to a known element can be done in O(1) time.

## Linked Lists vs. Arrays

An important aspect of linked lists is how they are differentiated from arrays, another data structure for storing objects sequentially.

**Advantages**
* **Dynamic size**: Can grow or shrink, whereas arrays must be reallocated.
* **Efficient insertions/deletions**: Inserting a node at the beginning and removing a node from the end is an O(1) operation.
* **Memory efficiency**: Memory is allocated as-needed. Arrays may be overprovisioned to prevent successive reallocations.

**Disadvantages**
* **No random access**: You cannot index into a linked list, as is the case with arrays. Linked lists must be traversed from the beginning requiring O(n) time complexity.
* **Extra memory for pointers**: Though small, the pointer to the next/prev node must be stored with its value.
* **Not cache-friendly**: Nodes do not share spatial locality and therefore may not be loaded from main memory into the CPU cache.

## Time Complexity

| Operation          | Big O |
| ------------------ | ----- |
| Access             | O(n)  |
| Search             | O(n)  |
| Insert<sup>†</sup> | O(1)  |
| Delete<sup>†</sup> | O(1)  |

<sup>†</sup>: Assumes you have a reference to the insert/delete location.

## Types of Linked Lists

There are three common types of linked lists:
* **Singly linked list**: Each node points to the next node and the last node points to null.
* **Doubly linked list**: Each node points to the next node and the previous node. `prev` of the first and `next` of the last node point to null.
* **Circular linked list**: A singly linked list where the last node points back to the first node.

## Implementations

Python's built-in [`list`](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) type actually uses dynamic arrays (not linked lists) under the hood. The [`collections.deque`](https://docs.python.org/3/library/collections.html#collections.deque) class uses a doubly-linked list implementation, however.

## Techniques

### Iterate Over a Linked List

Starting from head, update the current node to be the next node until the current node is null.

```python
curr = head
while curr:
    ...
    curr = curr.next
```

### Reverse a Linked List

This can be done in-place by adjusting node pointers:
1. Store the current node's reference to next.
2. Update the current node's next to be the previous node.
3. Update the previous node to be the current node.
4. Update the current node to be the next node (stored in 1).

### Two Pointers

Two pointers are commonly used for finding the middle node, finding the kth node, and cycle detection.

### Find the Middle Node

Using two pointers, `fast` is advanced by 2 and `slow` is advanced by 1. When `fast` reaches the end of the linked list, `slow` is at the middle node.

### Find the kth Node

Using two pointers, `p1` is k nodes ahead of `p2`. When advanced together, `p2` is always k nodes behind `p1`.

### Cycle Detection

Using two pointers, `fast` is advanced by 2 and `slow` is advanced by 1. If `fast` and `slow` point to the same node before reaching the end of the linked list, the linked list has a cycle. This is Floyd's cycle-finding algorithm (tortoise and hare algorithm).

### Merge Two Sorted Linked Lists

This can be done in-place by adjusting node pointers and using a head sentinel node:
0. Start by instantiating a head sentinel node.
1. Compare the heads of the two lists.
2. Update the current node's next to be the lesser of the two.
3. Update the head of the list from which the node was taken.
4. Update the current node in the merged list.
5. If either of the lists still have nodes, attached to the end of the merged list.

### Merge k Sorted Linked Lists

Merging k sorted linked lists can be done in O(nlog k) time complexity and O(k) space complexity using a heap (priority queue).
1. Build a heap using the head of each list.
2. For each selection, remove the smallest element from the heap, adding it to the merged list.
3. Insert the head of the list from which the node was taken into the heap.

### Sentinel/Dummy Node

Using a sentinel/dummy node at the head/tail of the linked list may help when operations must be performed on the head/tail. This removes the need for performing conditional checks for null pointers.
