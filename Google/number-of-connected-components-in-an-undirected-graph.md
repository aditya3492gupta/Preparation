# [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/)

## Problem Statement
- You have a graph of `n` nodes. You are given an integer `n` and an array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between `ai and bi` in the graph.
- Return the *number of connected components* in the graph.
    


## Constraints
- 1 <= n <= 2000
- 1 <= edges.length <= 5000
- edges[i].length == 2
- 0 <= a<sub>i</sub> <= b<sub>i</sub> < n
- a<sub>i</sub> != b<sub>i</sub>
- There are no repeated edges.



## Test Cases
1. **Input:** n = 5, edges = \[[0,1],[1,2],[3,4]] <br>
**Output:** 2
2. **Input:** n = 5, edges = \[[0,1],[1,2],[2,3],[3,4]]<br>
**Output:** 1

## Approach / Intuition 
- Using the **DFS** for searching the number of components.
- Visit each unvisited node and mark them visited with all the nodes connected to it.

## Algorithm 
1. Create an adjacency list `adjList` to represent the graph, and a `visited` array initialized to 0 to track visited nodes.
2. Populate `adjList` by iterating over `edges` and adding connections between nodes.
3. Implement a depth-first search (DFS) helper function to mark all nodes reachable from a given source as visited.
4. Traverse each node; if it is unvisited, increment `components` and run DFS from that node to mark all reachable nodes.
5. After visiting all nodes, return the total count of connected components.

## Complexity
##### Time Complexity
- \(O(V + E)\)
##### Space Complexity
- \(O(V)\)

## Code
```cpp
class Solution {
public:
    void dfs(vector<int> adjList[], vector<int> &visited, int src) {
        visited[src] = 1;
        for (int i = 0; i < adjList[src].size(); i++) {
            if (visited[adjList[src][i]] == 0) {
                dfs(adjList, visited, adjList[src][i]);
            }
        }
    }
    
    int countComponents(int n, vector<vector<int>>& edges) {
        if (n == 0) 
            return 0;
        int components = 0;
        vector<int> visited(n, 0);
        vector<int> adjList[n];
        for (int i = 0; i < edges.size(); i++) {
            adjList[edges[i][0]].push_back(edges[i][1]);
            adjList[edges[i][1]].push_back(edges[i][0]);
        }
        for (int i = 0; i < n; i++) {
            if (visited[i] == 0) {
                components++;
                dfs(adjList, visited, i);
            }
        }
        return components;
    }
};
```     