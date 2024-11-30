# [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/description/)

## Problem Statement
-There is a new alien language that uses the English alphabet. However, the order of the letters is unknown to you.
- You are given a list of strings `words` from the alien language's dictionary. Now it is claimed that the strings in `words` are sorted lexicographically by the rules of this new language.
- If this claim is incorrect, and the given arrangement of string in `words` cannot correspond to any order of letters, return `""`.
- Otherwise, return a string of the unique letters in the new alien language sorted in lexicographically increasing order by the new language's rules. If there are multiple solutions, return any of them.




## Constraints
- 1 <= words.length <= 100
- 1 <= words[i].length <= 100
- words[i] consists of only lowercase English letters.




## Test Cases
1. **Input:** words = ["wrt","wrf","er","ett","rftt"] <br>
**Output:** "wertf"
2. **Input:** words = ["z","x"]<br>
**Output:** "zx"
3. **Input:** words = ["z","x","z"]<br>
**Output:** ""




## Approach / Intuition 
- Using **Topological Sort**.
- Treat each character as a node and deduce their order by creating directed edges based on the first mismatched characters between consecutive words.
- Ensure no invalid order exists by checking for cycles in the graph using a topological sorting approach.
- Use an indegree map to count how many prerequisites each character has, starting with nodes that have zero prerequisites.
- Use a queue to process characters in topological order, reducing indegrees for their neighbors as they're added to the result.
- If the output string includes all unique characters, it represents a valid order; otherwise, return an empty string for an invalid input.




## Algorithm 
1. Create an `indegree` map for all unique characters, initializing values to 0. Initialize an adjacency list `(graph)` for storing edges.
2. Compare adjacent words to deduce the order of characters. For the first differing characters in two words, add a directed edge in the graph and update the `indegree` of the destination character.
3. Use a queue to process characters with an `indegree` of `0`. Add these characters to the result string and reduce the `indegree` of their neighbors. Push neighbors with zero indegree into the queue.
4. f the result string's length equals the number of unique characters, return the result. Otherwise, return an empty string.




## Complexity
##### Time Complexity
- \(O(N+M)\)
##### Space Complexity
- \(O(N+M)\)




## Code
```cpp
class Solution {
public:
    string alienOrder(vector<string>& words) {
        if (words.size() == 0) return "";
        unordered_map<char, int> indegree;
        unordered_map<char, unordered_set<char>> graph;
        for (int i = 0; i < words.size(); i++) {
            for (int j = 0; j < words[i].size(); j++) {
                char c = words[i][j];
                indegree[c] = 0; 
            }
        }
        for (int i = 0; i < words.size() - 1; i++) {
            string cur = words[i];
            string nex = words[i + 1];
            if (cur.size() > nex.size() && cur.compare(0, nex.length(), nex) == 0) {
                return "";
            }
            int len = min(cur.size(), nex.size());
            for (int j = 0; j < len; j++) {
                if (cur[j] != nex[j]) {
                    unordered_set<char> set = graph[cur[j]];
                    if (set.find(nex[j]) == set.end()) {
                        graph[cur[j]].insert(nex[j]); 
                        indegree[nex[j]]++; 
                    }
                    break;                        
                }
            }
        }
        string ans;
        queue<char> q;
        for (auto& e : indegree) {
            if (e.second == 0) {
                q.push(e.first);
            }
        }
        while(!q.empty()) {
            char cur = q.front();
            q.pop();
            ans += cur; 
            if (graph[cur].size() != 0) {
                for (auto& e : graph[cur]) {
                    indegree[e]--;
                    if (indegree[e] == 0) {
                        q.push(e);
                    }
                }
            }            
        }
        return ans.length() == indegree.size() ? ans : "";
    }
};
```