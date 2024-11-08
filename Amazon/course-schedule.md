# [Course Schedule](https://leetcode.com/problems/course-schedule/description/)




## Problem Statement
- There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array prerequisites where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.
- Return `true` if you can finish all courses. Otherwise, return `false`.




## Constraints
- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= 5000
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- All the pairs prerequisites[i] are unique.




## Test Cases
1. **Input:**  numCourses = 2, prerequisites = \[[1,0]] <br>
**Output:** true
2. **Input:** numCourses = 2, prerequisites = \[[1,0],[0,1]]<br>
**Output:** false





## Approach / Intuition 
- Using **Topological Sort** with **BFS Algorithm** .
- Represent courses and prerequisites as a directed graph where edges point from prerequisites to dependent courses.
- Start with courses having zero prerequisites (indegree of 0) as they can be taken without dependencies.
- Use BFS to remove dependencies for each course; add courses with no remaining prerequisites to the queue.
- If all courses are processed (ans.size() == n), no cycles exist, so completing all courses is feasible; otherwise, there's a dependency loop.




## Algorithm 
1. Create an adjacency list `adj` where each course points to the courses that depend on it. Use an `indegree` array to count prerequisites for each course.
2. For each prerequisite pair `[a, b]`, add `b` to `adj[a]` (meaning `a` must be taken before `b`). Increment `indegree[b]` by `1` to record that `b` has an additional prerequisite.
3. Push all courses with `indegree[i] == 0` into a queue since they have no prerequisites and can be taken initially.
4. While the queue is not empty, remove the front course `t`, add it to the `ans` list, and decrement the indegree of all its dependent courses. If a dependent course’s `indegree` becomes `0`, push it into the queue as it can now be taken.
5. If `ans.size() == n`, then all courses can be completed (no cycle). If `ans.size() < n`, a cycle exists, meaning it's impossible to finish all courses. Return `false` accordingly.




## Complexity
##### Time Complexity
- O(N + P)
##### Space Complexity
- O(N + P)



## Code
```cpp
class Solution {
public:
    bool canFinish(int n, vector<vector<int>>& prerequisites) {
        vector<int> adj[n];
        vector<int> indegree(n, 0);
        vector<int> ans;
        for(auto x: prerequisites){
            adj[x[0]].push_back(x[1]);
            indegree[x[1]]++;
        }
        queue<int> q;
        for(int i = 0; i < n; i++){
            if(indegree[i] == 0)
                q.push(i);
        }
        while(!q.empty()){
            auto t = q.front();
            ans.push_back(t);
            q.pop();
            for(auto x: adj[t]){
                indegree[x]--;
                if(indegree[x] == 0)
                    q.push(x);
            }
        }
        return ans.size() == n;
    }
};
```