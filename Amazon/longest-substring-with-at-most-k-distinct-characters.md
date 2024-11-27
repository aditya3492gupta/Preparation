# [ Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/)



## Problem Statement
- Given a string `s` and an integer `k`, return the length of the longest substring of `s` that contains at most `k` ***distinct*** characters.



## Constraints
- 1 <= s.length <= 5 * 10<sup>4</sup>
- 0 <= k <= 50



## Test Cases
1. **Input:** rs = "eceba", k = 2 <br>
**Output:** 3
2. **Input:** s = "aa", k = 1 <br>
**Output:** 2




## Approach / Intuition 
- Using **sliding window approach**.
- `mp` helps in maintaining the count of characters present in the window.
- If the count exceed `k` reduce the count of the character from the left.
- Find the maximum length of the string with requirements.




## Algorithm 
1. Initialize an `unordered_map<char, int> mp` for storing the frequency of the characters in the current window.
2. `i` represent the right pointer of window and `j` for left.
3. Iterate over `s` and increment the frequency of `s[i]`.
4. Check if the size of `mp` exceed `k`.
5. if yes, move the left pointer by removing the character from the left.
6. Check for **maximum** of the generated.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(K)\)



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