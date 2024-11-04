# [Word Ladder ll](https://leetcode.com/problems/word-ladder-ii/description/)

## Problem Statement
- A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:
    - Every adjacent pair of words differs by a single letter.
    - Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
    - `sk == endWord`  
- Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return all the **shortest transformation sequences** from `beginWord` to `endWord`, or an empty list if no such sequence exists. Each sequence should be returned as a list of the words `[beginWord, s1, s2, ..., sk]`.


## Constraints
- 1 <= beginWord.length <= 5
- endWord.length == beginWord.length
- 1 <= wordList.length <= 500
- wordList[i].length == beginWord.length
- `beginWord, endWord, and wordList[i]` consist of lowercase English letters.
- beginWord != endWord
- All the words in `wordList` are **unique**.
- The **sum** of all shortest transformation sequences does not exceed 10<sup>5</sup>.


## Test Cases
1. **Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"] <br>
**Output:** \[["hit","hot","dot","dog","cog"],["hit","hot","lot","log","cog"]]
2. **Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]<br>
**Output:** []



## Approach / Intuition 
- Using **BFS and DFS algorithm**.
- Use BFS from `beginWord` to find the shortest path lengths to `endWord`, storing each word's transformation step in `mp`.
- For each word, generate all possible one-letter transformations, adding valid ones to the queue and marking them with the current step
- Stop BFS if `endWord` is reached to ensure shortest paths only, as BFS explores all paths at the current depth before moving deeper.
- Use DFS from `endWord` to `beginWord`, adding transformations to `ans` if they match `mp's` shortest step condition.
- Reverse each valid path in **DFS** and add to `ans`, which collects all shortest transformation sequences.



## Algorithm 
1. Start **BFS** from `beginWord` with a queue, storing each word's step in a map (`mp`)
2. For each word in BFS, try all one-letter transformations and add valid ones to queue with `step + 1`.
3. Stop **BFS** when `endWord` is reached to ensure shortest paths only are stored in `mp`.
4. Use **DFS** from `endWord` to `beginWord`, building paths by checking `mp` for words one step shorter.
5. Reverse each valid path found in DFS and store in `ans` for all shortest transformation sequences.


## Complexity
##### Time Complexity
- \(O(n * m + P * m)\)
##### Space Complexity
- \(O(n * m + P * m)\)

## Code
```cpp
class Solution {
public:
    unordered_map<string, int> mp;
    vector<vector<string>> ans;
    string s;
    void dfs(string endWord, vector<string> &seq){
        if(s == endWord){
            reverse(seq.begin(), seq.end());
            ans.push_back(seq);
            reverse(seq.begin(), seq.end());
            return;
        }
        int sz = endWord.size();
        int step = mp[endWord];
        for(int i = 0 ; i < sz ; i++){
            char og = endWord[i];
            for(char c = 'a' ; c <= 'z' ; c++){
                endWord[i] = c;
                if(mp.find(endWord) != mp.end() and mp[endWord] + 1 == step){
                    seq.push_back(endWord);
                    dfs(endWord, seq);
                    seq.pop_back();
                }
                endWord[i] = og;
            }
        }
    }
    vector<vector<string>> findLadders(string beginWord, string endWord,
                                       vector<string>& wordList) {
        unordered_set<string> st(wordList.begin(), wordList.end());
        queue<string> q;
        q.push({beginWord});
        s = beginWord;
        mp[beginWord] = 1;
        int sz = beginWord.size();
        st.erase(beginWord);
        while(!q.empty()){
            string word = q.front();
            int step = mp[word];
            q.pop();
            if(endWord == word)
                break;
            for(int i = 0 ; i < sz ; i++){
                char og = word[i];
                for(char c = 'a' ; c <= 'z' ; c++){
                    word[i] = c;
                    if(st.count(word)){
                        q.push(word);
                        st.erase(word);
                        mp[word] = step + 1;
                    } 
                }
                word[i] = og;
            }
        }
        if(mp.find(endWord) != mp.end()){
            vector<string> seq;
            seq.push_back(endWord);
            dfs(endWord, seq);
        }
        return ans;
    }
};
```     