# [Word Ladder](https://leetcode.com/problems/word-ladder/)

## Problem Statement
- A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary wordList is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:
    - Every adjacent pair of words differs by a single letter.
    - Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
    - `sk == endWord`  
- Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return the **number of words** in the **shortest transformation sequence** from `beginWord` to `endWord`, or `0` if no such sequence exists.


## Constraints
- 1 <= beginWord.length <= 10
- endWord.length == beginWord.length
- 1 <= wordList.length <= 5000
- wordList[i].length == beginWord.length
- `beginWord, endWord, and wordList[i]` consist of lowercase English letters.
- beginWord != endWord
- All the words in `wordList` are **unique**.


## Test Cases
1. **Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"] <br>
**Output:** 5
2. **Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]<br>
**Output:** 0



## Approach / Intuition 
- Using **BFS algorithm**.
- Queue holds each word along with the number of transformation steps taken to reach it.
- Character Replacement iterates through each letter in the current word, trying every possible single-letter change from 'a' to 'z'.
- Valid Transformations (i.e., words in `wordList`) are added to the queue and removed from the set to avoid revisiting.
- End Condition: If `endWord` is reached, return the transformation count; if the queue is exhausted, return 0 (no path found).



## Algorithm 
1. Start by pushing `beginWord` with a step count of 1 into a queue and place all words from `wordList` into a set for quick access.
2. While the queue is not empty, dequeue the current word and its transformation step count.
3. If the current word is `endWord`, return the step count as it represents the shortest transformation sequence.
4. For each character position in the current word, replace it with every letter from 'a' to 'z' to form a new word.
5. If the transformed word exists in the set, it’s a valid transformation. Push it to the queue with an incremented step count and remove it from the set to avoid revisiting. If the queue is exhausted, return 0 (no transformation sequence found).

## Complexity
##### Time Complexity
- \(O(N*M)\)
##### Space Complexity
- \(O(N*M)\)

## Code
```cpp
class Solution {
public:
    int ladderLength(string beginWord, string endWord,
                     vector<string>& wordList) {
        queue<pair<string, int>> q;
        q.push({beginWord, 1});
        unordered_set<string> st(wordList.begin(), wordList.end());
        st.erase(beginWord);
        while (!q.empty()) {
            auto [word, step] = q.front();
            q.pop();
            if (word == endWord)
                return step;
            for (int i = 0; i < word.size(); i++) {
                char og = word[i];
                for (auto j = 'a'; j <= 'z'; j++) {
                    word[i] = j;
                    if (st.find(word) != st.end()) {
                        st.erase(word);
                        q.push({word, step + 1});
                    }
                }
                word[i] = og;
            }
        }
        return 0;
    }
};
```     