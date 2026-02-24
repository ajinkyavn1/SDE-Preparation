# GRAPH REVISION NOTES (Part 3)

==================================================
13. Shortest Path Algorithms
==================================================

--------------------------------------------
13.1 BFS (Unweighted Graph)
--------------------------------------------

Use When:
Edges have equal weight (or weight = 1)

Idea:
Level order traversal gives shortest distance

Time Complexity:
O(V + E)

Space:
O(V)

Very Important:
BFS guarantees shortest path ONLY in unweighted graph


--------------------------------------------
13.2 Dijkstra’s Algorithm
--------------------------------------------

Use When:
Positive weighted graph

Data Structure:
Min Heap / Priority Queue

Idea:
Greedy — always expand smallest distance node

Time Complexity:
Using Min Heap:
O((V + E) log V)

Space:
O(V)

Important:
Does NOT work with negative weights


--------------------------------------------
13.3 Bellman-Ford
--------------------------------------------

Use When:
Graph may contain negative weights

Idea:
Relax all edges V-1 times

Why V-1?
Shortest path can have at most V-1 edges

Time Complexity:
O(V * E)

Space:
O(V)

Bonus:
Can detect negative cycle
If relaxation still possible in Vth iteration → negative cycle


--------------------------------------------
13.4 Floyd-Warshall
--------------------------------------------

Use When:
All-pairs shortest path

Idea:
Dynamic Programming
Try every node as intermediate

Time:
O(V^3)

Space:
O(V^2)

Used when:
V is small (≈ 200 or less)

==================================================
14. Minimum Spanning Tree (MST)
==================================================

Definition:
Tree connecting all vertices
With minimum total edge weight

Works only for:
Connected, Undirected, Weighted graph

--------------------------------------------
14.1 Kruskal’s Algorithm
--------------------------------------------

Approach:
Greedy — pick smallest edge first

Steps:
1. Sort edges by weight
2. Use DSU to avoid cycles

Time Complexity:
Sorting edges → O(E log E)
DSU operations → O(E α(V))

Overall:
O(E log E)

Used When:
Graph is edge list format


--------------------------------------------
14.2 Prim’s Algorithm
--------------------------------------------

Approach:
Grow MST from starting node

Data Structure:
Min Heap

Time Complexity:
O((V + E) log V)

Better When:
Graph is adjacency list format

Difference from Dijkstra:
Dijkstra → shortest path
Prim → minimum spanning tree

==================================================
15. Comparison Table (High Retention Section)
==================================================

Unweighted Shortest Path → BFS → O(V + E)

Positive Weighted → Dijkstra → O(E log V)

Negative Weights → Bellman-Ford → O(VE)

All Pairs → Floyd Warshall → O(V^3)

MST Edge Based → Kruskal → O(E log E)

MST Node Based → Prim → O(E log V)

==================================================
16. Critical Interview Observations
==================================================

1. BFS ≠ Dijkstra
   BFS only works for equal weights

2. If weights are 0 and 1:
   Use 0-1 BFS (Deque)
   Time → O(V + E)

3. If graph is dense:
   E ≈ V^2
   Dijkstra becomes O(V^2 log V)

4. Bellman-Ford is rarely optimal
   Use only when negative edges exist

==================================================
MEMORY MAP
==================================================

Traversal Family → O(V + E)

Shortest Path:
BFS → O(V + E)
Dijkstra → O(E log V)
Bellman → O(VE)
Floyd → O(V^3)

MST:
Kruskal → O(E log E)
Prim → O(E log V)
