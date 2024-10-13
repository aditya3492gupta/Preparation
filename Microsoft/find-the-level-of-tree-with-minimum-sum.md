# [Find the Level of Tree With Minimum Sum](https://leetcode.com/problems/find-the-level-of-tree-with-minimum-sum/description/)

## Problem Statement
- Given the `root` of a binary tree root where each node has a value, return the level of the tree that has the **minimum** sum of values among all the levels (in case of a tie, return the **lowest** level).
- Note that the root of the tree is at `level 1` and the level of any other node is its distance from the `r`oot + 1`.

 


## Constraints
- The number of nodes in the tree is in the range [1, 10<sup>5</sup>].
- 1 <= Node.val <= 10<sup>9</sup>


## Test Cases
1. **Input:** [36,17,10,null,null,24] <br>
**Output:** 3
2. **Input:** root = [50,6,2,30,80,7] <br>
**Output:** 2

## Approach / Intuition 
- Using the ***BFS algorithm***.
- Calculating the sum of the nodes at each level and then comparing the current sum with the minimum value found previously.
- Update `ans` if new minimum value found/

## Algorithm 
1. Initialize a queue that stores a `TreeNode` as its element and use it for applying the BFS algorithm.
2. Visit each node at a particular `level` and then add its `val` to `x` and then compare `x` with `mn`.
3. If `mn` is greater then `x` then update `mn` and `ans` with new values.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)

## Code
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int minimumLevel(TreeNode* root) {
        int ans = 1;
        long long mn = LONG_MAX;
        if(root == nullptr)
            return ans;
        queue<TreeNode *> q;
        q.push(root);
        int level = 0;
        while(!q.empty()){
            int n = q.size();
            long long x = 0;
            level++;
            for(int i = 0 ; i < n ; i++){
                TreeNode *temp = q.front();
                x += temp->val;
                q.pop();
                if(temp->left)
                    q.push(temp->left);
                if(temp->right)
                    q.push(temp->right);
            }
            if(mn > x){
                mn = x;
                ans = level;
            }
        }
        return ans;
    }
};
```