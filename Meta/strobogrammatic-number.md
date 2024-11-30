# [Strobogrammatic Number](https://leetcode.com/problems/strobogrammatic-number/description/)

## Problem Statement
- Given a string `num` which represents an integer, return `true` if `num` is a strobogrammatic number.
- A strobogrammatic number is a number that looks the same when rotated `180` degrees (looked at upside down).




## Constraints
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>
- All Nodes will have unique values.




## Test Cases
1. **Input:** num = "69" <br>
**Output:** true
2. **Input:** num = "88"<br>
**Output:** true
3. **Input:** num = "962"<br>
**Output:** false




## Approach / Intuition 
- Use a lookup table to define how digits map to their rotated counterparts.
- Compare the leftmost and rightmost digits to ensure valid symmetry.
- Verify each digit exists in the mapping and matches its pair's rotated value.
- Return false if any character fails the rotation mapping check.
- If all pairs are valid, the number is strobogrammatic.




## Algorithm 
1. The `lut` map defines valid strobogrammatic mappings (e.g., '6' maps to '9').
2. Use two pointers `(l and r)` to compare characters from the left and right ends of the string.
3. Ensure both characters exist in the `lut`. Verify that the left character maps to the right character according to the `lut`.
4. If any character is not in the `lut` or fails the mapping check, return `false`.
5. If all pairs pass the check, the number is strobogrammatic.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)




## Code
```cpp
class Solution {
public:
    bool isStrobogrammatic(string num) {
        unordered_map<char, char> lut{{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}};
        for (int l = 0, r = num.size() - 1; l <= r; l++, r--) {
            if (lut.find(num[l]) == lut.end() || lut[num[l]] != num[r]) {
                return false;
            }
        }
        return true;
    }
};
```