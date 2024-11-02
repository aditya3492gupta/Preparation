# [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/description/)

## Problem Statement
- You are given an `m x n` matrix board containing letters `'X'` and `'O'`, capture regions that are **surrounded**:
    - **Connect**: A cell is connected to adjacent cells horizontally or vertically.
    - **Region**: To form a region connect every `'O'` cell.
    - **Surround**: The region is surrounded with   `'X'` cells if you can `connect the region` with `'X'` cells and none of the region cells are on the edge of the `board`.
- A **surrounded region is captured** by replacing all `'O's` with `'X's` in the input matrix `board`.


## Constraints
- m == board.length
- n == board[i].length
- 1 <= m, n <= 200
- board[i][j] is 'X' or 'O'.


## Test Cases
1. **Input:** board = \[["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]] <br>
**Output:** \[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
2. **Input:** \[["X"]]<br>
**Output:** \[["X"]]



## Approach / Intuition 
- Using **DFS with recursion**.
- The `O` on the boundary cannot be converted into `X` as it is not surrounded by `X`.
- Mark all the `O` on the boundary using `vis`.
- Mark all the other `O` that are adjacent to the boundary `O`.
- Make the changes using the unmarked `O`.



## Algorithm 
1. Mark the Boundary `O` in `vis`.
2. Mark the adjacent `O` of the above marked `O`.
3. Convert the `O` to `X` which are unmarked.

## Complexity
##### Time Complexity
- \(O(N*M)\)
##### Space Complexity
- \(O(N*M)\)

## Code
```cpp
class Solution {
public:
    void dfs(int i, int j, vector<vector<int>> &vis, vector<vector<char>>& board, vector<vector<int>> &direction){
        vis[i][j] = 1;
        int n = board.size();
        int m =board[0].size();
        for(int k = 0 ; k < 4 ; k++){
            int row = i + direction[k][0];
            int col = j + direction[k][1];
            if(row >= 0 and row < n and col >= 0  and col < m and !vis[row][col] and board[row][col] == 'O')
                dfs(row, col, vis, board, direction);

        }
    }
    void solve(vector<vector<char>>& board) {
        int n = board.size();
        int m = board[0].size();
        vector<vector<int>> vis(n, vector<int>(m, 0));
        vector<vector<int>>direction = {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};
        for(int j = 0 ; j < m ; j++){
            if(!vis[0][j] and board[0][j] == 'O')
                dfs(0, j, vis, board, direction);
            if(!vis[n - 1][j] and board[n - 1][j] == 'O')
                dfs(n - 1, j, vis, board, direction);
        }
        for(int i = 0 ; i < n ; i++){
            if(!vis[i][0] and board[i][0] == 'O')
                dfs(i, 0, vis, board, direction);
            if(!vis[i][m - 1] and board[i][m - 1] == 'O')
                dfs(i, m - 1, vis, board, direction);
        }
        for(int i = 0 ; i < n ; i++){
            for(int j = 0 ; j < m ; j++){
                if(!vis[i][j] and board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
    }
};
```     