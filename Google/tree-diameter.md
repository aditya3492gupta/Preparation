# [Tree Diameter](https://leetcode.com/problems/tree-diameter/description/)

## Problem Statement
- The **diameter** of a tree is **the number of edges** in the longest path in that tree.
- There is an undirected tree of `n` nodes labeled from `0` to `n - 1`. You are given a 2D array `edges` where `edges.length == n - 1` and `edges[i] = [ai, bi]` indicates that there is an undirected edge between nodes `ai` and `bi` in the tree.
- Return the **diameter** of the tree.




## Constraints
- n == edges.length + 1
- 1 <= n <= 10<sup>4</sup>
- 0 <= a<sub>i</sub>, b<sub>i</sub> < n
- a<sub>i</sub> != b<sub>i</sub>



## Test Cases
1. **Input:** edges = \[[0,1],[0,2]] <br>
**Output:** 2
2. **Input:** edges = \[[0,1],[1,2],[2,3],[1,4],[4,5]]<br>
**Output:** 4



## Approach / Intuition 
- Using **BFS algorithm**.
- For finding the **diameter** of a tree find the longest path between two node.
- Find the farthest node from `0`.
- From that node find the farthest node and return the distance between them.



## Algorithm 
1. Construct a adjacency list.
2. Declare a queue `q` and initialize a vector `vis` with initial value `0`.
3. Start **BFS** traversal from the node `0`. 
4. Mark the node adjacent node visited and push it to `q`, if any of these node found already visited then skip the step. Through this `u` stores the farthest node from `0` node.
5. Again fill the value `0` in  `vis`.
6. Start **BFS** again from `u`.
7. This would help in finding the farthest node from `u` and update `ans` which will store the distance between the two nodes.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)




## Code
```cpp
class Solution {
public:
    int treeDiameter(vector<vector<int>>& edges) {
        int n = edges.size() + 1;
        vector<vector<int>> adj(n, vector<int>());
        for (auto& i : edges) {
            adj[i[0]].push_back(i[1]);
            adj[i[1]].push_back(i[0]);
        }
        queue<int> q;
        vector<int> vis(n, 0);
        q.push(0);
        vis[0] = true;
        int u = 0;
        while (!q.empty()) {
            u = q.front();
            q.pop();
            for (auto v : adj[u]) {
                if (vis[v])
                    continue;
                vis[v] = true;
                q.push(v);
            }
        }
        fill(vis.begin(), vis.end(), 0);
        q.push(u);
        vis[u] = 1;
        int ans = -1;
        while (!q.empty()) {
            int sz = q.size();
            while (sz--) {
                u = q.front();
                q.pop();
                for (auto v : adj[u]) {
                    if (vis[v])
                        continue;
                    vis[v] = 1;
                    q.push(v);
                }
            }
            ans++;
        }
        return ans;
    }
};

```     