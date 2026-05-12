# Pattern Identification Guide

The hardest part of a DSA interview isn't writing the code—it's **identifying the correct algorithm**. This guide helps you map problem keywords to patterns.

## 1. Array & String Problems

| If the problem asks for... | Then use... | Why? |
| :--- | :--- | :--- |
| Contiguous subarray/substring | **Sliding Window** | Avoids $O(n^2)$ by moving boundaries. |
| Sorted input, finding pairs | **Two Pointers** | $O(n)$ search by narrowing the range. |
| Overlapping ranges/intervals | **Merge Intervals** | Sorting by start time simplifies logic. |
| Numbers in range $[1, n]$ | **Cyclic Sort** | Maps value to index directly. |
| Multiple sorted lists | **K-way Merge (Heap)** | Efficiently picks minimum from $K$ pointers. |

## 2. Tree & Graph Problems

| If the problem asks for... | Then use... | Why? |
| :--- | :--- | :--- |
| Shortest path (unweighted) | **BFS** | Explores level-by-level (nearest first). |
| Any path / Connectivity | **DFS** | Simple recursion to explore deep. |
| Dependent tasks (Order) | **Topological Sort** | Resolves dependencies using Indegree. |
| Minimum spanning tree | **Prim's / Kruskal's** | Greedy choice of smallest edges. |
| All possible paths/combinations | **Backtracking** | Explores all possibilities with pruning. |

## 3. Optimization & Math

| If the problem asks for... | Then use... | Why? |
| :--- | :--- | :--- |
| Maximum/Minimum sum/path (Overlapping subproblems) | **Dynamic Programming** | Caches results to avoid re-calculation. |
| Local optimal choice leads to global | **Greedy** | Faster than DP if the property holds. |
| Search in a range | **Binary Search** | $O(\log n)$ by discarding half the space. |
| Frequency count / Quick lookup | **Hash Map** | $O(1)$ access at the cost of $O(n)$ space. |

## 4. The "Mental Flowchart"

1. **Check Constraints:** 
   - $n \le 10 \implies$ Factorial/Exponential ($O(2^n)$ / $O(n!)$).
   - $n \le 100 \implies$ Cubic ($O(n^3)$).
   - $n \le 500 \implies$ Quadratic ($O(n^2)$).
   - $n \le 10^5 \implies$ Linearithmic ($O(n \log n)$).
   - $n \ge 10^6 \implies$ Linear or Logarithmic ($O(n)$ / $O(\log n)$).

2. **Is it sorted?**
   - Yes $\implies$ Binary Search or Two Pointers.
   - No $\implies$ Can I sort it? Would sorting help?

3. **Do I need to track "visited" items?**
   - Yes $\implies$ Hash Set or Boolean array.

4. **Is it a "top/bottom K" problem?**
   - Yes $\implies$ Heap (Priority Queue).

5. **Does the sub-problem result help solve the main problem?**
   - Yes $\implies$ Dynamic Programming.

---

### Pro-Tip: The "Brute Force" First
In an interview, **always** state the brute force solution first. It shows you understand the problem. Then, look for redundancies (repeated work) to apply one of the patterns above.
