# DSA Patterns: Detailed Theory

This guide expands the patterns listed in `DSA patterns Cheat Sheet.xlsx`. Use it to understand **when** a pattern applies, **what invariant** makes it correct, and **which complexity** to target before opening the linked problems.

## How to Read a Problem

1. Identify the input shape: array, string, linked list, tree, graph, or sequence of choices.
2. Look for structure: sorted data, contiguity, repeated subproblems, dependencies, or a fixed `k`.
3. State the brute-force idea and its repeated work.
4. Choose a pattern that removes that repeated work.
5. Write the invariant: the fact that must remain true after every iteration.
6. Test boundaries: empty input, one item, duplicates, negative values, and the answer at either endpoint.

For typical constraints, `O(n)` or `O(n log n)` is expected when `n` can be `10^5`. Exponential backtracking is usually reserved for small `n`, unless pruning or memoization reduces the work.

## 1. Two Pointers

### Core idea

Maintain two indexes and move at least one of them on every iteration. The movement is justified by an ordering or by the fact that a part of the search space can no longer contain an answer.

### When to recognize it

- The array is sorted and the task asks for a pair, triplet, difference, or closest value.
- The task compares characters or values from both ends of a sequence.
- The array contains a binary partition such as `0`s and `1`s.
- A result must be built in place with `O(1)` extra space.

### Main variants

- **Opposite ends:** `left = 0`, `right = n - 1`; useful for target sums and palindromes.
- **Same direction:** a slow pointer stores the next write position while a fast pointer scans; useful for removing duplicates.
- **Partitioning:** move values that belong on the wrong side until the range is partitioned.

### Invariant and complexity

For a sorted pair-sum problem, if `a[left] + a[right]` is too small, every pair using `left` with a smaller right index is also too small, so `left` can advance. If it is too large, decrease `right`. This gives `O(n)` time and `O(1)` extra space after sorting; sorting adds `O(n log n)` if the input is not already sorted.

### Common mistakes

- Moving both pointers after a non-matching sum, which can skip a valid pair.
- Forgetting to skip duplicates when unique combinations are requested.
- Using this pattern on unsorted input without first deciding whether sorting is allowed.
- Returning indexes after sorting without preserving original indexes.

Typical workbook problems: Pair with Target Sum, Rearrange 0 and 1, Remove Duplicates, and 3Sum.

## 2. Fast and Slow Pointers

### Core idea

Two pointers traverse a sequence at different speeds. If a cycle exists, the faster pointer eventually catches the slower pointer inside that cycle.

### Cycle reasoning

Use `slow = slow.next` and `fast = fast.next.next`. If `fast` or `fast.next` becomes `None`, the list is acyclic. If the pointers meet, the meeting point proves a cycle but is not necessarily its entry.

To find the cycle entry, reset one pointer to the head and move both one step at a time. They meet at the entry because the distance from the head to the entry equals the distance from the first meeting point around the cycle, modulo the cycle length.

### Other uses

- Find the middle of a linked list; when `fast` reaches the end, `slow` is at the middle.
- Detect happy-number cycles by treating each number transformation as a next pointer.
- Split a list before reversing or checking whether it is a palindrome.

Time is `O(n)` and extra space is `O(1)`. Decide whether an even-length list should return the first or second middle before coding.

## 3. Sliding Window

### Core idea

Track a contiguous range `[window_start, window_end]` and update its state incrementally as the right edge expands and the left edge contracts.

### Fixed-size window

Use when the size is exactly `k`. Add the new right value, evaluate the window when it reaches size `k`, then remove the outgoing left value. This solves maximum sum of a subarray of size `k` in `O(n)` time and `O(1)` or `O(alphabet)` space.

### Variable-size window

Use when a window must satisfy a condition such as at most `k` distinct values or sum at least `target`.

1. Expand the right edge and update counts or sums.
2. While the window is valid, record the answer if looking for a minimum, then shrink from the left.
3. If looking for a maximum or longest valid window, record after the window becomes valid.

This is linear when every item enters and leaves the window at most once. The usual positive-number minimum-sum template does **not** work with negative values; use prefix sums and a suitable monotonic structure instead.

### Frequency-map windows

Maintain a map from value or character to frequency. Keep a `distinct` count or a `missing` count rather than repeatedly examining the whole window. For replacement problems, the window is valid when:

`window_length - most_frequent_count <= allowed_replacements`.

The maximum frequency can remain stale while expanding in the common longest-window formulation; shrinking is still safe because the window length is only used to improve the best answer. Be more careful when the exact current frequency is required.

