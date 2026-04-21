# Sorting & Searching Algorithms

## 1. Searching Algorithms

Finding an element within a massive dataset efficiently is foundational to database operations.

| Algorithm | Method Overview | Time Complexity (Worst/Avg) | Notes |
|-----------|-----------------|-----------------------------|-------|
| **Linear Search** | Checks sequentially node by node. | $O(n)$ | Mandatory for fully unsorted datasets. |
| **Binary Search** | Assumes the data is **sorted**. Checks the middle point repeatedly, cutting search bounds by half each iteration. | $O(\log n)$ | Standard application for all sorted arrays. |

### Binary Search Details & Patterns
While fundamentally simple (`mid = left + (right - left) / 2`), Binary Search is notorious for frustrating edge cases around `>=` vs `>` and updating pointers `left = mid + 1` vs `left = mid`.
- **Finding Exact Target**: standard strict BS structure.
- **Finding First / Last Instance (Lower/Upper Bound)**: Useful when duplicates exist.
- **Searching Rotated Arrays**: Requires identifying which half of the pivot is strictly sorted before jumping.
- **Searching the "Answer Space" (Binary Search on Answer)**: Many optimization problems (e.g. "Find the minimum maximum capacity") can be explicitly solved by guessing an answer using Binary Search across a mathematical constraint checker.

## 2. Sorting Algorithms

Sorting inherently structures memory, dramatically speeding up downstream tasks (like searching).

### Comparison Sorts (Theoretical Bound: $O(n \log n)$)

1. **Bubble Sort / Insertion Sort / Selection Sort**
   - **Time**: $O(n^2)$
   - **Space**: $O(1)$
   - Usage: Almost strictly educational. Insertion sort technically acts extremely fast if the dataset is already *nearly fully sorted*.

2. **Merge Sort**
   - **Time**: $O(n \log n)$ strict bound always.
   - **Space**: $O(n)$ auxiliary array.
   - **Stability**: Yes (keeps relative duplicates in sequence).
   - Concept: Divide physically the array linearly into halves repeatedly. Merge them concurrently upwards checking conditions. (Highly preferred internally for sorting Linked Lists).

3. **Quick Sort**
   - **Time**: $O(n \log n)$ physically extremely fast avg. $O(n^2)$ worst case.
   - **Space**: $O(\log n)$ call stack space.
   - **Stability**: No.
   - Concept: Picks a pivot, sequentially strictly partitions smaller values left, larger values right. Then recurses. Very cache-friendly, making it explicitly physically much faster than Merge Sort for large primitive arrays.

4. **Heap Sort**
   - **Time**: $O(n \log n)$.
   - **Space**: $O(1)$.
   - Concept: Builds a strict Max-Heap linearly out of the array physically in place. Then continually pops max and structurally re-heapifies down.

### Non-Comparison Sorts

Algorithms mathematically bypassing the comparison bounds $O(n \log n)$ leveraging integer-specific memory mappings.

1. **Counting Sort**
   - **Time & Space Limit**: $O(n + k)$ where strictly $k$ is the max integer variance range.
   - Great for small integer arrays (like sorting student test scores strictly 0-100).
   
2. **Radix Sort**
   - **Time**: $O(d \times(n + b))$ where strictly $d$ represents digits count, $b$ is base.
   - Uses completely stable counting sorts digits by digits (safely from least significant physically to most significant bit).

## Deep Thought
Default `sort()` methods mathematically utilized in modern languages (Java `Arrays.sort`, Python `Timsort`) practically utilize hybrid approaches. They apply pure Quick Sort / Merge Sort heavily on larger bounds, but structurally shift silently to pure Insertion Sort mathematically on chunks that shrink practically less than purely ~32-64 length elements to strictly prevent recursion branch overhead.
