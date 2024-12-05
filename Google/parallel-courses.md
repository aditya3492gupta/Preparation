# [Parallel Courses](https://leetcode.com/problems/parallel-courses/description/)

## Problem Statement
- You are given an integer `n`, which indicates that there are `n` courses labeled from `1 to n`. You are also given an array `relations` where `relations[i] = [prevCoursei, nextCoursei]`, representing a prerequisite relationship between course `prevCoursei` and course `nextCoursei`: course `prevCoursei` has to be taken before course `nextCoursei`.
- In one semester, you can take any number of courses as long as you have taken all the prerequisites in the previous semester for the courses you are taking.
- Return the minimum number of semesters needed to take all courses. If there is no way to take all the courses, return `-1`.




## Test Cases
1. **Input:** n = 3, relations = \[[1,3],[2,3]] <br>
**Output:** 2
2. **Input:** n = 3, relations = \[[1,2],[2,3],[3,1]] <br>
**Output:** -1




## Constraints
- 1 <= n <= 5000
- 1 <= relations.length <= 5000
- relations[i].length == 2
- 1 <= prevCoursei, nextCoursei <= n
- prevCoursei != nextCoursei
- All the pairs [prevCoursei, nextCoursei] are unique.




## Approach / Intuition 
- Using **Topological Sort**.
- Calculate the `indegree` of all the nodes by 0-indexing.
- Move to each `course` and check for the completion of the previous course.
- Clear the current course.





## Algorithm 
1. Construct a adjacency list `adj` and `indegree` of the current DAG using the 0-indexing.
2. Push the nodes in `q` with `indegree == 0`.
3. Use the `topological sort` and push `course` whose previous course is completed.
4. Increment `ans` and decrement `n`.
5. Check whether the `n == 0`, if yes return `ans` else return `-1`





## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(N)\)




## Code
```cpp
class Solution {
public:
    int minimumSemesters(int n, vector<vector<int>>& relations) {
        vector<vector<int>> adj(n);
        vector<int> indegree(n, 0);
        for (auto i : relations) {
            adj[i[0] - 1].push_back(i[1] - 1);
            indegree[i[1] - 1]++;
        }
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0)
                q.push(i);
        }
        int ans = 0;
        while (!q.empty()) {
            int sz = q.size();
            for (int i = 0; i < sz; i++) {
                n--;
                int node = q.front();
                q.pop();
                for (auto j : adj[node]) {
                    indegree[j]--;
                    if (indegree[j] == 0)
                        q.push(j);
                }
                adj[node].clear();
            }
            ans++;
        }
        return n == 0 ? ans : -1;
    }
};
```     