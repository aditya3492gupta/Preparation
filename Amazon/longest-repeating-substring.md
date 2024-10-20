# [Longest Repeating Substring](https://leetcode.com/problems/longest-repeating-substring/description/)

## Problem Statement
- Given a string `s`, return the length of the **longest repeating substrings**. If no repeating substring exists, return `0`.

## Constraints
- 1 <= s.length <= 2000
- `s` consists of lowercase English letters.


## Test Cases
1. **Input:**  s = "abcd" <br>
**Output:** 0
2. **Input:** s = "abbaba"<br>
**Output:** 2
3. **Input:** s = "aabcaabdaab"<br>
**Output:** 3

## Approach / Intuition 
- It is a modification of problem **Longest Common Substring**.
- If common characters are found then add one to the previous diagonal of `dp`.
- Compare the `ans` with current value of `dp[i][j]`.

## Algorithm 
1. Initialize the 2D `dp` vector with value `0`.
2. Then iterating over the string `s` using `s[i]` and the forthcoming character of `s` using `s[j]`, if the characters are common then increment `dp[i][j]` and compare `ans` with current value of `dp[i][j]`.
3. If there is atleast a substring that contains repeating character then `ans` will return its value otherwise the `ans` will return `0`. 

## Complexity
##### Time Complexity
- O(N<sup>2</sup>)
##### Space Complexity
- O(N<sup>2</sup>)

## Code
```cpp
class Solution {
public:
    int longestRepeatingSubstring(string s) {
        int n = s.size();
        vector<vector<int>>dp(n + 1, vector<int>(n + 1, 0));
        int ans = 0;
        for(int i = 1 ; i < n + 1 ; i++){
            for(int j = i + 1 ; j < n + 1 ; j++){
                if(s[i - 1] == s[j - 1]){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                    ans = max(ans, dp[i][j]);
                }
            }
        }
        return ans;
    }
};
```