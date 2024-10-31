# [Closest Leaf in a Binary Tree](https://leetcode.com/problems/closest-leaf-in-a-binary-tree/)

## Problem Statement
- Given the `root` of a binary tree where every node has **a unique value** and a target integer `k`, return the value of the **nearest leaf node** to the target `k` in the tree.
- **Nearest to a leaf** means the least number of edges traveled on the binary tree to reach any leaf of the tree. Also, a node is called a leaf if it has no children.

## Constraints
- The number of nodes in the tree is in the range `[1, 50]`.
- 0 <= Node.val, target <= 1000



## Test Cases
1. **Input:** root = [1,3,2], k = 1 <br>
**Output:** 2
2. **Input:** root = [1], k = 1<br>
**Output:** 1
3. **Input:** root = [1,2,3,4,null,null,null,5,null,6], k = 2<br>
**Output:** 3



## Approach / Intuition 
- Using **DFS algorithm and BFS algorithm**.
- Each node in a binary tree can connect to its parent and children, forming an undirected graph where each node has references to its neighbors. This is done through a DFS traversal, creating a graph structure that allows easy traversal in any direction.
- Initialize a BFS from the node that has value `k`. Since the graph is undirected, we can use BFS to explore outward from `k` and find the closest leaf node in the shortest number of steps.
- Using BFS ensures we find the shortest path (minimum steps) to a leaf node. For each node we visit, if it’s a leaf (meaning it has only one neighbor, which would be its parent if it’s not the root), we immediately return that node's value as it's the closest leaf to `k`.
- To prevent cycles and redundant visits, a `seen` set tracks visited nodes.




## Algorithm 
1. Traverse the tree with DFS to construct a graph of parent-child connections.
2. Start BFS from the node with value `k`, adding it to a queue and marking it as visited.
3. For each node in the BFS, if it has no children (or only one parent), it’s a leaf—return its value.
4. For each neighbor, if unvisited, add it to the queue and continue until a leaf is found.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)



## Code
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def findClosestLeaf(self, root, k):
        """
        :type root: Optional[TreeNode]
        :type k: int
        :rtype: int
        """
        graph = collections.defaultdict(list)
        def dfs(node, par = None):
            if node:
                graph[node].append(par)
                graph[par].append(node)
                dfs(node.left, node)
                dfs(node.right, node)
        dfs(root)
        queue = collections.deque(node for node in graph if node and node.val == k)
        seen = set(queue)
        while queue:
            node = queue.popleft()
            if node:
                if len(graph[node]) <= 1:
                    return node.val
                for x in graph[node]:
                    if x not in seen:
                        seen.add(x)
                        queue.append(x)        
```