Typical workbook problems: Maximum Sum Subarray of Size K, Fruits into Baskets, No-repeat Substring, Minimum Window Substring, and String Anagrams.

## 4. Kadane Pattern

### Core idea

At each index, decide whether the best subarray ending here should extend the previous subarray or start again at the current value.

`best_ending_here = max(value, best_ending_here + value)`

`best_so_far = max(best_so_far, best_ending_here)`

Initialize from the first element, not zero, when all values may be negative. The standard algorithm is `O(n)` time and `O(1)` space.

### Variants

- **Minimum subarray:** replace `max` with `min`.
- **Maximum product:** track both the largest and smallest product ending at the index because a negative value can swap their roles.
- **One deletion:** maintain states for the best sum with no deletion and with one deletion.
- **Circular array:** compare ordinary Kadane with `total_sum - minimum_subarray_sum`; use the ordinary result when every value is negative.
- **Maximum absolute sum:** compute the largest positive and most negative subarray sums.

The key question is whether the required subarray must be non-empty. That determines initialization and the all-negative result.

## 5. Prefix Sum

### Core idea

Define `prefix[i]` as the sum of elements before or through index `i`. Then the sum of a range can be found by subtraction:

`sum(left..right) = prefix[right + 1] - prefix[left]`.

### Prefix-sum hash map

For subarray sum equal to `k`, while scanning with running sum `current`, a previous prefix of `current - k` means the intervening subarray sums to `k`. Store how many times each prefix occurs, starting with `{0: 1}`. This handles overlapping subarrays and negative values in `O(n)` time.

For sums divisible by `k`, store counts by `prefix % k`. Normalize negative remainders when the language requires it. For a binary array, convert `0` to `-1`; equal prefix sums then represent equal numbers of zeroes and ones.

### When to prefer another pattern

If all numbers are non-negative and the task asks for a shortest or longest range satisfying a sum threshold, a sliding window may be simpler. For arbitrary negative numbers and a threshold, consider prefix sums plus a monotonic deque.

## 6. Merge Intervals

### Core idea

Sort intervals by start time. After sorting, only the last merged interval can overlap the next interval, so the entire problem becomes a single scan.

For intervals `[start, end]` and `[next_start, next_end]`, they overlap when `next_start <= end` for closed intervals. Merge by setting `end = max(end, next_end)`. Otherwise, emit the current interval and start a new one.

Sorting costs `O(n log n)` and the scan costs `O(n)`. The output itself may require `O(n)` space.

### Important variants

- **Insert interval:** emit intervals that end before the new interval, merge all overlaps with it, then emit the remainder.
- **Intersection:** for two sorted lists, intersect using `max(starts)` and `min(ends)`, then advance the interval that ends first.
- **Meeting rooms:** sort starts and ends separately or use a min-heap of active end times.
- **Maximum CPU load:** maintain active jobs and sum their loads in a min-heap ordered by end time.

State whether touching endpoints overlap. A mismatch between `<` and `<=` is a frequent source of wrong answers.

## 7. In-place Reversal of a Linked List

### Core idea

Reverse links one at a time while preserving the unreversed suffix:

```text
previous = None
current = head
while current is not None:
    next_node = current.next
    current.next = previous
    previous = current
    current = next_node
return previous
```

The saved `next_node` is essential because changing `current.next` otherwise loses the remaining list. The iterative solution is `O(n)` time and `O(1)` space.

### Sublist and group reversals

Use a dummy node before the head to simplify reversal at the first position. Locate the node before the section, reverse exactly the required number of links, and reconnect the prefix and suffix. For groups of `k`, first determine whether a complete group exists; reverse incomplete final groups only if the problem explicitly requires it.

For list rotation, compute the length, connect the tail to the head temporarily, and break the circle at the new tail. Reduce `k` modulo the length.

## 8. Stack and Monotonic Stack

### Core idea

A stack stores the most recent unresolved items. It is appropriate when the newest item must be processed first, or when a problem contains nested structure.

- Parentheses and path simplification use LIFO matching.
- Adjacent duplicate removal repeatedly compares the current value with the stack top.
- Expression and undo-style problems use the stack to preserve prior state.

### Monotonic stack

For next greater or next smaller problems, maintain indexes whose answers are not known yet. When the current value resolves the top condition, pop it and assign its answer. Then push the current index.

