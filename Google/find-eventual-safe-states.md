# [Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/description/)

## Problem Statement
- There is a directed graph of `n` nodes with each node labeled from `0` to `n - 1`. The graph is represented by a 0-indexed 2D integer array `graph` where `graph[i]` is an integer array of nodes adjacent to node `i`, meaning there is an edge from node `i` to each node in `graph[i]`.
- A node is a terminal node if there are no outgoing edges. A node is a safe node if every possible path starting from that node leads to a terminal node (or another safe node).
- Return an array containing all the safe nodes of the graph. The answer should be sorted in ascending order.


## Constraints
- n == graph.length
- 1 <= n <= 10<sup>4</sup>
- 0 <= graph[i].length <= n
- 0 <= graph[i][j] <= n - 1
- graph[i] is sorted in a strictly increasing order.
- The graph may contain self-loops.
- The number of edges in the graph will be in the range [1, 4 * 10<sup>4</sup>].


## Test Cases
1. **Input:** graph = \[[1,2],[2,3],[5],[0],[5],[],[]] <br>
**Output:** [2,4,5,6]
2. **Input:** graph = \[[1,2,3,4],[1,2],[3,4],[0,4],[]] <br>
**Output:** [4]

## Approach / Intuition 
- Using **topological sorting**.
- A node is "safe" if it is part of a terminal cycle (no outgoing paths) or if all its outgoing paths lead to safe nodes. 
- Reverse the graph's edges and focus on incoming connections to identify terminal nodes and propagate safety status backward.

## Algorithm 
1. Reverse the graph to create a new adjacency list `adj` where an edge points to the nodes that depend on it. Count the in-degrees for each node in the original graph `indegree`.
2. Nodes with `indegree == 0` are terminal. Push them into a queue.
3. Remove edges pointing to their dependencies (decrement `indegree`). Add nodes with `indegree == 0` to the queue. Mark nodes as safe.
4. Collect all nodes processed through the queue and sort them for output.

## Complexity
##### Time Complexity
- \(O(V+E+VlogV)\)
##### Space Complexity
- \(O(V+E)\)

## Code
```cpp
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        vector<int> ans;
        int n = graph.size();
        vector<int> indegree(n, 0);
        vector<vector<int>> adj(n);
        for (int i = 0; i < n; i++) {
            for (auto j : graph[i]) {
                adj[j].push_back(i);
                indegree[i]++;
            }
        }
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0)
                q.push(i);
        }
        while (!q.empty()) {
            int x = q.front();
            q.pop();
            ans.push_back(x);
            for (auto i : adj[x]) {
                indegree[i]--;
                if (indegree[i] == 0)
                    q.push(i);
            }
        }
        sort(ans.begin(), ans.end());
        return ans;
    }
};
```