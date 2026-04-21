# Stacks and Queues

Stacks and Queues are abstract consecutive linear data structures that provide restrictive access paradigms to the elements inside them. Rather than being primarily structures for accessing data linearly, they define behavioral models.

## 1. Stacks (LIFO - Last In, First Out)

Think of a stack of plates: you add plates to the top and you remove plates from the top. The last plate placed is the first one used.

### Core Operations:
- `Push(element)`: Add element to top. -> $O(1)$
- `Pop()`: Remove top element. -> $O(1)$
- `Peek()` / `Top()`: Look at top element without removing. -> $O(1)$
- `isEmpty()`: Returns if stack is empty. -> $O(1)$

### Implementations:
- **Array-based**: Can be fast but size may be fixed, or dynamic arrays may trigger $O(n)$ resize.
- **Linked-List-based**: Uses $O(1)$ inserts and removes from the `head` node. Never has to resize.

### Famous Applicatons of Stacks:
1. **Call Stack**: Function executions in almost all modern programming languages. Recursion fundamentally relies on a call stack.
2. **Undo/Redo Mechanisms**: Every action goes on the 'undo' stack.
3. **Expression Evaluation (Postfix & Prefix)**: And syntax parsing (e.g. valid parenthesis matching algorithm).
4. **Depth-First Search (DFS)**: Under the hood, DFS traversing trees/graphs resolves via an implicit (recursion call) or explicit stack.

### Key Algorithmic Patterns:
- **Monotonic Stack**: A specialized stack to find the "Next Greater Element" or "Next Smaller Element". An invariant is maintained where elements inside the stack are strictly increasing or strictly decreasing. Extremely powerful to squash $O(n^2)$ bounds-checking comparisons down to $O(n)$.

---

## 2. Queues (FIFO - First In, First Out)

Think of a queue of people at a grocery line. The first person to line up is the first person served.

### Core Operations:
- `Enqueue(element)` / `Push(element)`: Add element to the back (tail). -> $O(1)$
- `Dequeue()` / `Pop()`: Remove front element (head). -> $O(1)$
- `Front()` / `Peek()`: See front element without removing. -> $O(1)$

### Implementations:
- **Array-based (Circular Buffer tightly recommended)**: Standard array queue gets inefficient because dequeuing from index 0 requires shifting all elements left array $O(n)$. Better approach is circularly manipulating head/tail index pointers.
- **Linked-List-based**: Keep a `head` and `tail` pointer. Enqueue to tail, Dequeue from head. Both are $O(1)$.

### Types of Queues:
1. **Simple Queue**: Standard FIFO.
2. **Circular Queue**: Last position is connected back to the first. Ideal for memory constrained hardware loops.
3. **Priority Queue**: Elements are dequeued based on priority rather than arrival time. Implemented underneath using a **Heap**, giving $O(\log n)$ enqueues and dequeues.
4. **Deque (Double Ended Queue)**: Allows $O(1)$ `Push` and `Pop` at BOTH ends. It acts as both a Stack and a Queue combined. In Python `collections.deque` and Java `LinkedList/ArrayDeque`.

### Famous Applications of Queues:
1. **Breadth-First Search (BFS)**: Essential for level-order traversal traversing trees/graphs.
2. **Task Scheduling / OS context buffering**: Printing queries, CPU task waiting limits.
3. **Web Server Request Management**: Resolving requests concurrently FIFO model.

## Deep Thought
Both abstract Data Types exist to enforce access rules. If you need arbitrary access in the middle of a collection, you don't use these. These structures are meant to guarantee ordering behaviors (LIFO and FIFO) reliably at strict $O(1)$ complex bounds.
