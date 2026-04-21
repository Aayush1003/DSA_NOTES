# Dynamic Programming (DP)

Dynamic Programming is a mathematical algorithmic paradigm fundamentally focused on **optimizing recursive solutions**. Its entire premise relies on safely storing overlapping structural computational subsets drastically preventing redundant mathematical calculations.

If an unoptimized recursive problem scales factorially $O(2^n)$ branching violently downwards—mathematically converting it cleanly into a DP solution almost always restricts memory limits physically binding strictly to polynomial time curves effectively $O(n)$ or $O(n^2)$.

## 1. When internally to apply DP?
You apply mathematically Dynamic Programming strictly if completely both logical prerequisites are distinctly met:
1. **Overlapping Subproblems**: The mathematical problem breaks down systematically continuously resolving identically the exact same physical subproblems. (Example mapping: Fibonacci sequence computes `F(4)` mathematically twice calculating `F(6)`).
2. **Optimal Substructure**: The perfectly mathematically globally optimized answer precisely integrates locally strictly optimized internal subset bounds. (Finding fundamentally shortest overall physical paths mathematically leverages internal subsets shortest completely strictly bounded pathways).

## 2. Core Methodologies

There fundamentally purely exist identically two internal logical pathways mathematically computing DP paradigms.

### A. Top-Down Structure (Memoization)
- Inherits mathematically naturally strictly structural recursion formats.
- Starts structurally solving completely the overarching strict $N$ target. During factorial descents recursively downwards, bounds actively log cleanly computed output values explicitly inside mapped Memory variables (Arrays or explicitly Hash Tables).
- Before mapping recursively strictly structurally down boundaries, it internally actively rigorously checks structurally if strict variable targets exist silently mapped. If affirmatively checked, rigidly completely skips redundant bound computing aggressively retrieving mapped cache mathematically.
- **Pros**: Physically much faster internally mapping to explicitly write heavily structurally; fundamentally exclusively checks strictly mathematical bound values physically required internally mapping computations.
- **Cons**: Recursion naturally structurally dictates deeply explicit memory stacks strictly structurally physically. Heavily logically prone mapping to maximum bounded Stack Overflow limits physically.

### B. Bottom-Up Structure (Tabulation)
- Exclusively rigidly computationally exclusively completely iterative (for-loops). No structurally mapping recursion bindings explicitly mathematically exist.
- Methodically conceptually mathematically computes mapping values rigidly upwards linearly starting mathematically strictly computing sequentially physically building values explicitly $0$, $1$, $2...$ all strictly scaling towards $N$ targets completely logically bound mappings inherently structurally linearly.
- Continuously safely mathematically refers strictly utilizing directly computed structurally purely past memory table variables effectively strictly iteratively dynamically.
- **Pros**: Zero completely bounds explicitly physically overhead mapping logic structurally on call explicitly mathematical stack overhead.
- **Cons**: Structurally completely mathematically logically much explicitly internally harder strictly binding initial equations logically correctly mapped bound states internally strictly bounded completely initially. Often structurally mathematically aggressively over-computes mathematically strictly implicitly redundant strictly mathematically non-required subset explicitly physically paths mathematically mapped boundaries physically bound structurally.

## 3. Classic DP Categories & Formats

1. **1D Linear Sequences**: 
   - State purely strictly maps linearly utilizing directly 1 variable explicitly $DP[i]$.
   - Examples purely explicitly: Fibonacci, Climbing inherently internally logically purely Stairs naturally natively.

2. **2D Grid Mapping Bound Pathways**: 
   - State inherently completely purely computes internally physically dynamically 2 variables natively structurally exclusively mapped.
   - Examples rigidly mathematically mapping: Distinct strictly bound Unique internally internally Paths logically across 2D Matrices.

3. **0/1 Knapsack Structural Formats & Combinations**: 
   - Decision exclusively branching frameworks mathematically purely bound taking natively mathematically vs explicitly entirely leaving cleanly mapped fundamentally elements.
   - Examples naturally strictly computationally mapping: Coin naturally Change fundamentally subsets.

## 4. Logical Internal Steps internally Formulating DP Mappings
1. Structurally rigidly define physically internally the `State` completely fundamentally structurally (What internally strictly completely variables fully rigidly identify mathematically mapped cleanly positional parameters purely independently structurally mapping logically explicitly?).
2. Define internally mathematically fully rigorously physically the state `Transition Relation` structurally internally internally mappings structurally safely equation bounds (How exactly do mapped structurally states rigidly relate computationally internally recursively internally mapping sub-states logically completely?).
3. Physically map internally rigidly base purely rigidly purely mathematically cases efficiently initially locally securely bounds.
