# [Number of Ways to Arrive at Destination](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/description/)

## Problem Statement
- You are in a city that consists of `n` intersections numbered from `0` to `n - 1` with bi-directional roads between some intersections. The inputs are generated such that you can reach any intersection from any other intersection and that there is at most one road between any two intersections.
- You are given an integer n and a 2D integer array roads where `roads[i] = [ui, vi, timei]` means that there is a road between intersections `ui` and `vi` that takes `timei` minutes to travel. You want to know in how many ways you can travel from intersection `0` to intersection `n - 1` in the shortest amount of time.
- Return the number of ways you can arrive at your destination in the shortest amount of time. Since the answer may be large, return it modulo `10^9 + 7`.



## Constraints
- 1 <= n <= 200
- n - 1 <= roads.length <= n * (n - 1) / 2
- roads[i].length == 3
- 0 <= ui, vi <= n - 1
- 1 <= timei <= 10<sup>9</sup>
- ui != vi
- There is at most one road connecting any two intersections.
- You can reach any intersection from any other intersection.




## Test Cases
1. **Input:** n = 7, roads = \[[0,6,7],[0,1,2],[1,2,3],[1,3,3],[6,3,3],[3,5,1],[6,5,1],[2,5,1],[0,4,5],[4,6,2]]<br>
**Output:** 4
2. **Input:** n = 2, roads = \[[1,0,10]]<br>
**Output:** 1




## Approach / Intuition 
- Using the **Dijkstra's algorithm**. 
- Maintain a `distance` array to track the minimum distance to each node.
- Use a `path` array to count the number of ways to reach each node with the shortest path.
- Update the `path` array when another shortest path to a node is found.




## Algorithm 
1. Build the graph as an adjacency list with nodes and edge weights.
2. Initialize `distance` to infinity and path to `0` for all nodes; set `distance[0] = 0` and `path[0] = 1`.
3. Use a priority queue to process nodes in order of their current shortest distance.
4. Relax edges: update `distance` and `path` for neighbors if a shorter or equal path is found.
5. Return `path[n-1]` as the number of shortest paths to the target node.




## Complexity
##### Time Complexity
- \(O((E+V)logV)\)
##### Space Complexity
- \(O(V+E)\)




## Code
```cpp
class Solution {
public:
    int countPaths(int n, vector<vector<int>>& roads) {
        int mod = 1e9 + 7;
        vector<vector<pair<int, int>>> graph(n);
        for (auto& road : roads) {
            graph[road[0]].push_back({road[1], road[2]});
            graph[road[1]].push_back({road[0], road[2]});
        }
        vector<long long> distance(n, LONG_MAX);
        vector<int> path(n, 0);
        priority_queue<pair<long long, int>, vector<pair<long long, int>>, greater<pair<long long, int>>>pq;
        pq.push({0, 0});
        distance[0] = 0;
        path[0] = 1;
        while (!pq.empty()) {
            auto t = pq.top();
            pq.pop();
            for (auto& nbr : graph[t.second]) {
                long long vert = nbr.first;
                long long edge = nbr.second;
                if (distance[vert] > distance[t.second] + edge) {
                    distance[vert] = distance[t.second] + edge;
                    pq.push({distance[vert], vert});
                    path[vert] = path[t.second] % mod;
                } else if (distance[vert] == t.first + edge) {
                    path[vert] += path[t.second];
                    path[vert] %= mod;
                }
            }
        }
        return path[n - 1];
    }
};
```     