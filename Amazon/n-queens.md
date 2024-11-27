# [N-Queens](https://leetcode.com/problems/n-queens/)

## Problem Statement
- The n-queens puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.
- Given an integer `n`, return all distinct solutions to the **n-queens puzzle**. You may return the answer in **any order**.
- Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.



## Constraints
- 1 <= n <= 9



## Test Cases
1. **Input:** n = 4 <br>
**Output:** \[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
2. **Input:** n = 1<br>
**Output:** \[["Q"]]



## Approach / Intuition 
- Using the **backtracking approach**.
- Placing `'Q'` at each position and checking whether there exist any adjacent `'Q'` or not.
- If adjacent `'Q'` exist try for other position.
- Checking for all permutation and combination.



## Algorithm 
1. Initialize a string `s` with value `'.'` of size `n` and a `vector<string> v` for the output.
2. Now, for every `s[i]` check that `Q` could be placed legally or not.
3. If yes, then push that string in `v` and replace `'Q'` with `'.'` and recursively call the `recur` function.
4. The `check` function checks the legal placement of `'Q'` in the string `s`.
5. It checks for the presence of `'Q'` in the same row and same column.
6. If found then it returns `false`, else `true`.




## Complexity
##### Time Complexity
- \(O(N!)\)
##### Space Complexity
- \(O(N)\)




## Code
```cpp
class Solution {
    vector<vector<string>> ans;
    bool check(vector<string>& v, int ind, int n) {
        if (v.empty())
            return true;
        for (int i = 0; i < v.size(); i++) {
            if (v[i][ind] == 'Q')
                return false;
        }
        int y = ind - 1;
        int x = v.size() - 1;
        while (x >= 0 && y >= 0) {
            if (v[x][y] == 'Q')
                return false;
            x--;
            y--;
        }
        y = ind + 1;
        x = v.size() - 1;
        while (x >= 0 && y < n) {
            if (v[x][y] == 'Q')
                return false;
            x--;
            y++;
        }
        return true;
    }
    void recur(int n, string& s, vector<string>& v) {
        if (v.size() == n) {
            ans.push_back(v);
            return;
        }
        for (int i = 0; i < n; i++) {
            if (check(v, i, n)) {
                s[i] = 'Q';
                v.push_back(s);
                s[i] = '.';
                recur(n, s, v);
                v.pop_back();
            }
        }
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        string s = "";
        for (int i = 0; i < n; i++)
            s += '.';
        vector<string> v;
        recur(n, s, v);
        return ans;
    }
};
```