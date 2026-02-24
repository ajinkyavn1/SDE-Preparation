# GRAPH REVISION NOTES (Part 4 - Advanced)

==================================================
17. Strongly Connected Components (SCC)
==================================================

Definition:
In directed graph,
Every node reachable from every other node in the component.

--------------------------------------------
17.1 Kosaraju’s Algorithm
--------------------------------------------

Steps:
1. DFS and push nodes by finish time (Topo order)
2. Reverse all edges
3. DFS in reverse order of stack

Time Complexity:
O(V + E)

Space:
O(V)

--------------------------------------------
17.2 Tarjan’s Algorithm
--------------------------------------------

Single DFS
Uses:
- Discovery time
- Low-link value
- Stack

Time:
O(V + E)

More optimal than Kosaraju in practice

==================================================
18. Bridges in Graph
==================================================

Definition:
Edge whose removal increases number of components

Condition:
If low[neighbor] > disc[node]
→ edge is bridge

Time:
O(V + E)

Used in:
Network reliability problems

==================================================
19. Articulation Points
==================================================

Definition:
Node whose removal disconnects graph

Condition:
1. Root with >1 children
2. low[child] >= disc[node]

Time:
O(V + E)

==================================================
20. 0-1 BFS
==================================================

Use When:
Edge weights are only 0 or 1

Data Structure:
Deque

Rule:
Weight 0 → push front
Weight 1 → push back

Time:
O(V + E)

Faster than Dijkstra here

==================================================
21. Multi-Source BFS
==================================================

Idea:
Push all sources initially into queue

Used in:
- Rotting oranges
- Nearest distance problems
- Grid shortest path

Time:
O(V + E)

==================================================
22. Graph in Grid Problems
==================================================

Grid treated as graph:
Each cell = node
Edges = 4-direction or 8-direction

Common Patterns:
- Number of islands
- Shortest path in matrix
- Flood fill
- Rotten oranges

Time:
O(N * M)

Space:
O(N * M)

==================================================
23. Topological Sort + DP
==================================================

Used in:
- Longest path in DAG
- Course schedule variations
- Count paths in DAG

Idea:
1. Topo sort
2. Process nodes in order
3. Apply DP

Time:
O(V + E)

==================================================
24. Complete Complexity Master Table
==================================================

Traversal:
BFS / DFS → O(V + E)

Cycle Detection → O(V + E)

Topo Sort → O(V + E)

Bipartite → O(V + E)

Dijkstra → O(E log V)

Bellman-Ford → O(VE)

Floyd-Warshall → O(V^3)

Kruskal → O(E log E)

Prim → O(E log V)

SCC → O(V + E)

Bridges / Articulation → O(V + E)

0-1 BFS → O(V + E)

Grid Graph → O(NM)

==================================================
25. Google Interview Insights
==================================================

1. Most problems reduce to:
   - BFS
   - DFS
   - Dijkstra
   - Topo + DP

2. Always identify:
   - Weighted / Unweighted?
   - Directed / Undirected?
   - Need shortest path or connectivity?

3. If constraints:
   V ≤ 10^5, E ≤ 2*10^5
   → O(V + E) or O(E log V) only

4. If V ≤ 200
   → Floyd Warshall possible

5. Think in patterns:
   - Island problems → DFS/BFS
   - Dependency problems → Topo
   - Connectivity dynamic → DSU
   - Minimum cost connect → MST

==================================================
FINAL MEMORY ANCHOR
==================================================

Most graph algorithms:
O(V + E)

Weighted shortest:
Dijkstra → O(E log V)

Negative weight:
Bellman → O(VE)

All pairs:
Floyd → O(V^3)

MST:
Kruskal / Prim
