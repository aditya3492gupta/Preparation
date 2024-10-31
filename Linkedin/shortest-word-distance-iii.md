# [Shortest Word Distance lll](https://leetcode.com/problems/shortest-word-distance-iii/description/)

## Problem Statement
- Given an array of strings `wordsDict` and two strings that already exist in the array `word1` and `word2`, return the shortest distance between the occurrence of these two words in the list.
- **Note** that `word1` and `word2` may be the same. It is guaranteed that they represent two individual words in the list.


## Constraints
- 1 <= wordsDict.length <= 10<sup>5</sup>
- 1 <= wordsDict[i].length <= 10
- `wordsDict[i]` consists of lowercase English letters.
- `word1` and `word2` are in wordsDict.

## Test Cases
1. **Input:** wordsDict = ["practice", "makes", "perfect", "coding", "makes"], word1 = "makes", word2 = "coding" <br>
**Output:** 1
2. **Input:** wordsDict = ["practice", "makes", "perfect", "coding", "makes"], word1 = "makes", word2 = "makes"<br>
**Output:** 3

## Approach / Intuition 
- Using **2 Pointer approach**.
- Need to find the words at the nearest indices.
- If the two words are same then the previous values of `a` will be given to `b`. 

## Algorithm 
1. Iterate over the `wordsDict` and start comparing it with `word1` and `word2`.
2. If `word1` matches then check if the `word1` is equal to the `word2`.
3. If found true then assign the previous value of `a` to `b` and assign `b = i`.
4. Then `a = i`.
5. Check if the current word is equal to `word2`, if true then assign `b = i`.

## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)

## Code
```python
class Solution(object):
    def shortestWordDistance(self, wordsDict, word1, word2):
        """
        :type wordsDict: List[str]
        :type word1: str
        :type word2: str
        :rtype: int
        """
        ans = n = len(wordsDict)
        a, b = -1, -1
        for i in range(n):
            if wordsDict[i] == word1:
                if word1 == word2:
                    b = a
                a = i
            elif wordsDict[i] == word2:
                b = i
            if a != -1 and b != -1:
                ans = min(ans, abs(a - b))
        return ans
        
```