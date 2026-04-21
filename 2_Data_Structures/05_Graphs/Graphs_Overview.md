# Graphs

Graphs are the most versatile non-linear data structure, used to represent complex networks such as social networks, maps and routes, computer networks, and more. Physically, a Graph $G = (V, E)$ consisting of **Vertices (V)** (Nodes) and **Edges (E)** (Connections between nodes). 

*A Tree is technically a highly specific type of restricted graph that is connected and contains no cycles.*

## 1. Graph Terminology & Types
- **Directed Graph (Digraph)**: Edges have a strict one-way direction (A -> B). E.g., Follower model on Twitter.
- **Undirected Graph**: Edges are strictly bidirectional (A <-> B). E.g., Friendship on Facebook.
- **Weighted Graph**: Edges hold a numerical weight/cost representing distance, time, or cost.
- **Cyclic / Acyclic**: Whether a path exists that loops starting and ending at the exact same vertex.
- **DAG (Directed Acyclic Graph)**: Crucial in topological sorting (like task/build dependencies).

## 2. Graph Memory Representations

1. **Adjacency Matrix**: A 2D array of size $V \times V$ where `matrix[i][j]` is 1 (or the weight) if edge exists, 0 otherwise.
   - **Space Complexity**: $O(V^2)$.
   - **Pros**: $O(1)$ fast lookup to check if edge `A -> B` exists.
   - **Cons**: Severe memory waste for sparse graphs.

2. **Adjacency List**: An array (or map) of size $V$, where each vertex $V_i$ maps to a dynamic list representing the edges expanding outwards.
   - **Space Complexity**: $O(V + E)$.
   - **Pros**: Massively memory efficient for typical sparse graphs. Ideal for traversal algorithms.
   - **Cons**: Finding strict `A -> B` edge validation takes slightly longer ($O(Degree(A))$).

## 3. Core Graph Traversal Algorithms

### Breadth-First Search (BFS)
Explores graph uniformly in concentric outwardly circles (level by level).
- **Implementation**: Uses a **Queue**.
- **Important Uses**:
  - Finding the **Shortest Path** on an Unweighted Graph.
  - Doing layered/level-based analysis.
- **Time Complexity**: $O(V + E)$

### Depth-First Search (DFS)
Drills brutally deep down a singular path as far as possible before giving up and backtracking.
- **Implementation**: Uses a **Stack** (usually implicitly via recursion).
- **Important Uses**:
  - Checking general connectivity.
  - Detecting cycles in a graph.
  - Performing Topological Sort.
  - Solving mazes/puzzles.
- **Time Complexity**: $O(V + E)$

*(Note: Both traversals require maintaining a `visited` hashset/array to prevent infinite loops from cycles.)*

## 4. Advanced Graph Algorithms

Most graph problems boil down to picking the right advanced algorithm template.

### 1. Shortest Path (Weighted)
- **Dijkstra's Algorithm**: Finds the shortest path from a starting node to all other nodes. 
  - Cannot handle negative weights.
  - Uses a **Priority Queue (Min-Heap)**. Complexity primarily $O((V+E) \log V)$.
- **Bellman-Ford Algorithm**: Can handle negative weights and detect negative weight cycles. Computes primarily by loosening edges $V-1$ times. Complexity $O(V \times E)$.

### 2. Minimum Spanning Tree (MST)
Finding a subgraph that connects all vertices using the absolute minimum total edge weight.
- **Kruskal's Algorithm**: Sort edges by weight and union them greedily. (Relies heavily on Disjoint Set / Union Find). $O(E \log E)$.
- **Prim's Algorithm**: Builds the tree physically outwards from a start point greedily using a Priority Queue. $O((V+E) \log V)$.

### 3. Cycle Detection & Topo Sort
- **Topological Sorting**: Processing dependencies linearly $u \to v$. Only applies to DAGs (Directed Acyclic Graphs). Useful for resolving compile orders. Computed easily utilizing purely DFS or Kahn's Algorithm (BFS based).

## Deep Thought
Graphs often model system state spaces. Many logical problems can be mapped dynamically into Graphs. (e.g. Word Ladder, where words are purely nodes, and edges exist if letters differ by 1. Once conceptually modeled as a graph, resolving simply becomes running a BFS algorithm on it).