Use a decreasing stack for next greater values and an increasing stack for next smaller values, adjusting the exact inequality for duplicates. Each index is pushed and popped at most once, giving `O(n)` time and `O(n)` space.

For circular arrays, scan `2n` positions and use `index % n`, or initialize the stack from a second conceptual pass.

## 9. Hash Maps and Frequency Counting

### Core idea

Use a hash map for expected `O(1)` average lookup and update. It is ideal when the problem asks whether something has appeared, how often it appears, or where it last appeared.

Common state choices:

- `frequency[value]` for counts and anagram checks.
- `last_seen[value]` for the most recent index.
- `complement -> index` for two-sum style lookups.
- `prefix_sum -> count` for subarray counting.

Separate **existence**, **frequency**, and **index** maps; mixing their meanings often creates bugs. Consider a fixed-size array instead of a map when the alphabet or value range is small and known.

Hashing usually costs `O(n)` time and `O(n)` space. Worst-case hash behavior depends on the language implementation, but average-case complexity is the interview convention.

## 10. Binary Search

### Core invariant

Maintain a search interval in which the answer must still exist. Each iteration discards a half that cannot contain the answer.

Use `mid = left + (right - left) // 2` to avoid integer overflow in languages with fixed-width integers.

### Bound searches

- **Lower bound:** first index with `value >= target`.
- **Upper bound:** first index with `value > target`.
- First occurrence is lower bound; last occurrence is upper bound minus one, after checking presence.

The loop condition and pointer updates must match the interval convention. A useful half-open convention is `[left, right)`: when the predicate is true, set `right = mid`; otherwise set `left = mid + 1`.

### Rotated arrays and peaks

In a rotated sorted array, at least one half is sorted. Determine which half is sorted, decide whether the target lies within it, and discard the other half. Duplicates can make both halves appear equal; handle that ambiguity explicitly, sometimes by shrinking one boundary.

For a mountain or peak problem, compare `mid` with `mid + 1`. If the slope rises, move right; otherwise move left, preserving a peak in the remaining range.

### Binary search on the answer

This applies when the answer is numeric and feasibility is monotonic: if capacity `x` works, every larger capacity also works, or vice versa. Search the numeric range, and write a greedy `can_do(candidate)` checker. Typical examples include Koko, shipping capacity, bouquet days, book allocation, aggressive cows, and splitting an array.

For answer search, define the smallest and largest possible answers from the input rather than guessing arbitrary bounds. Total complexity is `O(log range * checker_cost)`.

## 11. Heaps and Priority Queues

### Core idea

A heap gives access to the smallest or largest active item in `O(log n)` update time and `O(1)` peek time. It is useful when candidates arrive continuously and only the best current candidate matters.

### Top K and K-way merge

- Keep a min-heap of size `k` for the `k` largest values; remove the smallest when the heap grows beyond `k`.
- Keep a max-heap of size `k` for the `k` smallest values.
- For top-frequency problems, count first, then heapify candidates by frequency.
- For K sorted arrays or lists, place the first item from each source in a min-heap. Pop the smallest and push the next item from the same source.

K-way merge costs `O(N log K)` for `N` total items. Always store enough metadata to locate the next item, such as source index and position.

### Two heaps

Maintain a max-heap for the lower half and a min-heap for the upper half. Keep their sizes equal or let the lower half contain one extra item. The median is either the top of the larger heap or the average of both tops. Rebalance after each insertion.

### Greedy with heaps

Sort or process events in a useful order, then use a heap for the best currently available choice. This is the core of refueling, IPO, task scheduling, course scheduling, and several resource-allocation problems.

## 12. Recursion and Backtracking

### Recursion model

Every recursive function needs:

1. A base case that returns without another recursive call.
2. A smaller subproblem.
3. Progress toward the base case.
4. A clear meaning for the return value.

For simple sequence problems such as Fibonacci, recursion exposes the recurrence but repeats work. Memoization changes the time from exponential to linear. For stack depth concerns, an iterative solution may be preferable.

### Backtracking model

Backtracking explores a decision tree:

1. Choose a candidate.
2. Apply it to the current state.
3. Recurse.
4. Undo the choice.

The undo step must restore every piece of mutable state. Use a `start` index for combinations, a `used` structure for permutations, and a validity check for parentheses or palindrome partitions.

Prune as soon as the partial state cannot lead to a valid answer. The worst case is often exponential, but good pruning and constraints determine whether it is practical. Avoid duplicate branches by skipping equal values at the same recursion depth after sorting.

## 13. Tree Patterns

### Traversal selection

