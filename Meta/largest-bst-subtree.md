# [Largest BST Subtree](https://leetcode.com/problems/largest-bst-subtree/description/)

## Problem Statement
- Given the root of a binary tree, find the largest 
subtree, which is also a Binary Search Tree (BST), where the largest means subtree has the largest number of nodes.
- A Binary Search Tree (BST) is a tree in which all the nodes follow the below-mentioned properties:
    - The left subtree values are less than the value of their parent (root) node's value.
    - The right subtree values are greater than the value of their parent (root) node's value.




## Constraints
- The number of nodes in the tree is in the range [0, 10<sup>4</sup>].
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup>




## Test Cases
1. **Input:** root = [10,5,15,1,8,null,7] <br>
**Output:** 3
2. **Input:**  root = [4,2,7,2,3,5,null,2,null,null,null,null,null,1] <br>
**Output:** 2




## Approach / Intuition 
- Process left and right subtrees first to ensure all data is ready for the current node.
- Check if the current node satisfies BST properties with respect to its left and right subtrees.
- Calculate the size of the BST and update the min/max range for the subtree.
- Maintain a global variable `res` to store the size of the largest BST found so far.
- If the current subtree is not a BST, propagate the largest valid subtree size from its children.




## Algorithm 
1. For each node, recursively check its left and right subtrees to determine. If they are valid BSTs. Their minimum and maximum values. Their sizes.
2. A subtree rooted at node is a BST. Its left subtree is a BST, and its right subtree is a BST. The node's value is greater than the maximum value in the left subtree (if it exists) and less than the minimum value in the right subtree (if it exists).
3. If the current subtree is a BST, calculate its size and update the global res if it is larger than the previous largest BST. Otherwise, return the size of the largest BST found in its left or right subtree.
4. Process the left and right children before validating the current node to ensure all necessary information (size, min, max) is available.




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
    int largestBSTSubtree(TreeNode* root) {
        int res = 0;
        int mini, maxi;
        bool b = isBST(root, res, mini, maxi);
        return res;
    }
    bool isBST(TreeNode* node, int& res, int& mini, int& maxi) {
        if (!node)
            return true;
        int left_size=0, right_size=0;
        int left_mini, left_maxi, right_mini, right_maxi;
        bool leftB = isBST(node->left, left_size, left_mini, left_maxi);
        bool rightB = isBST(node->right, right_size, right_mini, right_maxi);
        if (leftB && rightB) {
            if ( (!node->left || node->val > left_maxi) && (!node->right || node->val < right_mini) ) {
                res = left_size+right_size+1;
                mini = node->left ? left_mini : node->val;
                maxi = node->right ? right_maxi : node->val;
                return true;
            }
        }
        res = max(left_size, right_size);
        return false;
    }
};
```