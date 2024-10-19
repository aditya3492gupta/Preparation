# [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/)

## Problem Statement
- Given a string `s` and an integer `k`, return the length of the longest substring of `s` that contains at most `k` distinct characters.
    


## Constraints
- 1 <= s.length <= 5 * 10<sup>4</sup>
- 0 <= k <= 50.


## Test Cases
1. **Input:** s = "eceba", k = 2 <br>
**Output:** 3
2. **Input:** s = "aa", k = 1<br>
**Output:** 2

## Approach / Intuition 
- Using the **Sliding Window** Technique.
- Store the character frequency in the hashmap using the right pointer.
- If the hashmap size exceed the `k` then decrease the frequency of the character using the left pointer, until the size of the hashmap becomes less than or equal to `k`.
- Check the length of the current subarray and compare it with the maximum length found till now.

## Algorithm 
1. Declare a hashmap `mp` which stores `char` \& `int` as `key-value`.
2. Start iterating over the `s`.
3. Increase the frequency of `s[i]` using the right pointer in `mp` by one.
4. If the size of `mp` exceed `k` then using the left pointer decrease the size of `s[j]` until `mp.size() <= k`.
5. Compare the size of the current subarray with the `ans` and find the maximum of the two.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(K)\), K = max number of distinct character.

## Code
```cpp
class Solution {
public:
    int lengthOfLongestSubstringKDistinct(string s, int k) {
        int ans = 0;
        unordered_map<char, int>mp;
        int n = s.size();
        int j = 0;
        for(int i = 0 ; i < n ; i++){
            mp[s[i]]++;
            while(mp.size() > k){
                mp[s[j]]--;
                if(mp[s[j]] == 0)
                    mp.erase(s[j]);
            j++;
            }
            ans = max(ans, i - j + 1);
        }
        return ans;
    }
};
```     