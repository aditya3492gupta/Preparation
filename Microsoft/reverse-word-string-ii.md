# [Reverse Words in a String II](https://leetcode.com/problems/reverse-words-in-a-string-ii/description/)

## Problem Statement
- Given a character array `s`, reverse the order of the words.
- Your code must solve the problem ***in-place***, i.e. without allocating extra space.

 


## Constraints
- 1 <= s.length <= 10<sup>5</sup>
- `s[i]` is an English letter (uppercase or lowercase), digit, or space `' '`.
- `s` does not contain leading or trailing spaces.


## Test Cases
1. **Input:** ros = ["t","h","e"," ","s","k","y"," ","i","s"," ","b","l","u","e"] <br>
**Output:** ["b","l","u","e"," ","i","s"," ","s","k","y"," ","t","h","e"]
2. **Input:** root = ["a"] <br>
**Output:** ["a"]

## Approach / Intuition 
- Using the two pointer approach.
- Iterating `j` until a space `' '` is encountered and the reverse that word in the vector s.

## Algorithm 
1. Reverse the whole vector so that the word could take their appropriate position.
2. Start iterating `i` and `j` from 0.
3. Move `j` until a space `' '` is encountered and `i` is always in found at the start of the words.
4. Reverse the current word.
5. Move `j` by one place as it is now at the start of other word and then update `i = j` so that `i` could also be placed at the start of that particular word.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)

## Code
```cpp
class Solution {
public:
    void reverseWords(vector<char>& s) {
        int n = s.size();
        reverse(s.begin(), s.end());
        int i = 0, j = 0;
        while(i < n){
            while(j < n  and s[j] != ' ')
                j++;
            reverse(s.begin() + i, s.begin() + j);
            j++;
            i = j;
        }
    }
};
```