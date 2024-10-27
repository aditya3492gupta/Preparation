# [Find All The Lonely Nodes](https://leetcode.com/problems/find-all-the-lonely-nodes/description/)




## Problem Statement
- In a binary tree, a **lonely node** is a node that is the only child of its parent node. 
- The root of the tree is not lonely because it does not have a parent node.
- Given the `root` of a binary tree, return *an array containing the values of all lonely nodes* in the tree. 
- Return the list in **any order**.




## Constraints
- The number of nodes in the `tree` is in the range `[1, 1000]`.
- 1 <= Node.val <= 10<sup>6</sup>




## Test Cases
1. **Input:** root = [1,2,3,null,4] <br>
**Output:** [4]
2. **Input:** root = [7,1,4,6,null,5,3,null,null,null,null,null,2] <br>
**Output:** [6,2]
3. **Input:** root = [11,99,88,77,null,null,66,55,null,null,44,33,null,null,22] <br>
**Output:** [77,55,33,66,44,22]




## Approach / Intuition 
- Using the **DFS algorithm**.
- The lonely node does not have any sibling. 
- Or in other words, the parent of the lonely node has only one child.
- So visit each node and check whether the current node has only one child.




## Algorithm 
1. Initialize an empty array `ans` to store the resultant array.
2. Recursive visit each node using the **BFS** algorithm and check whether the current `node` has only one child.
3. If `true` store it in `ans` else recursively call the `root.left` and `root.right`.
4. Return the resultant array.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(H)\)




## Code
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def getLonelyNodes(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: List[int]
        """
        ans = []
        self.dfs(root, ans)
        return ans
    def dfs(self, root, ans):
        if root is None:
            return
        if root.right is None and root.left:
            ans.append(root.left.val)
        elif root.left is None and root.right:
            ans.append(root.right.val)
        self.dfs(root.left, ans)
        self.dfs(root.right, ans)
        
```