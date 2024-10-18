# [Paint Fence](https://leetcode.com/problems/paint-fence/)

## Problem Statement
- You are painting a fence of `n` posts with `k` different colors. You must paint the posts following these rules:
    - Every post must be painted exactly one color.
    - There **cannot** be three or more **consecutive** posts with the same color.
- Given the two integers n and k, return the **number of ways** you can paint the fence.


## Constraints
- 1 <= n <= 50.
- 1 <= k <= 10<sup>5</sup>
- The test cases are generated such that the answer is in the range `[0, 2^31 - 1]` for the given `n` and `k`.


## Test Cases
1. **Input:** n = 3, k = 2 <br>
**Output:** 6
2. **Input:** n = 1, k = 1<br>
**Output:** 1

## Approach / Intuition 
- Problem is based on the fibonacci pattern.
- If there are only one house, use any color.
- If there are two houses use any combination of two colors.
- If there are more than two house than only two adjacent house can have same color, so the current house can have `(k - 1) * [sum of nuber of ways to color last two houses]`.

## Algorithm 
1.  If there are only one house, use any color.
2. If there are two houses use any combination of two colors.
3. Initialize `dp` with `dp[1] = k` and `dp[2] = k * k' for the above two condition.
4. Update `dp[i] = ((k - 1) * (dp[i - 1] + dp[i - 2]))`.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)

## Code
```cpp
class Solution {
public:
    int numWays(int n, int k) {
        if(n == 1)
            return k;
        if(n == 2)
            return k * k;
        vector<int> dp(n + 1, 0);
        dp[1] = k;
        dp[2] = k * k;
        k--;
        for(int i = 3 ; i <= n ; i++)
            dp[i] = k * (dp[i - 1] + dp[i - 2]);
        return dp[n];
    }
};
```     