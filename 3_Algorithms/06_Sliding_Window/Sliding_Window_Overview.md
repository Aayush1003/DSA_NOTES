# Sliding Window Pattern

## Overview
The Sliding Window pattern is often used to solve problems that involve arrays or linked lists. These problems typically look for a contiguous subset (like a sub-array or sub-string) of a certain size (or condition) that fulfills specific constraints. 
Instead of computing everything repeatedly from scratch for each subset (which is usually an `O(n^2)` or `O(n^k)` solution), we create a window that moves smoothly over the data.

## Fixed vs Variable Sliding Window
- **Fixed Window:** The size `k` of the window is fixed. The window merely shifts by dropping the first element and adding the new element at the end.
- **Variable Sliding Window:** The window size grows and shrinks according to a certain condition (often used to find minimum/maximum sub-array satisfying a criteria).

## Identifying Sliding Window Problems
- The problem asks for the maximum, minimum, longest, or shortest something.
- The thing you are looking for must be contiguous (e.g., a sub-array or sub-string).

## Example: Fixed Window
**Problem:** Find the maximum sum of any contiguous subarray of size `k`.
```python
def max_sub_array_of_size_k(k, arr):
    max_sum, window_sum = 0, 0
    window_start = 0

    for window_end in range(len(arr)):
        window_sum += arr[window_end]  # add the next element
        # slide the window if we've hit the size k
        if window_end >= k - 1:
            max_sum = max(max_sum, window_sum)
            window_sum -= arr[window_start]  # subtract the element going out
            window_start += 1  # slide the window ahead
    return max_sum
```

## Example: Variable Window
**Problem:** Find the length of the smallest contiguous subarray whose sum is greater than or equal to `S`.
```python
def smallest_subarray_with_given_sum(s, arr):
    window_sum = 0
    min_length = float('inf')
    window_start = 0

    for window_end in range(len(arr)):
        window_sum += arr[window_end]

        # shrink the window as small as possible while the condition is met
        while window_sum >= s:
            min_length = min(min_length, window_end - window_start + 1)
            window_sum -= arr[window_start]
            window_start += 1

    return min_length if min_length != float('inf') else 0
```
