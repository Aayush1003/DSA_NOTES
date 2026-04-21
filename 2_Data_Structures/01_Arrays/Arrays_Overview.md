# Arrays

An Array is a linear data structure that stores a collection of items at contiguous memory locations. The idea is to store multiple items of the same type together, allowing for quick access using an index.

## 1. Memory Representation
Because array elements are stored in contiguous memory blocks, calculating the memory address of an element at a given index is a simple mathematical operation.
- Address of `arr[i]` = `Base_Address` + `(i * size_of_data_type)`
- This contiguous nature provides high **Spatial Locality**, which makes arrays heavily optimized for modern CPU caching mechanisms.

## 2. Types of Arrays

### A. Static Arrays
Fixed in size. Memory is allocated either at compile-time (global/stack arrays) or explicitly at runtime, but cannot change dynamically.
- **Pros**: Zero overhead, fast, contiguous elements.
- **Cons**: Size rigidly fixed. Can waste memory if over-allocated or cause overflow if under-allocated.

### B. Dynamic Arrays (e.g., `ArrayList` in Java, `list` in Python, `std::vector` in C++)
Can grow dynamically as elements are added. When the dynamic array reaches capacity, it allocates a new, larger block of memory (usually double the size), copies elements over, and frees the old block.
- **Amortized Time Complexity**: Inserting at the end is $O(1)$ amortized. Even though the resizing operation is $O(n)$, it happens rarely, so the average operations cost $O(1)$.

## 3. Complexity Operations

| Operation | Best Case | Worst Case | Reason |
|-----------|-----------|------------|--------|
| **Access** | $O(1)$ | $O(1)$ | Index calculation using formula. |
| **Search (Unsorted)** | $O(1)$ | $O(n)$ | Must check each element linearly. |
| **Search (Sorted)** | $O(1)$ | $O(\log n)$ | Can use Binary Search. |
| **Insertion (End)** | $O(1)$ | $O(n)$ | $O(1)$ if space exists. $O(n)$ if static capacity full & resizing dynamic array. |
| **Insertion (Middle)**| $O(n)$ | $O(n)$ | Must shift all subsequent rightward elements. |
| **Deletion (End)** | $O(1)$ | $O(1)$ | Just remove it. |
| **Deletion (Middle)**| $O(n)$ | $O(n)$ | Must shift all subsequent string leftward. |

## 4. Multi-dimensional Arrays
Arrays of arrays. A 2D array (matrix) is logically viewed as rows and columns.
- Row-major order (most common, e.g. C/C++, Python) vs Column-major order.
- Time to traverse an $N \times M$ 2D array is $O(N \times M)$.

## 5. Key Array Algorithms & Patterns to Master

1. **Two Pointers**: Used mostly in sorted arrays for searching pairs, reversing arrays, or finding palindromes. (e.g., Left pointer at index 0, Right at index $n-1$).
2. **Sliding Window**: Excellent for subarray/substring problems. Maintaining a "window" of array elements and sliding it forward to prevent recalculating overlapping elements. Complexity drops from $O(n^2)$ or $O(n^k)$ down to $O(n)$.
3. **Prefix Sum (Cumulative Sum)**: Used to query the sum of a subarray in $O(1)$ time after an $O(n)$ preprocessing step. `prefix[i] = prefix[i-1] + arr[i]`.
4. **Kadane's Algorithm**: For finding the Maximum Subarray Sum in $O(n)$ time.
5. **Dutch National Flag Algorithm / Three-way Partitioning**: For sorting arrays with 3 unique elements (e.g., 0s, 1s, and 2s) in a single pass $O(n)$ time and $O(1)$ space.
6. **Boyer-Moore Majority Vote Algorithm**: Finding the majority element (appears > $n/2$ times) in $O(n)$ time and $O(1)$ space.

## 6. Deep Thought: Arrays vs Linked Lists
Why use Arrays instead of Linked Lists since insertions/deletions are slow?
- Because modern CPU cache architectures significantly reward **Contiguous Memory Allocation**.
- Iterating through an array is physically many times faster than iterating via pointers in a linked list, because blocks of the array are pre-fetched into the L1/L2 cache. Therefore, arrays are preferred in almost all high-performance rendering engines and high-frequency algorithms unless insertions/deletions structurally dominate the program flow.
