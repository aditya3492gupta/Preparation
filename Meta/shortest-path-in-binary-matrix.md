# [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/description/)

## Problem Statement
- Given an `n x n` binary matrix `grid`, return the length of the shortest clear path in the matrix. If there is no clear path, return `-1`.
- A clear path in a binary matrix is a path from the top-left cell (i.e., `(0, 0)`) to the bottom-right cell (i.e., `(n - 1, n - 1)`) such that:
    - All the visited cells of the path are `0`.
    - All the adjacent cells of the path are 8-directionally connected (i.e., they are different and they share an edge or a corner).
- The length of a clear path is the number of visited cells of this path.




## Constraints
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>
- All Nodes will have unique values.




## Test Cases
1. **Input:** grid = \[[0,1],[1,0]] <br>
**Output:** 2
2. **Input:** grid = \[[0,0,0],[1,1,0],[1,1,0]]<br>
**Output:** 4
3. **Input:** grid = \[[1,0,0],[1,1,0],[1,1,0]]<br>
**Output:** -1




## Approach / Intuition 
- Inorder Successor of any node is the smallest node that is greater than it.
- It means that the node is the *leftmost* node of its right child or its parent node.




## Algorithm 
1. If the `right child` is present, return the *leftmost* node in the subtree.
2. Else start iterating from the `root` of the node.
3. If the `p->val > root->val` move to the right child.
4. Else update `ans` with `root` and move to the left child.
5. Return `ans`




## Complexity
##### Time Complexity
- \(O(N*M)\)
##### Space Complexity
- \(O(N*M)\)




## Code
```cpp
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        if (grid[0][0] || grid[n-1][m-1])
            return -1;
        vector<pair<int, int>> directions = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
        queue<pair<int, int>> q;
        q.push({0, 0});
        grid[0][0] = 1;
        while (!q.empty()) {
            auto [x, y] = q.front();
            q.pop();
            int steps = grid[x][y];
            if (x == n - 1 && y == m - 1)
                return steps;
            for (auto [dx, dy] : directions) {
                int nx = x + dx, ny = y + dy;
                if (nx >= 0 && nx < n && ny >= 0 && ny < m && grid[nx][ny] == 0) {
                    q.push({nx, ny});
                    grid[nx][ny] = steps + 1;
                }
            }
        }
        return -1;
    }
};

```