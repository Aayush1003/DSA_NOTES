# Recursion

## Overview
Recursion is a method of solving a computational problem where the solution depends on solutions to smaller instances of the same problem. Such problems can generally be solved by iteration, but this needs to be identified and solved at compile time. Recursion solves such recursive problems by using functions that call themselves from within their own code.

## Key Components
Every recursive algorithm consists of two parts:
1. **Base Case:** This is the terminating condition where the function stops calling itself to prevent an infinite loop.
2. **Recursive Step:** This is where the function calls itself with a modified argument, moving towards the base case.

## Example: Factorial
The factorial of a number `n` is denoted as `n!` and is defined as:
`n! = n * (n-1) * (n-2) * ... * 1`
Base case: `0! = 1`

```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive step
    else:
        return n * factorial(n - 1)
```

## Advantages
- Clean and readable code.
- Reduces repetitive code, especially in tree or graph traversals.
- Better suited for problems that have inherently recursive structures (like trees).

## Disadvantages
- High memory usage due to function call frames pushed onto the system call stack.
- Risk of Stack Overflow if recursion depth is too high.
- Usually slower than iterative counter-parts due to the overhead of function calls.

## Tail Recursion
A recursive function is tail-recursive when the recursive call is the last thing executed by the function. Some compilers can optimize tail-recursive calls to run without adding a new stack frame, thus preventing stack overflow.
