# [Network Delay Time](https://leetcode.com/problems/network-delay-time/description/)

## Problem Statement
- You are given a network of `n` nodes, labeled from `1` to `n`. You are also given times, a list of travel `time`s as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.
- We will send a signal from a given node `k`. Return the minimum time it takes for all the `n` nodes to receive the signal. If it is impossible for all the `n` nodes to receive the signal, return `-1`.




## Constraints
- 1 <= k <= n <= 100
- 1 <= times.length <= 6000
- times[i].length == 3
- 1 <= ui, vi <= n
- ui != vi
- 0 <= wi <= 100
- All the pairs (ui, vi) are unique. (i.e., no multiple edges.)




## Test Cases
1. **Input:** times = \[[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2 <br>
**Output:** 2
2. **Input:** times = \[[1,2,1]], n = 2, k = 1 <br>
**Output:** 1
3. **Input:** times = \[[1,2,1]], n = 2, k = 2 <br>
**Output:** -1




## Approach / Intuition 
- Using **BFS Algorithm**.
- The graph is represented as an adjacency list, `adj`, where each node points to a list of pairs `(time,neighbour)`.
- Each node is visited and shortest path is calculated.
- If maximum value of the `vis` is `INT_MAX` then answer is not possible so return `-1`.





## Algorithm 
1. Construct the adjacency list `adj`.
2. The `vis` array is used to keep track of the shortest time to reach each node. It is initialized with `INT_MAX`.
3. Starting from the given node `k`, the algorithm explores all reachable nodes.
4. For each neighbor of the current node, the algorithm calculates the "arrival time" based on the weight of the edge. If a shorter path to a neighbor is found, the `vis` array is updated, and the neighbor is added to the queue.
5. After traversal, the maximum time across all reachable nodes is computed.




## Complexity
##### Time Complexity
- \(O(V+E)\)
##### Space Complexity
- \(O(V+E)\)




## Code
```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<vector<pair<int, int>>> adj(n + 1);
        for (auto i : times)
            adj[i[0]].push_back({i[2], i[1]});
        vector<int> vis(n + 1, INT_MAX);
        queue<int> q;
        q.push(k);
        vis[k] = 0;
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            for (auto i : adj[node]) {
                int time = i.first;
                int neighbour = i.second;
                int arrival = vis[node] + time;
                if (vis[neighbour] > arrival) {
                    vis[neighbour] = arrival;
                    q.push(neighbour);
                }
            }
        }
        int ans = INT_MIN;
        for (int i = 1; i <= n; i++)
            ans = max(ans, vis[i]);
        return ans == INT_MAX ? -1 : ans;
    }
};
```