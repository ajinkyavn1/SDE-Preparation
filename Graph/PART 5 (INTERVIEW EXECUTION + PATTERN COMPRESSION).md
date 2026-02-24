# GRAPH INTERVIEW EXECUTION NOTES

==================================================
26. How To Identify Graph Problems Fast
==================================================

If problem says:
- "connections"
- "network"
- "dependency"
- "shortest route"
- "minimum cost to connect"
- "islands"
- "courses"
- "accounts merge"

Think → Graph

==================================================
27. Decision Tree (VERY IMPORTANT)
==================================================

STEP 1: Is it weighted?

NO →
    Is shortest path needed?
        YES → BFS
        NO → DFS / BFS

YES →
    Are weights positive?
        YES → Dijkstra
        NO → Bellman-Ford

Are weights only 0 and 1?
    → 0-1 BFS

==================================================
28. Connectivity Problems
==================================================

Static connectivity:
    DFS / BFS

Dynamic connectivity:
    DSU (Union Find)

Check cycle:
    Undirected → DFS(parent) or DSU
    Directed → DFS(recStack) or Kahn

==================================================
29. Dependency / Ordering Problems
==================================================

Keywords:
- prerequisites
- order of tasks
- scheduling

→ Topological Sort

Need longest path in DAG?
→ Topo + DP

==================================================
30. Minimum Cost Connection
==================================================

Keywords:
- connect all nodes
- minimum cost
- network cable
- cities connection

→ MST

Edge list given?
→ Kruskal

Adj list given?
→ Prim

==================================================
31. Grid Problems Mapping
==================================================

2D matrix?
Treat as graph.

Connected regions?
→ DFS / BFS

Shortest steps?
→ BFS

Weighted cells?
→ Dijkstra

==================================================
32. Complexity Recognition Practice
==================================================

Constraints:
V ≤ 10^5
E ≤ 2*10^5
→ O(V + E) or O(E log V)

V ≤ 200
→ Floyd possible

E ≈ V^2
→ Dense graph
Matrix usable

==================================================
33. Common Google Graph Patterns
==================================================

1. Multi-source BFS
2. Shortest path with state
3. Topo + DP
4. Graph compression
5. Reversal graph trick
6. DSU for grouping problems
7. Dijkstra with modified states
8. Binary search + BFS
9. BFS in implicit graph
10. Build graph from constraints

==================================================
34. Mental Compression Sheet (MEMORIZE THIS)
==================================================

Traversal → O(V + E)

Unweighted shortest → BFS

Positive weighted shortest → Dijkstra

Negative edges → Bellman

All pairs → Floyd

Dependency → Topo

Minimum connect → MST

Dynamic connectivity → DSU

Grid → BFS/DFS

0-1 weight → 0-1 BFS
