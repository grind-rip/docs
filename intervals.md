# Intervals

Intervals, or array intervals, refer to a contiguous sequence of elements from an array, starting at one index and ending at another ([start, end]).

For example, given the array [1, 2, 3, 4, 5, 6], the interval [1, 3] would correspond to [2, 3, 4]. Intervals are typically represented as a list of lists: [[1, 3], [2, 4], [3, 5]].

## Techniques

Merging (combining overlapping intervals), intersection (finding where intervals overlap), insert, searching, non-overlapping.

### Sort the Array of Intervals

A common routine for interval problems is to sort the array of intervals by each interval's starting index.

### Check If Two Intervals Overlap

Two intervals, `a` and `b`, overlap if both of the following are true:
  1. The starting index of `a` is less than the ending index of `b`.
  2. The ending index of `a` is greater than the starting index of `b`.

  ```
   | --- a --- |
  a[0]       a[1]
                                     ✓ Overlap
         | --- b --- |
        b[0]       b[1]
  ```

  ```
                  | --- a --- |
                 a[0]        a[1]
                                     ⅹ Overlap (a[0] > b[1])
   | --- b --- |
  b[0]        b[1]
  ```

  ```
   | --- a --- |
  a[0]        a[1]
                                     ⅹ Overlap (b[0] > a[1])
                  | --- b --- |
                 b[0]        b[1]
  ```

```python
def overlap(a: tuple[int, int], b: tuple[int, int]) -> bool:
    return a[0] < b[1] and b[0] < a[1]
```

### Merge Two Intervals

In order to merge two intervals, `a` and `b`, the starting index of the merge interval is the smaller of the two starting indices of `a` and `b` and the ending index of the merge interval is the larger of the two ending indices of `a` and `b`.

```python
def merge(a: tuple[int, int], b: tuple[int, int]) -> tuple[int, int]:
    return (min(a[0], b[0]), max(a[1], b[1]))
```
