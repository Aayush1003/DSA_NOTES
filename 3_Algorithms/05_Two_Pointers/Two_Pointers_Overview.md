# Two and Three Pointers

## Overview
The "Pointer" approach is a highly effective technique used to solve problems iteratively by maintaining multiple pointers (or indices) that iterate over a linear data structure like an Array, String, or Linked List. This pattern significantly optimizes the time and space complexities.

## 1. Two Pointers Pattern
In this pattern, we process two elements per loop, typically using two pointers that:
- Start from the beginning and end of a sequence (Opposite Direction).
- Look ahead or move at different speeds (Same Direction), e.g., slow and fast pointers.

### Applications (Two Pointers)
- Finding a pair in a sorted array that sums up to a target number.
- Reversing an array or string in-place.
- Detecting a cycle in a Linked List (Floyd's Cycle-Finding Algorithm).
- Partitioning arrays (e.g., in Quicksort).

### Example: Pair with Target Sum
```python
def two_sum(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return [-1, -1]
```

## 2. Three Pointers Pattern
An extension of the two-pointer technique where three pointers are used. This typically reduces an `O(N^3)` checking to `O(N^2)`.

### Applications (Three Pointers)
- **3Sum Problem:** Finding three elements in an array that sum to a target value (often `0`). The array is usually sorted first, then one pointer is fixed in an outer loop, while the other two pointers move towards each other.
- **Dutch National Flag Problem:** Sorting an array consisting of 0s, 1s, and 2s in a single pass using three pointers (`low`, `mid`, `high`).

### Example: Dutch National Flag
```python
def sort_colors(nums):
    low, mid, high = 0, 0, len(nums) - 1
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[high], nums[mid] = nums[mid], nums[high]
            high -= 1
```

## Complexity Analysis
- Usually, these techniques bring standard `O(n^2)` or `O(n^3)` brute force algorithms down to `O(n)` or `O(n^2)`.
- Space complexity is generally `O(1)` as no extra auxiliary space is allocated.
