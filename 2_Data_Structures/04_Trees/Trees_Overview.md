# Trees

A Tree is a widespread hierarchical data structure representing parent-child relationships. Unlike Arrays, Linked Lists, and Stacks/Queues which are linear, a Tree is non-linear. 

## 1. Core Terminology
- **Node**: An object containing a value and pointers to its children.
- **Root**: The topmost node of the tree.
- **Edge**: The strictly directed link connecting a parent to a child.
- **Leaf**: A node with no children.
- **Depth of a Node**: Number of edges from the Root to that Node. (Root depth = 0).
- **Height of a Tree**: Number of edges on the longest path from Root to a Leaf.

## 2. Binary Tree

A tree where every node has at most **two children** (typically referred to as `left` and `right`).

### Traversals
Because trees are non-linear, there are multiple ways to visit the nodes:
1. **Depth-First Search (DFS)** - Recursive primarily.
   - **Pre-order (`Node -> Left -> Right`)**: Useful for copying a tree or prefix notations.
   - **In-order (`Left -> Node -> Right`)**: In a BST, this yields nodes in ascending sorted order.
   - **Post-order (`Left -> Right -> Node`)**: Useful for gracefully deleting a tree (leaves gone first).
2. **Breadth-First Search (BFS) / Level-Order**:
   - Traverses level by level from top to bottom, left to right. Requires an explicit **Queue**.

## 3. Binary Search Tree (BST)

A specialized Binary Tree providing fast search, insert, and delete capabilities.
### The BST Property invariant:
- All nodes in a node's **left** subtree must be structurally `<` the node's value.
- All nodes in a node's **right** subtree must be structurally `>` the node's value.

### Complexity:
- **Average Time (Balanced)**: $O(\log n)$ for Search, Insert, and Delete.
- **Worst Case (Unbalanced, looks like a Linked List)**: $O(n)$ for operations.

## 4. Self-Balancing Binary Search Trees

To avoid the $O(n)$ worst-case scenarios of vanilla BSTs drifting into Linked Lists, Self-balancing trees constantly re-adjust their structures to guarantee a maximum height of $O(\log n)$.

- **AVL Tree**: Stricter balancing factor. Guarantees absolutely minimal height. Very fast for mostly-read systems. Balancing via "rotations" happens on insertion/deletion.
- **Red-Black Tree**: Slightly looser balancing rules relative to AVL (uses node red/black coloring invariants). Better for write-heavy systems since it rotates less often during insertions/deletions. Standard library implementations in Java (like `TreeMap`/`TreeSet`) and C++ (`std::map`) utilize Red-Black Trees.

## 5. Other Import Tree Types

### Trie (Prefix Tree)
An advanced N-ary tree structured to store strings. Each node represents a character. Very memory efficient for text/dictionary problems.
- **Searching a word/prefix**: $O(L)$, where $L$ is the length of the string.
- Common Use: Autocomplete systems, Spell-checkers, IP routing tables.

### Segment Tree
Used heavily in competitive programming for querying range data over an array efficiently.
- Queries (like finding the sum/min/max of subarray intervals) operate in $O(\log n)$.
- Updating an element also runs in $O(\log n)$.

## Deep Thought
If you want to maintain a continuously sorted stream of elements where you might constantly insert/remove/query values dynamically, arrays require $O(n)$ shifting on insertion. A balanced tree solves this by handling inserts/deletes/searches gracefully bounded purely at $O(\log n)$.