- **Preorder:** process node before children; useful for serialization and construction.
- **Inorder:** left, node, right; sorted order for a binary search tree.
- **Postorder:** children before node; useful when a node depends on child results.
- **Level order:** breadth-first traversal; useful for depth, nearest nodes, and level-based output.

DFS recursion uses `O(h)` stack space, where `h` is tree height. BFS uses `O(w)` queue space, where `w` is maximum width. A skewed tree has `h = n`, while a balanced tree has `h = O(log n)`.

### The return-value technique

For bottom-up tree problems, make the recursive function return exactly the information the parent needs. Examples:

- Balanced tree: return height, or a failure sentinel when a subtree is unbalanced.
- Diameter: return height while updating the best path through the current node.
- Maximum path sum: return the best downward gain; update the global answer with left gain plus node plus right gain.
- Path sum: pass the remaining target downward, or return whether a child can complete it.

Do not allow a negative child contribution to reduce a maximum path; clamp it to zero when the path may stop at the current node.

### BST reasoning

For a binary search tree, all values in the left subtree are smaller and all values in the right subtree are larger, subject to the duplicate policy. Validate with an allowed range passed down recursively, not only by comparing a node with its direct children.

Inorder traversal of a valid BST is sorted, so it supports kth-smallest and sorted-value checks. For LCA in a BST, move left or right using value comparisons; for a general tree, recurse into both children and combine the returned candidates.

### Construction and symmetry

When constructing from preorder/inorder or postorder/inorder, the traversal identifies the root and the inorder position splits the left and right subtrees. A value-to-index map avoids repeatedly scanning inorder, giving `O(n)` construction. Mirror and symmetry checks compare corresponding nodes recursively or with a queue of node pairs.

## 14. Graph Patterns

### Representation

An adjacency list uses `O(V + E)` space and is usually best for sparse graphs. An adjacency matrix uses `O(V^2)` space but gives constant-time edge lookup. Decide whether edges are directed, weighted, and one-way before building the graph.

### DFS and BFS

Both visit each reachable vertex and edge in `O(V + E)` with an adjacency list. Mark a node when it is added to the stack or queue, not when it is removed, to avoid duplicate work.

- DFS is natural for components, flood fill, cycle detection, and exploring a path.
- BFS is natural for shortest paths in unweighted graphs because the first visit occurs at minimum distance.
- Multi-source BFS starts with all sources at distance zero, as in Rotten Oranges.

### Cycle detection and bipartite graphs

For an undirected graph, DFS/BFS tracks the parent; a visited neighbor that is not the parent indicates a cycle. For a directed graph, track three states: unvisited, currently visiting, and finished. An edge to a currently visiting node is a back edge and proves a cycle.

To test bipartiteness, color a node and all neighbors with alternating colors. A conflict means the graph is not bipartite. This also explains why an odd cycle fails two-coloring.

### Topological sort

Topological order exists only for a directed acyclic graph. Kahn's algorithm repeatedly removes zero-indegree nodes; DFS uses the visiting-state cycle check and pushes a node after exploring its dependencies. If fewer than `V` nodes are output, a cycle exists.

### Shortest paths and spanning trees

- **Unit-weight graph:** BFS.
- **Non-negative weighted graph:** Dijkstra with a min-heap; ignore stale heap entries when popped distance is no longer current.
- **Negative edges:** Bellman-Ford, which relaxes every edge `V - 1` times and can detect negative cycles.
- **Minimum spanning tree:** Prim grows one connected tree using the cheapest crossing edge; Kruskal sorts edges and uses DSU to avoid cycles.

Dijkstra is not valid with negative edge weights. For grid problems, model cells as vertices and use BFS, Dijkstra, or binary search on a threshold depending on the cost definition. Word Ladder is an unweighted shortest-path problem over implicit neighbor relationships.

## 15. Dynamic Programming

### When DP applies

DP is appropriate when a problem has:

- **Overlapping subproblems:** the same state is reached repeatedly.
- **Optimal substructure:** an optimal answer can be built from optimal answers to smaller states.

### A reliable design process

1. Define the state in one sentence, such as `dp[i]` = best answer using the first `i` items.
2. Write the transition from smaller states.
3. Set base cases for the smallest valid inputs.
4. Choose top-down memoization or bottom-up tabulation.
5. Determine the iteration order from dependencies.
6. Compress space only after the full recurrence is correct.

### Workbook families

