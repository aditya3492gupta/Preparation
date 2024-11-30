# [Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/description/)

## Problem Statement
- You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists.
- The depth of an integer is the number of lists that it is inside of. For example, the nested list `[1,[2,2],[[3],2],1]` has each integer's value set to its depth.
- Return the sum of each integer in `nestedList` multiplied by its depth.



## Constraints
- 1 <= nestedList.length <= 50
- The values of the integers in the nested list is in the range [-100, 100].
- The maximum depth of any integer is less than or equal to 50.




## Test Cases
1. **Input:** nestedList = \[[1,1],2,[1,1]] <br>
**Output:** 10
2. **Input:** nestedList = \[1,[4,[6]]] <br>
**Output:** 27
3. **Input:** nestedList = [0] <br>
**Output:** 0




## Approach / Intuition 
- Using **BFS Algorithm**.
- I Each integer's value is multiplied by its depth in the nested list.
- Use a queue to process elements level by level, aligning with depth computation.
- Add integers to the total and enqueue nested lists for further exploration.
- After processing all elements at one level, increment depth for the next.
- Sum the weighted contributions of all integers and return the result.




## Algorithm 
1. Enqueue all elements of the input list into the queue. Start with a depth of 1.
2. Process all elements at the current depth level before moving to the next.
3. If it is an integer, add its value (multiplied by the current depth) to the total sum. If it is a nested list, enqueue all its inner elements for processing in the next level.
4. Once all elements at the current depth level are processed, increment the depth counter.
5. After processing all levels, return the accumulated weighted sum.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)




## Code
```cpp
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Constructor initializes an empty nested list.
 *     NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     NestedInteger(int value);
 *
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Set this NestedInteger to hold a single integer.
 *     void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     void add(const NestedInteger &ni);
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class Solution {
public:
    int depthSum(vector<NestedInteger>& nestedList) {
        queue<NestedInteger> q;
        for(NestedInteger i : nestedList)
            q.push(i);
        int depth = 1;
        int total = 0;
        while(!q.empty()){
            int sz = q.size();
            for(int i = 0 ; i < sz ; i++){
                NestedInteger nest = q.front();
                q.pop();
                if(nest.isInteger())
                    total += nest.getInteger() * depth;
                else{
                    for(NestedInteger nestDepth : nest.getList())
                        q.push(nestDepth);
                }
            }
            depth++;
        }
        return total;
    }
};
```