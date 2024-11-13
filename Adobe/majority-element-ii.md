# [Majority Element II](https://leetcode.com/problems/majority-element-ii/description/)



## Problem Statement
- Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.



## Constraints
- 1 <= nums.length <= 5 * 10<sup>4</sup>.
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>




## Test Cases
1. **Input:** nums = [3,2,3] <br>
**Output:** [3]
2. **Input:** nums = [1]<br>
**Output:** [1]
3. **Input:** nums = [1,2]<br>
**Output:** [1,2]


## Approach / Intuition 
- Using **Moore's Voting Algorithm**.
- Identify elements that appear more than `n/3` times in the array, as there can be at most two such elements.
- Use two counters and two temporary candidates to track the potential majority elements.
- If we encounter the same element as a candidate, increment its counter; if a counter is zero, assign the element as the candidate.
- When both candidates are already assigned, decrement both counters to balance the count with non-majority elements.
- Count occurrences of the two candidates and check if they appear more than `n/3` times to confirm them as majority elements.



## Algorithm 
1. Set up two counters (`cnt1` and `cnt2`) to track potential majority elements, and two variables (`temp1` and `temp2`) to hold these candidates.
2. Iterate through each element in the array:
   - If the current element matches `temp1`, increment `cnt1`.
   - Else, if it matches `temp2`, increment `cnt2`.
   - Else, if `cnt1` is `0`, assign `temp1` to the current element and set `cnt1` to `1`.
   - Else, if `cnt2` is `0`, assign `temp2` to the current element and set `cnt2` to `1`.
   - Otherwise, decrement both `cnt1` and `cnt2` to balance out non-majority elements.
3. After identifying potential candidates, reset `cnt1` and `cnt2` to zero to validate their actual counts.
4. Iterate through the array again to count the occurrences of `temp1` and `temp2`.
5. If `cnt1` is greater than `n/3`, add `temp1` to the result list. If `cnt2` is greater than `n/3`, add `temp2` to the result list.
6. Return the list of elements that appear more than `n/3` times.



## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)



## Code
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        if not nums:
            return []
        cnt1, cnt2, temp1, temp2 = 0, 0, None, None
        for n in nums:
            if temp1 == n:
                cnt1 += 1
            elif temp2 == n:
                cnt2 += 1
            elif cnt1 == 0:
                temp1 = n
                cnt1 = 1
            elif cnt2 == 0:
                temp2 = n
                cnt2 = 1
            else:
                cnt1 -= 1
                cnt2 -= 1
        cnt1, cnt2 = 0, 0
        for i in nums:
            if i == temp1:
                cnt1 +=1
            elif i == temp2:
                cnt2 += 1
        ans = []
        if cnt1 > len(nums) // 3:
            ans.append(temp1)
        if cnt2 > len(nums) // 3:
            ans.append(temp2)
        return ans
```