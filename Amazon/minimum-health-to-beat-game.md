# [Minimum Health to Beat Game](https://leetcode.com/problems/minimum-health-to-beat-game/description/)

## Problem Statement
- You are playing a game that has `n` levels numbered from `0` to `n - 1`. You are given a 0-indexed integer array `damage` where `damage[i]` is the amount of health you will lose to complete the i<sup>th</sup> level.
- You are also given an integer `armor`. You may use your armor ability at most once during the game on any level which will protect you from at most `armor` damage.
- You must complete the levels in order and your health must be **greater than** `0` at all times to beat the game.
- Return the **minimum health** you need to start with to beat the game.


## Constraints
- n == damage.length
- 1 <= n <= 10<sup>5</sup>
- 0 <= damage[i] <= 10<sup>5</sup>
- 0 <= armor <= 10<sup>5</sup>


## Test Cases
1. **Input:** damage = [2,7,4,3], armor = 4 <br>
**Output:** 13
2. **Input:** damage = [2,5,3,4], armor = 7<br>
**Output:** 10
3. **Input:** damage = [3,3,3], armor = 0<br>
**Output:** 10

## Approach / Intuition 
- Using the **greedy approach**.
- The armor will be used against the damage it can bear the maximum.

## Algorithm 
1. Calculate the sum of the damage that can be caused in `ans`.
2. Increase it by one as there must be atleast one health point remaining at the end.
3. If the armor damage bearing capacity is `0` then return `ans`.
4. Else find minimum among `armor` and maximum damage caused at an instance and subtract that value from the `ans` and return the final value

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)

## Code
```cpp
class Solution {
public:
    long long minimumHealth(vector<int>& damage, int armor) {
        long long ans = 0;
        int n = damage.size();
        for(int i = 0 ; i < n ; i++)
            ans += damage[i];
        ans++;
        if(armor == 0)
            return ans;
        int mx = *max_element(damage.begin(), damage.end());
        ans -= min(mx, armor);
        return ans;
    }
};
```