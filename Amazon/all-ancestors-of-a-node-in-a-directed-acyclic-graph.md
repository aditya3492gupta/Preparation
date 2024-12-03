# [All Ancestors of a Node in a Directed Acyclic Graph](https://leetcode.com/problems/all-ancestors-of-a-node-in-a-directed-acyclic-graph/description/)

## Problem Statement
- You are given a positive integer `n` representing the number of nodes of a Directed Acyclic Graph (DAG). The nodes are numbered from `0` to `n - 1` (inclusive).
- You are also given a 2D integer array `edges`, where `edges[i] = [fromi, toi]` denotes that there is a unidirectional edge from `fromi` to `toi` in the graph.
- Return a list `answer`, where `answer[i]` is the list of ancestors of the `ith` node, sorted in ascending order.
- A node `u` is an ancestor of another node `v` if `u` can reach `v` via a set of edges.




## Test Cases
1. **Input:**  n = 8, edgeList = \[[0,3],[0,4],[1,3],[2,4],[2,7],[3,5],[3,6],[3,7],[4,6]] <br>
**Output:** \[[],[],[],[0,1],[0,2],[0,1,3],[0,1,2,3,4],[0,1,2,3]]
2. **Input:** n = 5, edgeList = \[[0,1],[0,2],[0,3],[0,4],[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]] <br>
**Output:** \[[],[0],[0,1],[0,1,2],[0,1,2,3]]






## Constraints
- 1 <= n <= 1000
- 0 <= edges.length <= min(2000, n * (n - 1) / 2)
- edges[i].length == 2
- 0 <= fromi, toi <= n - 1
- fromi != toi
- There are no duplicate edges.
- The graph is directed and acyclic.



## Approach / Intuition 
- Using **Topological Sort**.
- Calculate the `indegree` of all the nodes.
- Add all the nodes that are reachable to the current node.
- If the current node is present in the set then push it to `ans`.





## Algorithm 
1. Construct a adjacency list `adj` and `indegree` of the current DAG.
2. Push the nodes in `q` with `indegree == 0`.
3. Use the `topological sort` and store the nodes in `order` given after sorting.
4. Insert the nodes and all the other reachable nodes to the `ans_list`.
5. Iterating over each node and checking its presence in `ans_list`.
6. If present, insert it in `ans`.






## Complexity
##### Time Complexity
- \(O(N^2)\)
##### Space Complexity
- \(O(N^2)\)




## Code
```cpp
class Solution {
public:
    vector<vector<int>> getAncestors(int n, vector<vector<int>>& edges) {
        vector<vector<int>> ans(n);
        vector<vector<int>> adj(n);
        vector<int> indegree(n, 0);
        for (auto i : edges) {
            adj[i[0]].push_back(i[1]);
            indegree[i[1]]++;
        }
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0)
                q.push(i);
        }
        vector<int> order;
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            order.push_back(node);
            for (auto i : adj[node]) {
                indegree[i]--;
                if (indegree[i] == 0) {
                    q.push(i);
                }
            }
        }
        vector<unordered_set<int>> ans_list(n);
        for (auto i : order) {
            for (auto j : adj[i]) {
                ans_list[j].insert(i);
                ans_list[j].insert(ans_list[i].begin(), ans_list[i].end());
            }
        }
        for (int i = 0; i < ans.size(); i++) {
            for (int j = 0; j < n; j++) {
                if (i == j)
                    continue;
                if (ans_list[i].find(j) != ans_list[i].end())
                    ans[i].push_back(j);
            }
        }
        return ans;
    }
};
```     