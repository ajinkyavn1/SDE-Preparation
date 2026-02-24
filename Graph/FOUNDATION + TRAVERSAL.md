# GRAPH REVISION NOTES

---

# 1. Graph Basics

## Definition
A graph consists of:
- V vertices (nodes)
- E edges (connections)

Graph can be:
- Directed / Undirected
- Weighted / Unweighted
- Cyclic / Acyclic
- Connected / Disconnected

---

# 2. Graph Representation

## 2.1 Adjacency Matrix

Representation:
matrix[V][V]

Space Complexity:
O(V^2)

When to use:
- Dense graph (E ≈ V^2)
- Fast edge lookup needed

Edge Check:
O(1)

Drawback:
Memory heavy for sparse graphs

---

## 2.2 Adjacency List

Representation:
Array/List of lists

Space Complexity:
O(V + E)

When to use:
- Sparse graphs
- Most interview problems

Edge Check:
O(degree)

Preferred in interviews

---

# 3. Graph Traversal

Traversal = visiting all vertices

Two main methods:
- BFS
- DFS

---

# 4. Breadth First Search (BFS)

## Idea
Level-by-level traversal using Queue

## Used For
- Shortest path (unweighted)
- Multi-source BFS
- Bipartite check
- Grid problems

## Time Complexity
O(V + E)

## Space Complexity
O(V)

## Core Pattern
1. Push source to queue
2. Mark visited
3. While queue not empty:
    - Pop
    - Traverse neighbors
    - If not visited → push

---

# 5. Depth First Search (DFS)

## Idea
Go deep before going wide

Implemented via:
- Recursion
- Stack

## Used For
- Cycle detection
- Topological sort
- Connected components
- Bridges / SCC

## Time Complexity
O(V + E)

## Space Complexity
O(V) recursion stack

---

# 6. Connected Components

Definition:
Number of isolated subgraphs

Method:
Run DFS/BFS from every unvisited node

Time Complexity:
O(V + E)

---

# 7. Important Complexity Rule (VERY IMPORTANT)

For adjacency list:
Most graph algorithms run in:

O(V + E)

Remember:
Each vertex visited once
Each edge processed once

This dominates almost all graph problems.
