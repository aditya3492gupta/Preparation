# [Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/description/)

## Problem Statement
- Given the `root` of a binary tree, collect a tree's nodes as if you were doing this:
    - Collect all the leaf nodes.
    - Remove all the leaf nodes.
    - Repeat until the tree is empty.


## Constraints
- The number of nodes in the tree is in the range `[1, 100]`.
- -100 <= Node.val <= 100


## Test Cases
1. **Input:** root = [1,2,3,4,5] <br>
**Output:** \[[4,5,3],[2],[1]]
2. **Input:** root = [1]<br>
**Output:** \[[1]]

## Approach / Intuition 
- Using **DFS with recursion**.
- Move to the `leaf node` and find that the height i.e., *0*. 
- If the current height is not visited previously then create space for it.
- Push the `node` to `ans` according to the height.
- Move back to the `parent` if `right child` present move to the `right child` else work on the `parent` of the last visited node example, `parent` of leaf node, height = 1.

## Algorithm 
1. Move to the `left child` until finds `nullptr` then finds its height.
2. If the height is not previously visited then create space.
3. Push the `val` of node to the `ans`.
4. Do a call back to last node and if `right child` is present move to it else find height of the node and push its `val` to `ans`.

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
    int addLeaves(TreeNode *root, vector<vector<int>> &ans){
        if(root == nullptr)
            return -1;
        int left = addLeaves(root->left, ans);
        int right = addLeaves(root->right, ans);
        int height = max(left, right) + 1;
        if(ans.size() == height)
            ans.push_back({});
        ans[height].push_back(root->val);
        return height;
    }
    vector<vector<int>> findLeaves(TreeNode* root) {
        vector<vector<int>> ans;
        if(root == nullptr)
            return ans;
        int x = addLeaves(root, ans);
        return ans;
    }
};
```