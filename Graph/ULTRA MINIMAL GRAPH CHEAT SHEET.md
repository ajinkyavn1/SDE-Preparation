

# GRAPH CHEAT SHEET (INTERVIEW COMPRESSION)

==============================
CORE RULE
==============================

Adj List → Space O(V + E)
Most Graph Algorithms → O(V + E)

==============================
TRAVERSAL
==============================

BFS → O(V + E)
Use for:
- Unweighted shortest path
- Multi-source problems
- Grid shortest distance

DFS → O(V + E)
Use for:
- Cycle detection
- Components
- Bridges / SCC

==============================
CYCLE
==============================

Undirected:
DFS + parent check

Directed:
DFS + recursion stack
OR
Topo (Kahn) → if size < V → cycle

==============================
TOPOLOGICAL SORT (DAG)
==============================

Kahn (BFS) → O(V + E)
DFS + stack → O(V + E)

Use when:
- Dependencies
- Order of tasks
- Course schedule

==============================
SHORTEST PATH
==============================

Unweighted → BFS → O(V + E)

Positive weights → Dijkstra → O(E log V)

Negative weights → Bellman-Ford → O(VE)

All pairs → Floyd Warshall → O(V^3)

0/1 weights → 0-1 BFS → O(V + E)

==============================
MST
==============================

Kruskal → O(E log E)
(Edge list + DSU)

Prim → O(E log V)
(Adj list + heap)

==============================
CONNECTIVITY
==============================

Static → DFS/BFS
Dynamic → DSU

==============================
ADVANCED
==============================

SCC → Kosaraju / Tarjan → O(V + E)

Bridges → low[] > disc[]

Articulation → low[] >= disc[]

==============================
DECISION TREE
==============================

Weighted?
    No → BFS / DFS
    Yes →
        Negative? → Bellman
        Positive? → Dijkstra

Need order? → Topo
Need min connect? → MST
Need grouping? → DSU
Grid? → BFS/DFS