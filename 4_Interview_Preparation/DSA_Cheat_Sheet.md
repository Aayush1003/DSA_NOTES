# DSA Interview Cheat Sheet

A condensed guide to everything you need to remember right before an interview.

## 1. Time & Space Complexity Quick Ref

| Data Structure | Access | Search | Insertion | Deletion | Space |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Array** | $O(1)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ |
| **Stack** | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ | $O(n)$ |
| **Queue** | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ | $O(n)$ |
| **Singly Linked List** | $O(n)$ | $O(n)$ | $O(1)$ | $O(1)$ | $O(n)$ |
| **Hash Table** | N/A | $O(1)$ | $O(1)$ | $O(1)$ | $O(n)$ |
| **BST (Balanced)** | $O(\log n)$ | $O(\log n)$ | $O(\log n)$ | $O(\log n)$ | $O(n)$ |
| **Binary Heap** | N/A | $O(n)$ | $O(\log n)$ | $O(\log n)$ | $O(n)$ |

## 2. Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable? |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Merge Sort** | $n \log n$ | $n \log n$ | $n \log n$ | $O(n)$ | Yes |
| **Quick Sort** | $n \log n$ | $n \log n$ | $O(n^2)$ | $O(\log n)$ | No |
| **Heap Sort** | $n \log n$ | $n \log n$ | $n \log n$ | $O(1)$ | No |
| **Insertion Sort** | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | Yes |

## 3. Must-Know Patterns & Mental Models

### Sliding Window
- **When:** Input is linear (array/string), and you're asked for a sub-range (contiguous).
- **Keywords:** "longest/shortest substring", "maximum sum of subarray of size K".

### Two Pointers
- **When:** Input is sorted array or linked list. You need to find pairs or compare elements.
- **Keywords:** "target sum", "remove duplicates", "reverse array".

### Fast & Slow Pointers (Hare & Tortoise)
- **When:** Linked list or cyclic array.
- **Keywords:** "detect cycle", "find middle of linked list", "palindrome linked list".

### Merge Intervals
- **When:** Given a list of intervals.
- **Keywords:** "overlapping intervals", "merge intervals", "insert interval".

### Cyclic Sort
- **When:** Array contains numbers in a specific range (e.g., $1$ to $n$).
- **Keywords:** "find missing number", "find duplicate number".

### Top 'K' Elements (Heaps)
- **When:** Asked to find the top/smallest/frequent 'K' elements.
- **Keywords:** "Kth largest", "Top K frequent", "Merge K sorted lists".

## 4. Graph Basics
- **Adjacency List Space:** $O(V + E)$
- **Adjacency Matrix Space:** $O(V^2)$
- **BFS (Breadth First Search):** Use for **Shortest Path** in unweighted graphs. Uses a **Queue**.
- **DFS (Depth First Search):** Use for **Exhaustive Search**, connectivity. Uses **Recursion/Stack**.
- **Dijkstra:** Shortest path in weighted graphs (no negative weights). $O(E \log V)$.

## 5. Bit Manipulation Tricks
- `x ^ x = 0`
- `x ^ 0 = x`
- `x & (x - 1)` : Removes the lowest set bit (useful for counting set bits).
- `x & -x` : Gets the lowest set bit.

## 6. Tree Traversals
- **Pre-order:** Root -> Left -> Right
- **In-order:** Left -> Root -> Right (Sorted order for BST)
- **Post-order:** Left -> Right -> Root
- **Level-order:** BFS (Queue)

---
*Tip: In an interview, always clarify constraints (input size, memory limits) and ask about edge cases (null, empty, single element) before coding.*
