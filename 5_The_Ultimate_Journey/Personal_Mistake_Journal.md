# Personal Mistake Journal (The "Failure" Book)

"He who makes no mistakes, makes nothing." Use this file to log the bugs that frustrated you the most. These are your biggest growth opportunities.

## Template:
### [Date]: [Problem Name]
- **The Bug:** (e.g., Infinite loop in BFS)
- **Why it happened:** (e.g., Forgot to mark node as 'visited' before adding to queue)
- **The Solution:** (e.g., `visited.add(node)` must happen exactly when pushing to queue)
- **Lesson for next time:** Always double-check "visited" logic for Graphs.

---

## Hall of Fame (Common Mistakes to Watch For):

1. **The Off-by-One Error:**
   - `for i in range(len(arr))` vs `for i in range(len(arr) - 1)`.
   - *Fix:* Always dry run with a 2-element array.

2. **The Integer Overflow:**
   - `(a + b) / 2` can overflow in some languages.
   - *Fix:* Use `a + (b - a) / 2`.

3. **The Null Pointer Exception:**
   - Accessing `node.next` without checking `if node`.
   - *Fix:* Use a dummy node for Linked Lists to simplify edge cases.

4. **The "Pass by Value" vs "Pass by Reference" Trap:**
   - Modifying a list inside a recursive call and forgetting to backtrack.
   - *Fix:* `path.pop()` after recursion or pass a copy `path[:]`.

5. **The Improper Base Case:**
   - Recursion never stops.
   - *Fix:* Identify the smallest possible input (empty, 1 element) and write it FIRST.
