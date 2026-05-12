# Interview Communication Framework (REACT)

Coding is only 50% of the interview. The other 50% is how you communicate. Use the **REACT** framework to structure your thoughts.

## 1. R - Clarify **Requirements**
Don't start coding immediately! Spend 2-5 minutes asking:
- "What is the input size? Can it be empty?"
- "What is the range of numbers? Negative numbers allowed?"
- "Do I need to return the result or print it?"
- "Can I assume the input is valid?"

## 2. E - **Example** Test Cases
Walk through a small example manually.
- Create a normal case.
- Create an edge case (empty list, single element, negative numbers).
- This helps you catch logic errors *before* you write a single line of code.

## 3. A - Propose **Approach**
Explain your plan before coding.
- "The brute force would be $O(n^2)$ using nested loops, but I can optimize it to $O(n)$ using a Hash Map."
- Wait for the interviewer's nod or feedback. They might steer you away from a bad path.

## 4. C - **Code** Cleanly
- Use meaningful variable names (`left_pointer` instead of `i`).
- Keep it modular (use helper functions if needed).
- **Think aloud.** "I'm initializing a queue here for BFS..."

## 5. T - **Test** & Optimize
- Don't just say "I'm done."
- Walk through your code with a test case (your example from step 2).
- Analyze Time & Space complexity again.
- "Can we improve this? Maybe we can use less space?"

---

## Red Flags to Avoid
- **Silence:** If you're quiet for more than 30 seconds, the interviewer doesn't know if you're stuck or thinking.
- **Ignoring Hints:** Interviewers often give "nudges." Pay close attention to them.
- **Defensiveness:** If they find a bug, thank them and fix it. It shows coachability.

## The "I'm Stuck" Emergency Kit
If you hit a wall:
1. **Re-state the goal:** "Okay, I'm trying to find the shortest path, and I've tried BFS..."
2. **Backtrack:** "Let me look at the example again. Is there a pattern I missed?"
3. **Ask for a nudge:** "I'm thinking about using DP here, but I'm struggling with the state transition. Is that the right direction?"
