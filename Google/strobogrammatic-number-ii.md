# [ Strobogrammatic Number II](https://leetcode.com/problems/strobogrammatic-number-ii/description/)

## Problem Statement
- Given an integer `n`, return all the strobogrammatic numbers that are of length n. You may return the answer in any order.
- A strobogrammatic number is a number that looks the same when rotated `180` degrees (looked at upside down).




## Constraints
- 1 <= n <= 14



## Test Cases
1. **Input:** n = 2 <br>
**Output:** ["11","69","88","96"]
2. **Input:** n = 1 <br>
**Output:** ["0","1","8"]




## Approach / Intuition 
- Strobogrammatic numbers are symmetric, constructed using reversible pairs.
- Use recursion to build numbers layer by layer, starting from the middle.
- Ensure no leading zeros for multi-digit numbers by skipping {'0', '0'} at the outermost layer.
- At each level, prepend and append valid pairs to previously generated numbers.
- Return the final list of numbers when the desired length is reached.




## Algorithm 
1. Strobogrammatic digits are defined by pairs that can form valid numbers when rotated: `{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}`. The outermost digits of the number must be chosen from these pairs.
2. If `n==0` Return an empty string as the base layer for constructing longer numbers. If `n==1`: Return the middle digits allowed in strobogrammatic numbers `({"0", "1", "8"})`.
3. Generate strobogrammatic numbers for `n−2`. For each smaller number, prepend and append each reversible pair to form larger numbers. Ensure that `{'0', '0'}` is not used at the outermost positions for numbers greater than 1 digit (to avoid leading zeros)
4. Call the recursive function for the desired length `n`, passing the length as `finalLength` to handle leading zero constraints.






## Complexity
##### Time Complexity
- \(O(N*5^(N/2))\)
##### Space Complexity
- \(O(N+5^(N/2))\)




## Code
```cpp
class Solution {
public:
    vector<vector<char>> reversiblePairs = {
        {'0', '0'}, {'1', '1'}, 
        {'6', '9'}, {'8', '8'}, {'9', '6'}
    };
    vector<string> generateStroboNumbers(int n, int finalLength) {
        if (n == 0) {
            return { "" };
        }  
        if (n == 1) {
            return { "0", "1", "8" };
        }
        vector<string> prevStroboNums = generateStroboNumbers(n - 2, finalLength);
        vector<string> currStroboNums;
        for (string& prevStroboNum : prevStroboNums) {
            for (vector<char>& pair : reversiblePairs) {
                if (pair[0] != '0' || n != finalLength) {
                    currStroboNums.push_back(pair[0] + prevStroboNum + pair[1]);
                }
            }
        }
        return currStroboNums;
    }
    vector<string> findStrobogrammatic(int n) {
        return generateStroboNumbers(n, n);
    }
};
```     