- **Fibonacci and Climbing Stairs:** one-dimensional recurrence; keep the previous two states.
- **House Robber:** at each house, choose skip or take; `dp[i] = max(dp[i - 1], dp[i - 2] + value)`.
- **0/1 Knapsack:** each item is used once. Iterate capacity backward for a one-dimensional in-place table so an item is not reused in the same iteration.
- **Subset Sum and Target Sum:** boolean or counting knapsack states; check whether the target is reachable before indexing.
- **LIS:** the `O(n^2)` DP compares earlier smaller values; the tails method gives `O(n log n)` length but stores tails, not necessarily the actual sequence.
- **LCS:** compare the final characters; equal characters extend the diagonal state, otherwise take the better of removing one character from either string.
- **Unique Paths:** grid transitions come from the top and left; obstacles force a zero state.
- **Stock problems:** include day, holding state, transaction count, and cooldown/fee when relevant. Write the state before coding.
- **Minimum cost to cut a stick:** interval DP; sort cuts and solve smaller intervals between boundary cuts.

Do not call a greedy choice DP without proving that local choices are safe. Do not use a two-dimensional table when the transition only needs the previous row, but preserve the correct direction when compressing.

## 16. Greedy Algorithms

### Core idea

Make the best-looking local choice and prove that it can be part of an optimal global solution. A greedy algorithm needs more than an intuition that the choice is reasonable.

Common proof ideas are an exchange argument, a cut property, or showing that an optimal solution can be transformed to use the greedy choice without becoming worse.

### Workbook examples

- **Assign Cookies:** sort children and cookies, then satisfy the least-demanding remaining child with the smallest sufficient cookie.
- **Lemonade Change:** preserve smaller bills because they are more flexible as future change.
- **Jump Game:** maintain the farthest reachable index; if the current index is beyond it, the goal is impossible.
- **Fractional Knapsack:** sort by value-to-weight ratio because fractions make the exchange argument valid.
- **Interval scheduling:** sort by earliest finishing time to leave maximum room for future intervals.
- **Heap-assisted greedy:** when several choices are currently feasible, use a heap to select the best one; refueling and IPO are examples.

Greedy often fails for 0/1 knapsack, arbitrary coin change, and many transaction-limited stock problems because a locally best choice can block a better combination. Use DP or another proof-backed method there.

## Pattern Selection Quick Reference

| Signal in the problem | First pattern to test | Essential question |
| --- | --- | --- |
| Sorted array and pair/triplet | Two pointers | Which pointer movement discards impossible pairs? |
| Cycle or middle of a list | Fast/slow pointers | Can traversal speed expose the structure? |
| Contiguous range | Sliding window or prefix sum | Are values non-negative, or are negatives allowed? |
| Best contiguous sum | Kadane | Should the current range extend or restart? |
| Exact range sums or count of subarrays | Prefix sum + map | Which prior prefix produces the target? |
| Overlapping time ranges | Merge intervals | What happens after sorting by start? |
| Next greater/smaller | Monotonic stack | Which unresolved indexes does the current value resolve? |
| Top K or streaming minimum/maximum | Heap | How many candidates must remain active? |
| Monotonic feasible numeric answer | Binary search on answer | Is the feasibility checker one-directional? |
| All combinations or permutations | Backtracking | What choice is made, and how is it undone? |
| Parent depends on children | Postorder tree DFS | What compact result should the child return? |
| Shortest unweighted path | BFS | Are all edges equal cost? |
| Repeated states and optimization | DP | What is the smallest complete state? |
| Locally safe choice with a proof | Greedy | Can an exchange or cut argument justify it? |

## Practice Map

The workbook remains the source of truth for the complete problem links. Use this guide before solving each group:

- **Arrays and strings:** Two Pointers, Sliding Window, Kadane, Prefix Sum, Hash Maps, and Binary Search.
- **Intervals and scheduling:** Merge Intervals, Heaps, and Greedy.
- **Linked lists:** Fast/Slow Pointers and In-place Reversal.
- **Nested or next-element logic:** Stack and Monotonic Stack.
- **Search spaces and selection:** Binary Search and Heaps.
- **Exhaustive construction:** Recursion and Backtracking.
- **Hierarchical data:** Tree Traversals, BST reasoning, Path Sum, and Construction.
- **Networks:** DFS, BFS, cycle detection, topological sort, shortest paths, and MST.
- **Optimization:** Dynamic Programming and Greedy.

For each problem, write down the pattern, invariant, complexity, and one edge case before looking at an implementation. That turns the spreadsheet from a list of links into a deliberate progression from recognition to mastery.