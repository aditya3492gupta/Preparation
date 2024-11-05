# [Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/description/)



## Problem Statement
- There is an **undirected graph** with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:
    - There are no self-edges (`graph[u]` does not contain `u`).
    - There are no parallel edges (`graph[u]` does not contain duplicate values).
    - If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
    - The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.
- A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that every edge in the graph connects a node in set `A` and a node in set `B`.
- Return `true` if and only if it is **bipartite**.




## Constraints
- graph.length == n
- 1 <= n <= 100
- 0 <= graph[u].length < n
- 0 <= graph[u][i] <= n - 1
- graph[u] does not contain u.
- All the values of graph[u] are unique.
- If graph[u] contains v, then graph[v] contains u.




## Test Cases
1. **Input:** graph = \[[1,2,3],[0,2],[0,1,3],[0,2]] <br>
**Output:** false
2. **Input:** graph = \[[1,3],[0,2],[1,3],[0,2]]<br>
**Output:** true




## Approach / Intuition 
- Using the **DFS algorithm**.
- The graph is represented as an adjacency list, where each node points to its connected neighbors.
- Each node is assigned one of two colors (0 or 1) to differentiate between two sets, ensuring adjacent nodes have different colors.
- If a neighboring node is already colored with the same color as the current node, the graph is not bipartite, and the function returns false
- The process continues until all nodes are checked; if no conflicts are found, the graph is confirmed as bipartite.




## Algorithm 
1.  Create a color vector initialized to -1 for all vertices, indicating that no vertex has been colored yet.
2. For each vertex in the graph, check if it has been colored; if not, initiate a DFS from that vertex.
3. In the DFS, assign the current node a color and recursively color its uncolored neighbors with the opposite color.
4. During the DFS, if an adjacent node is already colored with the same color as the current node, return false, indicating the graph is not bipartite.
5. If all vertices are successfully colored without conflicts, return true, confirming that the graph is bipartite.




## Complexity
##### Time Complexity
- \(O(V + E)\)
##### Space Complexity
- \(O(V)\)




## Code
```cpp
class Solution {
public:
    bool dfs(vector<vector<int>> &graph, vector<int> &color, int node, int col){
        color[node] = col;
        for(auto i : graph[node]){
            if(color[i] == -1){
                if(!dfs(graph, color, i, !col))
                    return false;
            }
            else if(color[i] == col)
                return false;
        }
        return true;
    }
    bool isBipartite(vector<vector<int>>& graph) {
        int v = graph.size();
        vector<int> color(v, -1);
        for(int i = 0 ; i < v ; i++){
            if(color[i] == -1){
                if(!dfs(graph, color, i ,0))
                    return false;
            }
        }
        return true;
    }
};
```     