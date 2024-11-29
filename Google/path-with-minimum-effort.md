# [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/description/)

## Problem Statement
- You are a hiker preparing for an upcoming hike. You are given `heights`, a 2D array of size `rows x columns`, where `heights[row][col]` represents the height of cell `(row, col)`. You are situated in the top-left cell, `(0, 0)`, and you hope to travel to the bottom-right cell, `(rows-1, columns-1)` (i.e., 0-indexed). You can move up, down, left, or right, and you wish to find a route that requires the minimum effort.
- A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.
- Return the minimum effort required to travel from the top-left cell to the bottom-right cell.




## Constraints
- rows == heights.length
- columns == heights[i].length
- 1 <= rows, columns <= 100
- 1 <= heights[i][j] <= 10<sup>6</sup>




## Test Cases
1. **Input:** heights = [[1,2,2],[3,8,2],[5,3,5]]<br>
**Output:** 2
2. **Input:** heights = [[1,2,3],[3,8,4],[5,3,5]]<br>
**Output:** 1
3. **Input:** heights = [[1,2,3],[3,8,4],[5,3,5]]<br>
**Output:** 1




## Approach / Intuition 
- Using the **Dijkstra's algorithm**.
- Treat the grid as a graph where each cell connects to its neighbors with an effort equal to their height difference.
- Use a priority queue to always expand the path with the smallest current maximum effort.
- Update the `dist` array whenever a lower maximum effort path to a cell is found.
- Stop when the bottom-right cell is reached, as Dijkstra guarantees the optimal path.




## Algorithm 
1. Treat the grid as a graph where nodes are cells, and edges have weights equal to the absolute height difference between adjacent cells.
2. Initialize a `dist` array with large values and set `dist[0][0] = 0`; use a priority queue to process cells by minimum current effort.
3. For each cell, calculate the effort to move to its neighbors and update their distance if a smaller maximum effort path is found.
4. Push updated neighbors into the priority queue for further exploration.
5. Stop when the bottom-right cell is reached, as the priority queue ensures the smallest maximum effort is processed first.




## Complexity
##### Time Complexity
- \(O(n*m*log(n*m))\)
##### Space Complexity
- \(O(n*m)\)




## Code
```cpp
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) {
        priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int,int>>>> pq;
        int n = heights.size();
        int m = heights[0].size();
        vector<vector<int>> dist(n, vector<int>(m, 1e9));
        dist[0][0] = 0;
        pq.push({0, {0, 0}});
        int dr[] = {-1, 0, 1, 0};
        int dc[] = {0, 1, 0, -1};
        while (!pq.empty()) {
            auto it = pq.top();
            pq.pop();
            int diff = it.first;
            int row = it.second.first;
            int col = it.second.second;
            if (row == n - 1 && col == m - 1)
                return diff;
            for (int i = 0; i < 4; i++) {
                int newr = row + dr[i];
                int newc = col + dc[i];
                if (newr >= 0 && newc >= 0 && newr < n && newc < m) {
                    int newEffort =
                        max(abs(heights[row][col] - heights[newr][newc]), diff);
                    if (newEffort < dist[newr][newc]) {
                        dist[newr][newc] = newEffort;
                        pq.push({newEffort, {newr, newc}});
                    }
                }
            }
        }
        return 0;
    }
};
```     