# Complexity Analysis & Big O Notation

Understanding complexity is the foundation of analyzing any data structure or algorithm. It allows us to mathematically evaluate the efficiency of an algorithm in terms of time (execution speed) and space (memory consumption).

## 1. Time Complexity

Time complexity is not about measuring the exact physical time in seconds/milliseconds an algorithm takes. Instead, it measures the **rate of growth of the time taken as the input size ($n$) approaches infinity**.

### Common Asymptotic Notations
- **Big O ($O$)**: Represents the **Upper Bound** (Worst-case scenario). It defines the maximum time an algorithm could take.
- **Omega ($\Omega$)**: Represents the **Lower Bound** (Best-case scenario). It defines the minimum time an algorithm needs.
- **Theta ($\Theta$)**: Represents the **Tight Bound** (Average-case or exact bounds).

*We generally focus on Big O ($O$) notation because we usually want to know the worst-case performance guarantees of our systems.*

### Big-O Complexity Chart (From Best to Worst)

| Complexity Name | Notation | Example Algorithms / Operations |
|-----------------|----------|----------------------------------|
| Constant | $O(1)$ | Array lookup `arr[i]`, Push/Pop on Stack, Hash Map Get/Set. Size of input doesn't matter. |
| Logarithmic | $O(\log n)$ | Binary Search, Traversing a balanced BST. The input size is fractioned (usually halved) at each step. |
| Linear | $O(n)$ | Simple loop through an array/list, Linear Search. Time scales linearly with input size. |
| Linearithmic | $O(n \log n)$| Merge Sort, Quick Sort, Heap Sort. Typically seen in efficient sorting algorithms or 'divide and conquer' combined with linear work. |
| Quadratic | $O(n^2)$ | Nested loops, Bubble sort, Insertion sort. Operations grow proportional to the square of size. |
| Cubic | $O(n^3)$ | Three nested loops, naive matrix multiplication. |
| Exponential | $O(2^n)$ | Recursive Fibonacci, Generating all subsets. Highly inefficient for large $n$. |
| Factorial | $O(n!)$ | Permutations, Traveling Salesman Problem (brute force). The worst complexity. |

## 2. Space Complexity

Space complexity measures the total amount of memory an algorithm utilizes relative to the input size. It consists of:
1. **Auxiliary Space**: The extra, temporary space used by the algorithm.
2. **Input Space**: Space used to store input variables.

*When we say an algorithm has $O(1)$ space complexity, we mean its auxiliary space is constant.*

### Memory Cost of Data Structures (Worst Case)
- Primitive Types (int, boolean): $O(1)$
- Arrays/Lists (size $n$): $O(n)$
- 2D Arrays ($n \times n$): $O(n^2)$
- Call stack in Recursion (depth $n$): $O(n)$ additional memory

## 3. Rules to Calculate Big O Time Complexity

1. **Drop the Constants**: $O(2n) \rightarrow O(n)$. $O(n/2) \rightarrow O(n)$. Constants don't matter as $n \to \infty$.
2. **Drop the Non-Dominant Terms**: $O(n^2 + n) \rightarrow O(n^2)$. As $n$ grows, $n^2$ dominates the growth curve.
3. **Different steps get added**: If you do step A then step B, it's $O(a + b)$.
   ```python
   for x in arrA: print(x)
   for y in arrB: print(y)
   # Complexity: O(A + B)
   ```
4. **Different nested steps get multiplied**: If you do step B inside step A, it's $O(a \times b)$.
   ```python
   for x in arrA:
       for y in arrB:
           print(x, y)
   # Complexity: O(A * B)
   ```

## 4. Deep Thinking & Tips
- Always ask: "What is $n$?" Understand what the input size is. For graphs, it's usually defined in terms of Vertices ($V$) and Edges ($E$), so complexities look like $O(V + E)$.
- Recursion adds to Space Complexity: Every recursive call adds a frame to the call stack. A recursive function that calls itself $n$ times has an $O(n)$ space complexity unless optimized with tail recursion (which is language-dependent).
- Trade-offs: Very often, you can optimize Time Complexity by worsening Space Complexity (e.g., using a Hash Table to "remember" states, lowering time from $O(n^2)$ to $O(n)$ but raising space from $O(1)$ to $O(n)$). This is known as a **Space-Time Tradeoff**.
