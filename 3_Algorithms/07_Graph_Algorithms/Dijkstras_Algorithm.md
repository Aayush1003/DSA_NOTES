# Dijkstra's Algorithm

## Overview
Dijkstra's Algorithm is a greedy algorithm used to find the shortest path from a starting node to all other nodes in a weighted graph. It works for both directed and undirected graphs, provided that all edge weights are non-negative.

## Characteristics
- **Algorithm Type:** Greedy Algorithm.
- **Constraints:** Does **not** work with graphs containing negative edge weights. If a graph has negative edges, algorithms like Bellman-Ford should be used.
- **Primary Data Structure:** A Min-Priority Queue (usually implemented using a Min-Heap) is used to constantly fetch the current cheapest node to visit.

## How it Works
1. Initialize the shortest distance to all nodes as infinity (`∞`), except for the starting node, which is initialized to `0`.
2. Insert the starting node into a Min-Priority Queue.
3. While the priority queue is not empty:
   - Extract the node `u` with the minimum distance.
   - For every adjacent neighbor `v` of `u`:
     - Calculate the new proposed distance to `v`: `new_dist(start, v) = dist(start, u) + weight(u, v)`.
     - If `new_dist` is less than the currently recorded distance to `v`, update the distance to `v` and insert/update `v` in the Priority Queue.

## Python Implementation
```python
import heapq

def dijkstra(graph, start):
    """
    graph is an adjacency list format: {node: [(neighbor, weight), ...]}
    """
    # 1. Initialize distances
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    
    # Priority queue to store pairs of (distance, vertex)
    pq = [(0, start)]
    
    while pq:
        current_distance, current_node = heapq.heappop(pq)
        
        # Optimization: We might have multiple entries for the same node in pq.
        # If we got a longer distance than what's currently recorded, skip it.
        if current_distance > distances[current_node]:
            continue
            
        # Explore neighbors
        for neighbor, weight in graph[current_node]:
            distance = current_distance + weight
            
            # If we found a shorter path to neighbor
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))
                
    return distances
```

## Space and Time Complexity
- **Time Complexity:** `O(V + E \log V)` where `V` is the number of vertices and `E` is the number of edges. This assumes an adjacency list representation and a binary heap for the priority queue.
- **Space Complexity:** `O(V)` to store distances and the priority queue.
