# [Paint House](https://leetcode.com/problems/paint-house/)

## Problem Statement
- There is a row of `n` houses, where each house can be painted one of three colors: **red, blue, or green**.
- The cost of painting each house with a certain color is different. 
- You have to paint all the houses such that no two adjacent houses have the same color.
- Example for house 0 `costs[0][0]` -> red, `costs[0][1]` -> blue, `costs[0][2]` -> green.


## Constraints
- costs.length == n
- costs[i].length == 3
- 1 <= n <= 100
- 1 <= costs[i][j] <= 20


## Test Cases
1. **Input:** costs = \[[17,2,17],[16,16,5],[14,3,19]] <br>
**Output:** 10
2. **Input:** costs = \[[7,6,2]] <br>
**Output:** 2

## Approach / Intuition 
- Using tabulation method with dp.
- If we are choosing red then we cannot choose reed for the adjacent house.
- So calculating the cost of coloring by initially choosing all the three colors.
- Find minimum cost.

## Algorithm 
1. Initialize a 2D vector `dp` having rows equal to the number of houses and 3 column as of number of color with initial value 0.
2. In the first row update the value with the initial cost of coloring using each color.
3. Start iterating through `costs` and update the value of `dp` as per the given condition og not using the same adjacent color by 
```cpp
dp[i][0] = min(dp[i - 1][1], dp[i - 1][2]) + costs[i][0];
            dp[i][1] = min(dp[i - 1][0], dp[i - 1][2]) + costs[i][1];
            dp[i][2] = min(dp[i - 1][0], dp[i - 1][1]) + costs[i][2];
```
1. After iterating through the `cost` find the minimum value in the last row  of `dp`.
## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)

## Code
```cpp
class Solution {
public:
    int minCost(vector<vector<int>>& costs) {
        int n = costs.size();
        vector<vector<int>> dp(n, vector<int>(3, 0));
        dp[0][0] = costs[0][0];
        dp[0][1] = costs[0][1];
        dp[0][2] = costs[0][2];
        for(int i = 1; i < n ; i++){
            dp[i][0] = min(dp[i - 1][1], dp[i - 1][2]) + costs[i][0];
            dp[i][1] = min(dp[i - 1][0], dp[i - 1][2]) + costs[i][1];
            dp[i][2] = min(dp[i - 1][0], dp[i - 1][1]) + costs[i][2];
        }
        return min({dp[n - 1][0], dp[n - 1][1], dp[n - 1][2]});
    }
};
```