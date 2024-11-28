# [Flip Game II](https://leetcode.com/problems/flip-game-ii/description/)

## Problem Statement
- You are playing a Flip Game with your friend.
- You are given a string `currentState` that contains only `'+'` and `'-'`. You and your friend take turns to flip two consecutive `"++"` into `"--"`. The game ends when a person can no longer make a move, and therefore the other person will be the winner.
- Return `true` if the starting player can guarantee a win, and `false` otherwise.




## Constraints
- 1 <= currentState.length <= 60
- currentState[i] is either '+' or '-'.




## Test Cases
1. **Input:** currentState = "++++" <br>
**Output:** true
2. **Input:** currentState = "+" <br>
**Output:** false




## Approach / Intuition 
- Using **backtracking with memoization**.
- Simulate all possible moves where consecutive `"++"` are flipped to `"--"` in the current state. 
- For each move, check if the opponent loses in all subsequent states (recursive backtracking).
- Assume both players play optimally, and return `true` if a winning move exists for the current player.
- Store results of previously computed states to avoid redundant calculations.




## Algorithm 
1. Identify all positions of consecutive `"++"` in the current state.
2. For each such position, flip `"++"` to `"--"` and recursively check if the opponent loses
3. If any move ensures the opponent cannot win, mark the current state as a win `(true)` and return it.
4. Restore the flipped move (backtracking) and continue exploring other possible moves.
5. If no move guarantees a win, mark the state as a loss `(false)` and return it.




## Complexity
##### Time Complexity
- \(O(N*2^N)\)
##### Space Complexity
- \(O(2^N+N)\),




## Code
```cpp
class Solution {
    unordered_map<string, bool> dp;
    bool rec(string& cur) {
        if (dp.contains(cur))
            return dp[cur];
        auto pos = cur.find("++");
        while (pos != string::npos) {
            bool flg = false;
            cur[pos] = '-';
            cur[pos + 1] = '-';
            if (!rec(cur))
                flg = true;
            cur[pos] = '+';
            cur[pos + 1] = '+';
            if (flg)
                return dp[cur] = true;
            pos = cur.find("++", pos + 1);
        }
        return dp[cur] = false;
    }
public:
    bool canWin(string currentState) {
        dp.clear();
        return rec(currentState);
    }
};
```