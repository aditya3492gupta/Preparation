# [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/description/)

## Problem Statement
- Given the `root` of a binary search tree and a node `p` in it, return the **in-order successor** of that node in the **BST**. If the given node has no **in-order successor** in the tree, return `null`.
- The successor of a node `p` is the node with the **smallest key greater** than `p.val`.



## Constraints
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>5</sup> <= Node.val <= 10<sup>5</sup>
- All Nodes will have unique values.

## Test Cases
1. **Input:** root = [2,1,3], p = 1 <br>
**Output:** 2
2. **Input:** root = [5,3,6,2,4,null,null,1], p = 6 <br>
**Output:** null

## Approach / Intuition 
- Inorder Successor of any node is the smallest node that is greater than it.
- It means that the node is the *leftmost* node of its right child or its parent node.

## Algorithm 
1. If the `right child` is present, return the *leftmost* node in the subtree.
2. Else start iterating from the `root` of the node.
3. If the `p->val > root->val` move to the right child.
4. Else update `ans` with `root` and move to the left child.
5. Return `ans`

## Complexity
##### Time Complexity
- \(O(log*N)\)
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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if(p->right){
            p = p->right;
            while(p->left != nullptr)
                p = p->left;
            return p;
        }
        TreeNode *ans = nullptr;
        while(root != p){
            if(p->val > root->val)
                root = root->right;
            else
                root = (ans = root)->left;
        }
        return ans;
    }
};
```