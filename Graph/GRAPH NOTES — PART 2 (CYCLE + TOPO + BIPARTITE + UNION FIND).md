# GRAPH REVISION NOTES (Part 2)

---

# 8. Cycle Detection

--------------------------------------------------
8.1 Cycle Detection in Undirected Graph
--------------------------------------------------

Method 1: DFS with Parent Tracking

Idea:
If a visited neighbor is not the parent → cycle exists

Time Complexity:
O(V + E)

Space Complexity:
O(V)

Common Trap:
For undirected graph always pass parent node


Method 2: BFS with Parent Tracking

Same logic using queue

Time Complexity:
O(V + E)

---

--------------------------------------------------
8.2 Cycle Detection in Directed Graph
--------------------------------------------------

Method 1: DFS + Recursion Stack

Maintain:
- visited[]
- pathVisited[] (recursion stack)

If during DFS:
Neighbor already in pathVisited → cycle

Time Complexity:
O(V + E)

Space Complexity:
O(V)

---

Method 2: Kahn’s Algorithm (BFS / Topo Based)

If Topological Sort does NOT include all vertices
→ cycle exists

Time Complexity:
O(V + E)

---

# 9. Topological Sort (DAG Only)

Definition:
Linear ordering of vertices such that
u → v means u comes before v

Works only for Directed Acyclic Graph (DAG)

--------------------------------------------------
9.1 DFS Based Topo
--------------------------------------------------

Idea:
Push node to stack after DFS finishes

Reverse stack = Topo order

Time:
O(V + E)

Space:
O(V)

--------------------------------------------------
9.2 Kahn’s Algorithm (BFS Based)
--------------------------------------------------

Steps:
1. Compute indegree of all nodes
2. Push nodes with indegree = 0 into queue
3. Process and reduce indegree

Time:
O(V + E)

Space:
O(V)

Google Favorite Variation:
Topo + DP on DAG

---

# 10. Bipartite Graph

Definition:
Graph that can be colored using 2 colors
such that no adjacent nodes share same color

Method:
BFS or DFS with coloring

If neighbor has same color → not bipartite

Time:
O(V + E)

Space:
O(V)

Used in:
- Graph coloring problems
- Checking odd length cycle

Key Insight:
Odd cycle ⇒ Not bipartite

---

# 11. Union Find (Disjoint Set Union - DSU)

Used For:
- Detect cycle in undirected graph
- Kruskal MST
- Dynamic connectivity

Core Operations:

1. Find(x)
   Returns root parent

2. Union(x, y)
   Merge two sets

Optimizations:
- Path Compression
- Union by Rank / Size

Time Complexity:
Nearly O(1)
More precisely: O(α(N)) (Inverse Ackermann)

---

Cycle Detection using DSU:

For each edge:
If Find(u) == Find(v)
→ cycle exists
Else Union(u, v)

Time:
O(E * α(V))

---

# 12. Complexity Pattern Summary

Adj List Graph:
Most algorithms → O(V + E)

DSU:
Almost constant per operation

Topo / Cycle / Bipartite:
All O(V + E)

---

# Memory Trick

Traversal Family → O(V + E)
DSU → ~O(1)
Matrix → O(V²)
