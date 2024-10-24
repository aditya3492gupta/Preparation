# [Binary Tree Vertical Order Traversal](https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/)

## Problem Statement
- Given the `root` of a binary tree, return the **vertical order** traversal of its nodes' values. (i.e., from top to bottom, column by column).
- If two nodes are in the same row and column, the order should be from **left to right**.



## Constraints
- The number of nodes in the tree is in the range `[0, 100]`.
- -100 <= Node.val <= 100



## Test Cases
1. **Input:**  root = [3,9,20,null,null,15,7] <br>
**Output:** \[[9],[3,15],[20],[7]]
2. **Input:** root = [3,9,8,4,0,1,7] <br>
**Output:** \[[4],[9],[3,0,1],[8],[7]]
3. **Input:** root = [1,2,3,4,10,9,11,null,5,null,null,null,null,null,null,null,6] <br>
**Output:** \[[4],[2,5],[1,10,9,6],[3],[11]]



## Approach / Intuition 
- Using **vertical line** for the traversal and **BFS**.
- The `root` of the tree starts at `0` and left part goes for `line - 1` and right for `line + 1`.
- The `map` stores it in ascending order of the line and the `vector` stores all the nodes in the line.




## Algorithm 
1. Initialize `mp` that stores `line` as key and `node` that are present in the particular `line` as value and `q` for performing the **BFS** as it will store the `node` and the `line`.
2. Use the `node` and `line` from the queue to insert the `node` in `mp` at the particular position.
3. Now the `vector` in`mp` is storing the required nodes in the required order.



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
    vector<vector<int>> verticalOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if(root == nullptr)
            return ans;
        map<int, vector<int>> mp;
        queue<pair<TreeNode *, int>> q;
        q.push({root, 0});
        while(!q.empty()){
            int sz = q.size();
            for(int i = 0 ; i < sz ; i++){
                auto [node, line] = q.front();
                q.pop();
                mp[line].push_back(node->val);
                if(node->left){
                    q.push({node->left, line - 1});
                }
                if(node->right){
                    q.push({node->right, line + 1});
                }
            }
        }
        for(auto i : mp){
            ans.push_back(i.second);
        }
        return ans;
    }
};
```