# Linked Lists

A Linked List is a linear data structure consisting of a sequence of dynamically allocated nodes. Unlike arrays, linked list elements are not stored at contiguous memory locations. Instead, each node contains **data** and a **reference (pointer/link)** to the next node in the sequence.

## 1. Core Structure of a Node (Singly Linked List)

```java
class Node {
    int data;
    Node next;
    
    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

## 2. Types of Linked Lists

### A. Singly Linked List
Each node has data and points to the `next` node. Traversal is strictly unidirectional.
- Head reference marks the start. Tail reference (optional) marks the end, its next points to `null`.

### B. Doubly Linked List
Each node maintains a `prev` and `next` pointer.
- **Pros**: Allows for backward traversal. Deleting a given node is $O(1)$ if you hold a reference to it (because you can access its previous node instantly).
- **Cons**: Requires more memory to store the extra `prev` pointer per node. More complex pointer manipulation.

### C. Circular Linked List
The last node points back to the `head` node rather than `null`.
- Can be singly or doubly circular.
- Useful for applications that need to continually loop over items, like a Round-Robin scheduling algorithm in an OS, or multiplayer turn-taking.

## 3. Complexity Operations

| Operation | Time Complexity | Notes |
|-----------|-----------------|-------|
| **Access** | $O(n)$ | Must traverse nodes sequentially from the head (no index-based mapping). |
| **Search** | $O(n)$ | Must traverse linearly. |
| **Insertion (Start)** | $O(1)$ | Just rewire the new node's next to current head, and reassign head. |
| **Insertion (End)** | $O(n)$ or $O(1)$ | $O(n)$ if only head is known. $O(1)$ if tail reference is maintained. |
| **Insertion (Middle)**| $O(n)$ | Finding the position takes $O(n)$, but the actual pointer rewiring takes $O(1)$. |
| **Deletion (Start)** | $O(1)$ | Reassign head to `head.next`. |
| **Deletion (End)** | $O(n)$ | Must traverse to the second-to-last node to sever the link. |

## 4. Key Link List Algorithms & Patterns

1. **Fast and Slow Pointers (Floyd's Tortoise and Hare Algorithm)**: 
   - Uses two pointers moving at different speeds (e.g., one moves 1 step, the other moves 2 steps).
   - Core Uses:
     - **Detecting a Cycle**: If the list has a cycle, the fast pointer will eventually overlap with the slow pointer.
     - **Finding the Middle**: When the fast pointer hits the end, the slow pointer is precisely at the middle node.
2. **Dummy Head (Sentinel Node)**:
   - Extremely helpful cleanly handling edge cases when nodes at the start need to be removed or operated on.
   - Example pattern: `Node dummy = new Node(0); dummy.next = head; ... return dummy.next;`
3. **Reversing a Linked List**:
   - Requires keeping track of 3 pointers `prev`, `current`, `next` and iteratively (or recursively) flipping the arrows. It's a fundamental interview test of your grasp of references.
4. **Merge Two Sorted Lists**:
   - Similar to the merge step of Merge Sort but manipulated via pointers with $O(1)$ auxiliary space.

## 5. Deep Thought: When to choose Linked List over Array?
- **Unknown dynamic sizes**: When you have no idea how many elements you will manage, and you want to prevent sudden large amortized reallocation delays.
- **Frequent Head/Middle Insertions & Deletions**: If you are constantly inserting into the beginning or middle of a sequence, linked lists will do this in $O(1)$ *after* traversing to the node (for middle).
- **Cons over Arrays**: Poor spatial caching logic. Jumping across random memory blocks forces cache misses. Large pointer memory overhead. No random `O(1)` index access.
