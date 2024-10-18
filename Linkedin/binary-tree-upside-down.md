# [Binary Tree Upside Down](https://leetcode.com/problems/binary-tree-upside-down/)

## Problem Statement
- Given the `root` of a binary tree, turn the tree upside down and return the `new root`.
- You can turn a binary tree upside down with the following steps:
    1. The ***original left*** child becomes the ***new root***.
    2. The ***original root*** becomes the ***new right*** child.
    3. The ***original right*** child becomes the ***new left*** child.


## Constraints
- The number of nodes in the tree will be in the range `[0, 10]`.
- 1 <= Node.val <= 10
- Every right node in the tree has a sibling (a left node that shares the same parent).
- Every right node in the tree has no children.


## Test Cases
1. **Input:** root = [] <br>
**Output:** []
2. **Input:** root = [1,2,3,4,5]<br>
**Output:** [4,5,2,null,null,3,1]

## Approach / Intuition 
- Using DFS with recursion.
- Move to leftmost node of the tree and then using recursive call back perform the operations.
- Make the left child of current root node the new root, right child of the current root new left and current root new child. 

## Algorithm 
1. Move to the left child until either the node becomes `nullptr` or the left child of the node becomes `nullptr` and assign it as the `new root` of the resultant tree.
2. Call back to the previous node and assign its `right child` as the `left grandchild` of the current node or the `left child` of the `new root` and the `current node` as the `right grandchild` of the `current node` or `right child` of the `new root`.
3. Assign the `left` and `right child` of the current root as `nullptr` and return the address of `new root`.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)

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
    TreeNode *buildTree(TreeNode *root){
        if(root == nullptr or root->left == nullptr)
            return root;
        TreeNode *newRoot = buildTree(root->left);
        root->left->left = root->right;
        root->left->right = root;
        root->left = nullptr;
        root->right = nullptr;
        return newRoot;
    }
    TreeNode* upsideDownBinaryTree(TreeNode* root) {
        if(root == nullptr)
            return root;
        TreeNode *ans =  buildTree(root);
        return ans;        
    }
};
```