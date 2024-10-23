# [Number of Distinct Island](https://leetcode.com/problems/number-of-distinct-islands/description/)

## Problem Statement
- You are given an `m x n` binary matrix grid. An island is a group of `1's` (representing land) connected **4-directionally** (horizontal or vertical) .
- You may assume all four edges of the grid are surrounded by water.
- An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.
- Return the number of **distinct** islands.


## Constraints
- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 50
- `grid[i][j]` is either `0` or `1`.


## Test Cases
1. **Input:** grid = \[[1,1,0,0,0],[1,1,0,0,0],[0,0,0,1,1],[0,0,0,1,1]] <br>
**Output:** 1
2. **Input:** grid = \[[1,1,0,1,1],[1,0,0,0,0],[0,0,0,0,1],[1,1,0,1,1]]<br>
**Output:** 3


## Approach / Intuition 
- Using the **DFS**.
- `island` will contains distinct string.
- Visit `grid[i][j]` and if it is `1` then check for all the adjacent cell if they are a island or not.
- If found island then mark it as `0`.
- Add the relative position of the current cell to `s`.
- This help to find distinct `island`.

## Algorithm 
1. Declare an `unordered_set` island that contains the distinct island.
2. Iterate over the `grid` and if a cell is found as an island then check for all the adjacent islands.
3. Add the relative position of the current cell which is an island to s and then add it to `s`.
4. Insert `s` to `island` if `s` is already present in `island` then no change occur else the size of `island` increases which shows the number of distinct islands.

## Complexity
##### Time Complexity
- \(O(N*M)\)
##### Space Complexity
- \(O(N*M)\)

## Code
```cpp
class Solution {
public:
    void checkDistinct(vector<vector<int>> &grid, int i, int j, int row, int col, string &s){
        int n = grid.size();
        int m = grid[0].size();
        if(row >= 0 and row < n and col >= 0 and col < m and grid[row][col] == 1){
            grid[row][col] = 0;
            s += to_string(row - i) + to_string(col - j);
            checkDistinct(grid, i, j, row - 1, col, s);
            checkDistinct(grid, i, j, row + 1, col, s);
            checkDistinct(grid, i, j, row, col - 1, s);
            checkDistinct(grid, i, j, row, col + 1, s);
        }
    }
    int numDistinctIslands(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        unordered_set<string> island;
        for(int i = 0 ; i < n ; i++){
            for(int j = 0 ; j < m ; j++){
                if(grid[i][j]){
                    string s;
                    checkDistinct(grid, i, j , i , j, s);
                    island.insert(s);
                }
            }
        }
        return island.size();
    }
};
```