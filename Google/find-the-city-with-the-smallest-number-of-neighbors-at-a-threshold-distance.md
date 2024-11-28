# [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/description/)




## Problem Statement
- There are `n` cities numbered from `0` to `n-1`. Given the array edges where `edges[i] = [fromi, toi, weighti]` represents a bidirectional and weighted edge between cities `fromi` and `toi`, and given the integer `distanceThreshold`.
- Return the city with the smallest number of cities that are reachable through some path and whose distance is at most `distanceThreshold`, If there are multiple such cities, return the city with the greatest number.
- Notice that the distance of a path connecting cities i and j is equal to the sum of the edges' weights along that path.




## Constraints
- 2 <= n <= 100
- 1 <= edges.length <= n * (n - 1) / 2
- edges[i].length == 3
- 0 <= fromi < toi < n
- 1 <= weighti, distanceThreshold <= 10^4
- All pairs (fromi, toi) are distinct.




## Test Cases
1. **Input:** graph =n = 4, edges = \[[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4 <br>
**Output:** 3
2. **Input:** n = 5, edges = \[[0,1,2],[0,4,8],[1,2,3],[1,4,2],[2,3,1],[3,4,1]], distanceThreshold = 2 <br>
**Output:** 0




## Approach / Intuition 
- Using **Floyd-Warshall Algorithm**.
- Treat the cities as nodes in a graph and roads as weighted edges. The weight of an edge corresponds to the distance.
- The task reduces to finding the shortest paths between all pairs of cities and counting how many cities are reachable within the threshold for each city.
- Once the shortest distances between all pairs of cities are computed, determine for each city how many other cities are reachable within the given `distanceThreshold`.
- Identify the city with the smallest number of reachable cities.
- If multiple cities have the same number of reachable cities, select the one with the largest city number, ensuring the result is unique.





## Algorithm 
1. Create a 2D matrix dist to store the shortest distance between any two nodes. Initialize all distances to `INT_MAX` `(representing infinity)`, except for direct edges provided in the input `(edges)`, and set the diagonal elements `(dist[i][i])` to `0`.
2. Use three nested loops to update `dist[i][j]`. If a shorter path from `i` to `j` via `k` is found `(dist[i][j] > dist[i][k] + dist[k][j])`, update `dist[i][j]`.
3. For each city, count the number of other cities that are reachable within the given `distanceThreshold`.
4. Track the city with the minimum number of reachable cities. In case of ties, choose the city with the largest city number.




## Complexity
##### Time Complexity
- \(O(N^3)\)
##### Space Complexity
- \(O(N^2)\)




## Code
```cpp
class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        vector<vector<int>> dist(n, vector<int>(n, INT_MAX));
        for (auto it : edges) {
            dist[it[0]][it[1]] = it[2];
            dist[it[1]][it[0]] = it[2];
        }
        for (int i = 0; i < n; i++)
            dist[i][i] = 0;
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (dist[i][k] == INT_MAX || dist[k][j] == INT_MAX)
                        continue;
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
        int cntCity = n;
        int cityNo = -1;
        for (int city = 0; city < n; city++) {
            int cnt = 0;
            for (int adjCity = 0; adjCity < n; adjCity++) {
                if (dist[city][adjCity] <= distanceThreshold)
                    cnt++;
            }
            if (cnt <= cntCity) {
                cntCity = cnt;
                cityNo = city;
            }
        }
        return cityNo;
    }
};
```