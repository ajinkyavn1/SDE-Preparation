# ================================
# GRAPH MASTER TEMPLATE (C++)
# ================================

#include <bits/stdc++.h>
using namespace std;

# ================================
# 1. BFS (Unweighted Graph)
# ================================

vector<int> bfs(int V, vector<vector<int>>& adj, int start) {
    vector<int> dist(V, -1);
    queue<int> q;

    q.push(start);
    dist[start] = 0;

    while (!q.empty()) {
        int node = q.front(); q.pop();

        for (int nei : adj[node]) {
            if (dist[nei] == -1) {
                dist[nei] = dist[node] + 1;
                q.push(nei);
            }
        }
    }
    return dist;
}

# ================================
# 2. DFS (Recursive)
# ================================

void dfs(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;

    for (int nei : adj[node]) {
        if (!visited[nei]) {
            dfs(nei, adj, visited);
        }
    }
}

# ================================
# 3. Cycle Detection (Undirected)
# ================================

bool dfsCycle(int node, int parent,
              vector<vector<int>>& adj,
              vector<bool>& visited) {

    visited[node] = true;

    for (int nei : adj[node]) {
        if (!visited[nei]) {
            if (dfsCycle(nei, node, adj, visited))
                return true;
        }
        else if (nei != parent) {
            return true;
        }
    }
    return false;
}

# ================================
# 4. Cycle Detection (Directed)
# ================================

bool dfsDirected(int node,
                 vector<vector<int>>& adj,
                 vector<int>& visited,
                 vector<int>& pathVisited) {

    visited[node] = 1;
    pathVisited[node] = 1;

    for (int nei : adj[node]) {
        if (!visited[nei]) {
            if (dfsDirected(nei, adj, visited, pathVisited))
                return true;
        }
        else if (pathVisited[nei]) {
            return true;
        }
    }

    pathVisited[node] = 0;
    return false;
}

# ================================
# 5. Topological Sort (Kahn's)
# ================================

vector<int> topoSort(int V, vector<vector<int>>& adj) {
    vector<int> indegree(V, 0);

    for (int i = 0; i < V; i++)
        for (int nei : adj[i])
            indegree[nei]++;

    queue<int> q;
    for (int i = 0; i < V; i++)
        if (indegree[i] == 0)
            q.push(i);

    vector<int> topo;

    while (!q.empty()) {
        int node = q.front(); q.pop();
        topo.push_back(node);

        for (int nei : adj[node]) {
            indegree[nei]--;
            if (indegree[nei] == 0)
                q.push(nei);
        }
    }
    return topo;
}

# ================================
# 6. Dijkstra (Min Heap)
# ================================

vector<int> dijkstra(int V,
                     vector<vector<pair<int,int>>>& adj,
                     int src) {

    vector<int> dist(V, INT_MAX);
    priority_queue<pair<int,int>,
                   vector<pair<int,int>>,
                   greater<pair<int,int>>> pq;

    dist[src] = 0;
    pq.push({0, src});

    while (!pq.empty()) {
        auto [d, node] = pq.top(); pq.pop();

        if (d > dist[node]) continue;

        for (auto [nei, wt] : adj[node]) {
            if (dist[node] + wt < dist[nei]) {
                dist[nei] = dist[node] + wt;
                pq.push({dist[nei], nei});
            }
        }
    }
    return dist;
}

# ================================
# 7. Bellman-Ford
# ================================

vector<int> bellmanFord(int V,
                        vector<vector<int>>& edges,
                        int src) {

    vector<int> dist(V, INT_MAX);
    dist[src] = 0;

    for (int i = 0; i < V-1; i++) {
        for (auto& e : edges) {
            int u = e[0], v = e[1], wt = e[2];

            if (dist[u] != INT_MAX &&
                dist[u] + wt < dist[v]) {
                dist[v] = dist[u] + wt;
            }
        }
    }
    return dist;
}

# ================================
# 8. Union Find (DSU)
# ================================

class DSU {
public:
    vector<int> parent, rank;

    DSU(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    void unite(int x, int y) {
        int px = find(x);
        int py = find(y);

        if (px == py) return;

        if (rank[px] < rank[py])
            parent[px] = py;
        else if (rank[px] > rank[py])
            parent[py] = px;
        else {
            parent[py] = px;
            rank[px]++;
        }
    }
};

# ================================
# 9. Kruskal (MST)
# ================================

int kruskal(int V,
            vector<vector<int>>& edges) {

    sort(edges.begin(), edges.end(),
         [](auto &a, auto &b){
            return a[2] < b[2];
         });

    DSU dsu(V);
    int mstWeight = 0;

    for (auto& e : edges) {
        int u = e[0], v = e[1], wt = e[2];

        if (dsu.find(u) != dsu.find(v)) {
            mstWeight += wt;
            dsu.unite(u, v);
        }
    }
    return mstWeight;
}

# ================================
# 10. Prim (MST)
# ================================

int prim(int V,
         vector<vector<pair<int,int>>>& adj) {

    vector<bool> inMST(V, false);
    priority_queue<pair<int,int>,
                   vector<pair<int,int>>,
                   greater<pair<int,int>>> pq;

    pq.push({0, 0});
    int mstWeight = 0;

    while (!pq.empty()) {
        auto [wt, node] = pq.top(); pq.pop();

        if (inMST[node]) continue;
        inMST[node] = true;
        mstWeight += wt;

        for (auto [nei, w] : adj[node]) {
            if (!inMST[nei]) {
                pq.push({w, nei});
            }
        }
    }
    return mstWeight;
}

# ================================
# 11. 0-1 BFS
# ================================

vector<int> zeroOneBFS(int V,
                       vector<vector<pair<int,int>>>& adj,
                       int src) {

    deque<int> dq;
    vector<int> dist(V, INT_MAX);

    dist[src] = 0;
    dq.push_front(src);

    while (!dq.empty()) {
        int node = dq.front(); dq.pop_front();

        for (auto [nei, wt] : adj[node]) {
            if (dist[node] + wt < dist[nei]) {
                dist[nei] = dist[node] + wt;

                if (wt == 1)
                    dq.push_back(nei);
                else
                    dq.push_front(nei);
            }
        }
    }
    return dist;
}
