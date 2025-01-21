# Linked Lists

A linked list is a data structure where elements (often called nodes) are connected in a sequence, with each node containing both data and a reference (or "pointer") to the next node in the sequence. A linked list is used to represent sequential data, however, unlike arrays, its objects are not contiguous in memory.

Each node has:
1. `data`: The value being stored
2. `next`: A reference pointing to the next node
3. `prev` (Optional): A reference pointing to the previous node (for doubly linked lists)

The first node in the list is referred to as the *head*. Its `prev` points to null (for doubly linked lists) denoting the start of the list. The last node in the list is referred to as the *tail*. Its `next` points to null denoting the end of the list. For circular linked lists, there is no *head* or *tail*, since all nodes point to a next (or previous) node.

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

**Iterate over a linked list**
A basic operation requiring traversal from head to tail.

**Reverse a linked list**
This should be done in-place by adjusting node pointers.

**Two pointers**
Two pointers are commonly used for finding the middle node, finding the kth node, and cycle detection.

**Find the middle node**
Using two pointers, `fast` is incremented by 2 and `slow` is incremented by 1. When `fast` reaches the end of the linked list, `slow` is at the middle node.

**Find the kth node**
Using two pointers, `p1` is k nodes ahead of `p2`. When incremented together, `p2` is always k nodes behind `p1`.

**Cycle detection**
Using two pointers, `fast` is incremented by 2 and `slow` is incremented by 1. If `fast` and `slow` point to the same node before reaching the end of the linked list, the linked list has a cycle. This is Floyd's cycle-finding algorithm (tortoise and hare algorithm).

**Merge two or more sorted linked lists**
A common operation that involves comparing and linking nodes from multiple sorted lists.

**Sentinel/dummy nodes**
Using a sentinel/dummy node at the head/tail of the linked list may help when operations must be performed on the head/tail. This removes the need for performing conditional checks for null pointers.
