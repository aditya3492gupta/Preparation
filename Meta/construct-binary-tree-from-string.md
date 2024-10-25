# [Construct Binary Tree From String](https://leetcode.com/problems/construct-binary-tree-from-string/description/)

## Problem Statement
- You need to construct a binary tree from a string consisting of parenthesis and integers.
- IThe whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. 
- The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. 
- You always start to construct the **left** child node of the parent first if it exists.



## Constraints
- 0 <= s.length <= 3 * 10<sup4</sup>
- `s` consists of digits, `'('`, `')'`, and `'-'` only.



## Test Cases
1. **Input:** s = "4(2(3)(1))(6(5))" <br>
**Output:** [4,2,6,3,1,5]
2. **Input:** s = "4(2(3)(1))(6(5)(7))" <br>
**Output:** [4,2,6,3,1,5,7]
3. **Input:** s = "-4(2(3)(1))(6(5)(7))" <br>
**Output:** [-4,2,6,3,1,5,7]



## Approach / Intuition 
- Using stack for storing the `node`.
- Traverse the input string `s` character by character to extract integers and parentheses. The integers represent node values, while parentheses `(` and `)` denote the structure of the binary tree.
- Whenever an integer is extracted, it is converted into a `TreeNode` and pushed onto a stack. The stack helps in building parent-child relationships between nodes.
- After creating a node, check the top node of the stack. If its **left child** is `nullptr`, assign the newly created node as the **left child**. Otherwise, assign it as the **right child**.
- Opening parentheses `(` indicate the start of child nodes, while closing parentheses `)` mean the child subtree is finished, so the top node is popped from the stack.




## Algorithm 
1. Initialize an empty stack `st` and a string `temp` to accumulate digits for node values.
2. Traverse the input string `s` character by character, appending digits or `'-'` to `temp` and skipping `'('`.
3. When encountering `')'` or after extracting a number, create a `TreeNode` from temp, push it onto the stack, and if the stack isn't empty, link it as the **left or right child** of the node on **top**.
4. Upon encountering `')'`, *pop* the **top** node from the `st` since its subtree is complete.
5. After processing all characters, return the root node, which will either be on top of the stack or the last node created.



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
    TreeNode* str2tree(string s) {
        int n = s.size();
        if(n == 0)
            return nullptr;
        stack<TreeNode*>st;
        string temp;
        for(int i = 0 ; i < n ; i++){
            if(isdigit(s[i]) or s[i] == '-'){
                temp += s[i];
                continue;
            }
            if(temp.size() == 0 and s[i] == '(')
                continue;
            if(temp.size() == 0 and s[i] == ')'){
                st.pop();
                continue;
            }
            TreeNode* node = new TreeNode(stoi(temp));
            temp.clear();
            if(st.empty()){
                st.push(node);
                continue;
            }
            if(st.top()->left == nullptr)
                st.top()->left = node;
            else
                st.top()->right = node;
            st.push(node);
            if(s[i] == ')')
                st.pop();
        }
        if(!temp.empty())
            return new TreeNode(stoi(temp));
        return st.top();
    }
};
```