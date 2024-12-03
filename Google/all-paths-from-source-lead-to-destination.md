# [All Paths from Source Lead to Destination](https://leetcode.com/problems/all-paths-from-source-lead-to-destination/description/)

## Problem Statement
- Given the edges of a directed graph where `edges[i] = [ai, bi]` indicates there is an edge between nodes `ai` and `bi`, and two nodes `source` and `destination` of this graph, determine whether or not all paths starting from `source` eventually, end at `destination`, that is:
  - At least one path exists from the `source` node to the `destination` node
  - If a path exists from the `source` node to a node with no outgoing edges, then that node is equal to `destination`.
  - The number of possible paths from `source` to `destination` is a finite number.
- Return `true` if and only if all roads from `source` lead to `destination`.




## Test Cases
1. **Input:** n = 3, edges = \[[0,1],[0,2]], source = 0, destination = 2 <br>
**Output:** false
2. **Input:** n = 4, edges = \[[0,1],[0,3],[1,2],[2,1]], source = 0, destination = 3 <br>
**Output:** false
3. **Input:** n = 4, edges = \[[0,1],[0,2],[1,3],[2,3]], source = 0, destination = 3 <br>
**Output:** true





## Constraints
- 1 <= n <= 10<sup>4</sup>
- 0 <= edges.length <= 10<sup>4</sup>
- edges.length == 2
- 0 <= ai, bi <= n - 1
- 0 <= source <= n - 1
- 0 <= destination <= n - 1
- The given graph may have self-loops and parallel edges.



## Approach / Intuition 
- Using **Topological Sort**.
- Reverse the condition asked and start finding the path from `destination` to `source`.
- Store `indegree` as `outdegree` of nodes.
- If `destination` is same as the node with a `indegree` return `false`.




## Algorithm 
1. Declare `adj` for adjacency list and initialize `indegree` with `0` for storing the appropriate `indegree` of nodes.
2. Initialize `q` and push `destination` as we are finding the path from `destination` to `source`.
3. Using the `Topological Sort` find the path.
4. If `source` and current neighbour of the current node is same then return `true`.
5. Else return `false`.






## Complexity
##### Time Complexity
- \(O(V+E)\)
##### Space Complexity
- \(O(V)\)




## Code
```cpp
class Solution {
public:
    bool leadsToDestination(int n, vector<vector<int>>& edges, int source,
                            int destination) {
        vector<vector<int>> adj(n);
        vector<int> indegree(n, 0);
        for (auto i : edges) {
            if (i[0] == destination)
                return false;
            adj[i[1]].push_back(i[0]);
            indegree[i[0]]++;
        }
        queue<int> q;
        q.push(destination);
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            if (node == source)
                return true;
            for (auto i : adj[node]) {
                indegree[i]--;
                if (indegree[i] == 0)
                    q.push(i);
            }
        }
        return false;
    }
};
```     