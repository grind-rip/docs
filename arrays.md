# Arrays

An array is a block of contiguous memory of fixed size that holds one or more objects of a given type. An array is a highly efficient data structure, since access can be done in constant time (O(1)). This is due to the fact that the space required to hold an object is known, so accessing the location in memory that contains the ith object is a simple calculation (pointer to array + size of object * i). An array has poor performance for insertions and deletions, since this requires all elements at i + 1 to be shifted, a linear operation (O(n)).

## Arrays vs. Linked Lists

An important aspect of arrays is how they are differentiated from linked lists, another data structure for storing objects sequentially.

**Advantages**
* **Random access**: Arrays provide constant time (O(1)) access to any element using its index. A linked list must be traversed from its beginning.
* **Memory efficiency**: Arrays only store the values of their objects. However, arrays may be overprovisioned to prevent successive reallocations.
* **Cache-friendly**: Arrays have spatial locality, since elements are stored consecutively in memory. When an element is loaded into the CPU cache, neighboring elements are loaded as well, making subsequent access faster.

**Disadvantages**
* **Fixed size**: Arrays have a fixed size, which is specified when they are created. If the array needs to grow beyond this size, it must be reallocated and its elements copied to the new array.
* **Inefficient insertions/deletions**: Inserting an element into an array is an O(n) operation. The special case of inserting or deleting from the end can be done in constant time.
* **Memory allocation**: Arrays need contiguous memory blocks. In systems with limited or fragmented memory, finding a large enough continuous block can be challenging.

## Terminology

* **Subarray**: A contiguous subset of the array. All elements must be consecutive and maintain their original order. Ex. [1, 2, 3, 4, 5] -> [1, 2, 3]
* **Subsequence**: A sequence derived from deleting zero or more elements of the array. A subsequence does not need to be contiguous, but must maintain the original order of the elements. Ex. [1, 2, 3, 4, 5] -> [1, 3, 5]

**NOTE**: Be mindful about slicing or concatenating arrays in your code. Typically, slicing and concatenating arrays take O(n) time. Use start and end indices to demarcate a subarray/range where possible. This is true for slices in Python as well, as slicing a list (using [:]) creates a new list, essentially copying it.

## Time Complexity

| Operation | Big O |
| --------- | ----- |
| Access    | O(1)  |
| Search    | O(n)  |
| Insert    | O(n)  |
| Delete    | O(n)  |

**NOTE**: If the array is sorted, searching for an element can be achieved in logarithmic time O(log n) using binary search.
**NOTE**: Inserting and deleting to/from the end of an array can be done in constant time. For insertions, this requires that the array does not need to be reallocated.

## Techniques

It should be noted that these techniques can also be applied to strings, which are simply arrays of characters (character arrays).

### Sliding Window

The sliding window technique uses two pointers which maintain a "window" of elements that moves through an array or string in a specific way. The window can grow or shrink depending on certain conditions, but the pointers do not cross. This ensures that each value in the array is only accessed at most twice and the time complexity is still O(n). This is referred to as amortized analysis. The sliding window approach is particularly useful when you need to find a subarray or substring that meets certain criteria.

>Koan: Whenever you see a problem that involves finding a contiguous subarray or substring (size or the subarray/substring itself) always consider using sliding window.

**NOTE**: You should get **really** good at these types of problems.
