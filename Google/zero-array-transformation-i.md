# [Zero Array Transformation I](https://leetcode.com/problems/zero-array-transformation-i/description/)

## Problem Statement
- You are given an integer array nums of length `n` and a 2D array queries, where `queries[i] = [li, ri]`.
- For each queries[i]:
    - Select a subset of indices within the range `[li, ri]` in nums.
    - Decrement the values at the selected indices by `1`.
- A Zero Array is an array where all elements are equal to 0.
- Return `true` if it is possible to transform `nums` into a Zero Array after processing all the queries sequentially, otherwise return `false`.




## Constraints
- 1 <= nums.length <= 10<sup>5</sup>
- 0 <= nums[i] <= 10<sup>5</sup>
- 1 <= queries.length <= 10<sup>5</sup>
- queries[i].length == 2
- a<sub>i</sub> != b<sub>i</sub>
- 0 <= li <= ri < nums.length




## Test Cases
1. **Input:** [1,0,1], queries = \[[0,2]] <br>
**Output:** true
2. **Input:** nums = [4,3,2,1], queries = \[[1,3],[0,2]]<br>
**Output:** false




## Approach / Intuition 
- Using the **Prefix Sum and Difference Array**. 
- Use a prefix array to efficiently handle the range-based decrements from the queries.
- Increment the start of the range and decrement just past the end to mark the query.
- Compute the cumulative sum of the prefix array to get the actual decrement applied at each index.
- Compare the cumulative decrement with the original array to ensure all elements can reach zero.
- If any element cannot reach zero, return false; otherwise, return true.




## Algorithm 
1. Use a prefix array (pref) to apply the range increment operations efficiently. For each query `[l, r]`:
    - Increment `pref[l]` by `1` to mark the start of the operation.
    - Decrement `pref[r + 1]` by `1` to mark the end of the operation (if within bounds).
2. Convert the prefix array into the actual applied decrements for each index by calculating the cumulative sum. For index `i: pref[i] += pref[i-1]`.
3. Compare the cumulative decrement at each index with the original array:
    - If the cumulative decrement `(pref[i])` is less than `nums[i]` at any index, it is impossible to zero out the array using the given queries.
4. If all elements can be reduced to zero or below, return `true`.




## Complexity
##### Time Complexity
- \(O(n+q)\)
##### Space Complexity
- \(O(n)\)




## Code
```cpp
class Solution {
public:
    bool isZeroArray(vector<int>& nums, vector<vector<int>>& queries) {
        vector<int> pref(nums.size(), 0);
        for (int i = 0; i < queries.size(); i++) {
            pref[queries[i][0]]++;
            if (queries[i][1] < nums.size() - 1)
                pref[queries[i][1] + 1]--;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (i > 0)
                pref[i] = pref[i] + pref[i - 1];
            if (pref[i] < nums[i])
                return false;
        }
        return true;
    }
};
```     