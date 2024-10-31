# [Merge Operations to Turn Array Into a Palindrome](https://leetcode.com/problems/merge-operations-to-turn-array-into-a-palindrome/description/)



## Problem Statement
- You are given an array `nums` consisting of **positive** integers.
- You can perform the following operation on the array **any** number of times:
    - Choose any two **adjacent** elements and **replace** them with their sum.
        - For example, if nums = [1,<u>2,3</u>,1], you can apply one operation to make it `[1,5,1]`.
- Return the `minimum` number of operations needed to turn the array into a `palindrome`.


## Constraints
- 1 <= nums.length <= 10<sup>5</sup>.
- 1 <= nums[i] <= 10<sup>6</sup>


## Test Cases
1. **Input:** nums = [4,3,2,1,2,3,1] <br>
**Output:** 2
2. **Input:** nums = [1,2,3,4]<br>
**Output:** 3


## Approach / Intuition 
- Using **Two-Pointer Technique**.
- If the values at both pointers are already the same, move both pointers inward since no operation is needed.
- If the values are different, merge the smaller value toward the other side, as this reduces the discrepancy faster.
- Every time you merge an element, increment a counter to keep track of the operations needed.



## Algorithm 
1. Initialize two pointers at the start and end of the array.
2. If elements at both pointers are equal, move both pointers inward.
3. If the left element is smaller, add it to the next element on the left and move the left pointer; otherwise, add the right element to its neighbor and move the right pointer.
4. Count each merge operation until the pointers meet, returning the total.



## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)



## Code
```cpp
class Solution {
public:
    int minimumOperations(vector<int>& nums) {
        int cnt = 0, n = nums.size();
        int i = 0, j = n - 1;
        vector<long long> v(nums.begin(), nums.end());
        while (i < j) {
            if (v[i] == v[j]) {
                i++, j--;
                continue;
            }
            if (v[i] < v[j]) {
                v[i + 1] += v[i];
                i++;
            } else {
                v[j - 1] += v[j];
                j--;
            }
            cnt++;
        }
        return cnt;
    }
};
```