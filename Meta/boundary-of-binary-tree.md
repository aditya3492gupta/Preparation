# [Boundary of Binary Tree](https://leetcode.com/problems/boundary-of-binary-tree/description/)




## Problem Statement
- The boundary of a binary tree is the concatenation of the root, the left boundary, the leaves ordered from left-to-right, and the reverse order of the right boundary.
- The left boundary is the set of nodes defined by the following:
    - The root node's left child is in the left boundary. If the root does not have a left child, then the left boundary is empty.
    - If a node in the left boundary and has a left child, then the left child is in the left boundary.
    - If a node is in the left boundary, has no left child, but has a right child, then the right child is in the left boundary.
    - The leftmost leaf is not in the left boundary.
- The right boundary is similar to the left boundary, except it is the right side of the root's right subtree. Again, the leaf is not part of the right boundary, and the right boundary is empty if the root does not have a right child.
- The leaves are nodes that do not have any children. For this problem, the root is not a leaf.
- Given the `root` of a binary tree, return the values of its boundary.



## Constraints
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -1000 <= Node.val <= 1000



## Test Cases
1. **Input:** root = [1,null,2,3,4] <br>
**Output:**[1,3,4,2]
2. **Input:** root = [1,2,3,4,5,6,null,null,null,7,8,9,10] <br>
**Output:** [1,2,4,7,8,9,10,6,3]
3. **Input:** s = "-4(2(3)(1))(6(5)(7))" <br>
**Output:** [-4,2,6,3,1,5,7]



## Approach / Intuition 
- The boundary traversal will consist of the left boundary, right boundary and the leaf nodes of the tree.
- One thing to keep in mind that the leftmost leaf node and the rightmost leaf node does not get repeated.
- While adding the nodes of the left and right boundary check that the current node is not leaf node.
- Before adding the right boundary reverse the array .
- Do not add the left and right leaf node and add them while adding the leaf nodes only.




## Algorithm 
1. Initialize an empty array `ans`.
2. Call `addLeft` and add the left boundary except the leaf node.
3. Call `addLeaves` and traverse the tree and then add the leaf nodes only.
4. Call `addRight`, store the node in `tempAns` and store nodes in it, then reverse `tempAns` and store them in `ans`.
5. Return the resultant array `ans`.



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
    int isLeaf(TreeNode *root){
        return !root->left and !root->right;
    }
    void addLeft(TreeNode *root, vector<int>&ans){
        while(root != nullptr){
            if(!isLeaf(root))
                ans.push_back(root->val);
            if(root->left)
                root = root->left;
            else
                root = root->right;
        }
    }
    void addLeaves(TreeNode *root,vector<int>&ans){
        if(isLeaf(root)){
            ans.push_back(root->val);
            return;
        }
        if(root->left)
            addLeaves(root->left, ans);
        if(root->right)
            addLeaves(root->right, ans);
    }
    void addRight(TreeNode *root,vector<int>&ans){
        vector<int> tempAns;
        while(root != nullptr){
            if(!isLeaf(root))
                tempAns.push_back(root->val);
            if(root->right)
                root = root->right;
            else
                root = root->left;
        }
        for(int i = tempAns.size() - 1 ; i >= 0 ; i--)
            ans.push_back(tempAns[i]);
    }
    vector<int> boundaryOfBinaryTree(TreeNode* root) {
        vector<int>ans;
        if(root == nullptr)
            return ans;
        if(!isLeaf(root))
            ans.push_back(root->val);
        addLeft(root->left, ans);
        addLeaves(root, ans);
        addRight(root->right, ans);
        return ans;
    }
};
```