# [Split BST](https://leetcode.com/problems/split-bst/)

## Problem Statement
- Given the `root` of a binary search tree `(BST)` and an integer `target`, split the tree into two subtrees where the **first subtree** has nodes that are all **smaller or equal** to the `target` value, while the **second subtree** has all nodes that are **greater** than the `target` value.
- Most of the structure of the **original** tree should remain. Formally, for any child `c` with parent `p` in the **original** tree, if they are both in the same subtree after the split, then node `c` should still have the parent `p`.

## Constraints
- The number of nodes in the tree is in the range `[1, 50]`.
- 0 <= Node.val, target <= 1000


## Test Cases
1. **Input:** root = [4,2,6,1,3,5,7], target = 2 <br>
**Output:** \[[2,1],[4,3,6,null,null,5,7]]
2. **Input:** root = [1], target = 1<br>
**Output:** \[[1],[]]

## Approach / Intuition 
- Find the path from `root` to the leaf node including the `target` using stack.
- This would help in maintaining the structure of the tree.
- `ans` contains two elements `ans[0]` for **first subtree** and `ans[1]` for **second subtree**.
- Using this path which contains the splitting point split the tree.

## Algorithm 
1. Declare a ***stack*** that stores ***TreeNode*** as elements.
2. Find the path from root to leaf node that includes `target` which acts as the splitting point of the tree.
3. Start iterating through the nodes that are stored in `st` by using the topmost element and compare it to the `target`.
4. If the current `node` is greater than the `target` then update `node->left = ans[1]` making the `node` as current root and whatever `ans[1]` is storing, make the left subtree of the `node` and `ans[1] = node`.
5. Else `node->right = ans[0]` and `ans[0] = node`.

## Complexity
##### Time Complexity
- \(O(logN)\)
##### Space Complexity
- \(O(logN)\)

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
    vector<TreeNode*> splitBST(TreeNode* root, int target) {
        vector<TreeNode *> ans(2, nullptr);
        if(root == nullptr)
            return ans;
        stack<TreeNode *>st;
        while(root != nullptr){
            st.push(root);
            if(root->val > target)
                root = root->left;
            else
                root = root->right;
        }
        while(!st.empty()){
            TreeNode *node = st.top();
            st.pop();
            if(node->val > target){
                node->left = ans[1];
                ans[1] = node;
            }
            else{
                node->right = ans[0];
                ans[0] = node;
            }
        }
        return ans;
    }
};
```