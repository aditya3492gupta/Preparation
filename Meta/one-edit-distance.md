# [One Edit Distance](https://leetcode.com/problems/one-edit-distance/description/)

## Problem Statement
- Given two strings `s` and `t`, return `true` if they are both one edit distance apart, otherwise return `false`.
- A string `s` is said to be one distance apart from a string t if you can:
    - **Insert** exactly one character into `s` to get `t`.
    - **Delete** exactly one character from `s` to get `t`.
    - **Replace** exactly one character of `s` with a different character to get `t`.


## Constraints
- 0 <= s.length, t.length <= 10<sup>4</sup>
- `s` and `t` consist of lowercase letters, uppercase letters, and digits.


## Test Cases
1. **Input:** s = "ab", t = "acb" <br>
**Output:** true
2. **Input:** s = "", t = "" <br>
**Output:** false

## Approach / Intuition 
- Find the first dissimilar character in both the string and then check whether the the rest string is equal or not.
- If there is one insertion and one deletion and one replacement then no change in length of the string.
- If there is either of one insertion or deletion then maximum difference in length of both the string is 1.
- If the two string differ in length by two characters then there is no possible way of them be at one edit distance.

## Algorithm 
1. Find the length of both the string, if difference in the length is more than one then return false.
2. Make sure that the string s is smaller string.
3. Find the first character that is not same and check the rest string is same or not.
4. If the remaining string is same return true else return false.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)

## Code
```cpp
class Solution {
public:
    bool isOneEditDistance(string s, string t) {
        int n = s.size();
        int m = t.size();
        if(abs(n - m) > 1)
            return false;
        if(n > m)
           isOneEditDistance(t, s);
        for(int i = 0 ; i < n ; i++){
            if(s[i] != t[i]){
                if(n == m)
                    return s.substr(i + 1) == t.substr(i + 1);
                else
                    return s.substr(i) == t.substr(i + 1);
            }
        }
        return n == m - 1;
    }
};
```