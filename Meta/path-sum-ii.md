# [Path Sum 2](https://leetcode.com/problems/path-sum-ii/)

## Problem Statement
- Given the root of a `binary tree` and an integer `targetSum`, return all `root-to-leaf` paths where the sum of the node values in the path equals `targetSum`
- Each path should be returned as a list of the node values, not node references.


## Constraints
- The number of nodes in the tree is in the range `[0, 5000]`.
- -1000 <= Node.val <= 1000
- -1000 <= targetSum <= 1000


## Test Cases
1. **Input:** root = [1,2,3], targetSum = 5 <br>
**Output:** []
2. **Input:** root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22 <br>
**Output:** \[[5,4,11,2],[5,8,4,5]]

## Approach / Intuition 
- Using DFS with recursion.
- Visit every node in the tree and subtract its value from the `targetSum`.
- Push that visited node into `temp` vector.
- Check if at the leaf node the `targetSum` equals to 0, if yes push `temp` to `ans` else pop that node out of `temp`.

## Algorithm 
1. We subtract the value of the current node from `target` and add the current node's value to the `temp` vector, which tracks the path we are currently exploring.
2. If the `target` becomes zero and the current node is a leaf node (i.e., both root->left and root->right are ```nullptr```), this means we have found a valid path whose sum equals the `targetSum`. We then add this path (temp) to the `ans` vector.
3. Otherwise, we recursively explore the left and right subtrees by calling `printPath` on root->left and root->right while passing the updated `temp` and `target` values.
4. After exploring both the left and right subtrees, we backtrack by popping the last node from the `temp` vector to remove the current node's value and revert to the previous state.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(H)\), H = height of the tree

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
    void printPath(TreeNode *root, int target, vector<int> temp, vector<vector<int>>&ans){
        if(root == nullptr)
            return;
        target -= root->val;
        temp.push_back(root->val);
        if(target == 0 and root->left == nullptr and root->right == nullptr)
            ans.push_back(temp);
        else{
            printPath(root->left, target, temp, ans);
            printPath(root->right, target, temp, ans);
        }
        temp.pop_back();
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        vector<vector<int>> ans;
        if(root == nullptr)
            return ans;
        vector<int> temp;
        printPath(root, targetSum, temp, ans);
        return ans;
    }
};
```