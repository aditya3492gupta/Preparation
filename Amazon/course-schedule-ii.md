# [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)




## Problem Statement
- There are a total of `numCourses` courses you have to take, labeled from 0 to `numCourses - 1`. You are given an array prerequisites where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.
- Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.




## Constraints
- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= numCourses * (numCourses - 1)
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- ai != bi
- All the pairs [ai, bi] are distinct.




## Test Cases
1. **Input:**  numCourses = 2, prerequisites = \[[1,0]] <br>
**Output:** [0,1]
2. **Input:** numCourses = 4, prerequisites = \[[1,0],[2,0],[3,1],[3,2]]<br>
**Output:** [0,2,1,3]





## Approach / Intuition 
- Using **Topological Sort** with **BFS Algorithm** .
- Represent courses and prerequisites as a directed graph where edges point from prerequisites to dependent courses.
- Start with courses having zero prerequisites (indegree of 0) as they can be taken without dependencies.
- Use BFS to remove dependencies for each course; add courses with no remaining prerequisites to the queue.
- If all courses are processed (ans.size() == n), no cycles exist, so completing all courses is feasible, return `ans` otherwise, there's a dependency loop.




## Algorithm 
1. Create an adjacency list `adj` where each course points to the courses that depend on it. Use an `indegree` array to count prerequisites for each course.
2. For each prerequisite pair `[a, b]`, add `b` to `adj[a]` (meaning `a` must be taken before `b`). Increment `indegree[b]` by `1` to record that `b` has an additional prerequisite.
3. Push all courses with `indegree[i] == 0` into a queue since they have no prerequisites and can be taken initially.
4. While the queue is not empty, remove the front course `t`, add it to the `ans` list, and decrement the indegree of all its dependent courses. If a dependent course’s `indegree` becomes `0`, push it into the queue as it can now be taken.
5. If `ans.size() == n`, then all courses can be completed (no cycle), return 'ans'. If `ans.size() < n`, a cycle exists, meaning it's impossible to finish all courses. Return `{}` accordingly.




## Complexity
##### Time Complexity
- O(N + P)
##### Space Complexity
- O(N + P)



## Code
```cpp
class Solution {
public:
    vector<int> findOrder(int n, vector<vector<int>>& graph) {
        vector<int> ans;
        vector<int> indegree(n, 0);
        vector<int> adj[n];
        queue<int> qu;
        for (auto it : graph) 
            adj[it[1]].push_back(it[0]);
        for (int i = 0; i < n; i++) 
            for (auto it : adj[i])
                indegree[it]++;
        for (int i = 0; i < n; i++) 
            if (indegree[i] == 0)
                qu.push(i);
        while (!qu.empty()) {
            int node = qu.front();
            qu.pop();
            ans.push_back(node);
            for (auto it : adj[node]) {
                indegree[it]--;
                if (indegree[it] == 0)
                    qu.push(it);
            }
        }
        if (ans.size() == n)
            return ans;
        else
            return {};
    }
};
```