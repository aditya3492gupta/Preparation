# [Zigzag Iterator](https://leetcode.com/problems/zigzag-iterator/description/)

## Problem Statement
- Given two vectors of integers `v1` and `v2`, implement an iterator to return their elements alternately.
- Implement the `ZigzagIterator` class:
    - `ZigzagIterator(List<int> v1, List<int> v2)` initializes the object with the two vectors `v1` and `v2`.
    - `boolean hasNext()` returns `true` if the iterator still has elements, and `false` otherwise.
    - `int next()` returns the current element of the iterator and moves the iterator to the next element.




## Constraints
- 0 <= v1.length, v2.length <= 1000
- 1 <= v1.length + v2.length <= 2000
- -2<sup>31</sup> <= v1[i], v2[i] <= 2<sup>31</sup> - 1



## Test Cases
1. **Input:** v1 = [1,2], v2 = [3,4,5,6] <br>
**Output:** [1,3,2,4,5,6]
2. **Input:** v1 = [1], v2 = []<br>
**Output:** [1]
3. **Input:** v1 = [], v2 = [1]<br>
**Output:** [1]




## Approach / Intuition 
- Use a queue to manage the order of access for the two vectors.
- At initialization, only add non-empty vectors to the queue.
- For next, fetch the front pair (vector pointer and index), retrieve the value, and update the index.
- Reinsert the updated pair into the queue if there are more elements in the vector.
- Use hasNext to check if the queue still contains elements to iterate over.





## Algorithm 
1. A queue is used to store pairs of pointers to vectors and their current indices. Only non-empty vectors are added to the queue during initialization:
    - For v1, if it has elements, push a pair containing a pointer to v1 and index 0.
    - Similarly, add v2 if it is non-empty.
2. Retrieve the front of the queue, which contains the vector pointer and current index. Extract the value at the current index of the vector. If the next index in the vector is valid, push the updated pair (same vector, incremented index) back into the queue. Return the extracted value.
3. The iterator has more elements if the queue is not empty.





## Complexity
##### Time Complexity
- \(O(1)\)
##### Space Complexity
- \(O(N)\)




## Code
```cpp
class ZigzagIterator {
private:
    queue<pair<vector<int>*, int>> q;
public:
    ZigzagIterator(vector<int>& v1, vector<int>& v2) {
        if (v1.size()) {
            q.push({&v1, 0});
        }
        if (v2.size()) {
            q.push({&v2, 0});
        }
    }
    int next() {
        auto [listPointer, idx] = q.front();
        q.pop();
        int value = listPointer->at(idx);
        if (idx + 1 < listPointer->size()) {
            q.push({listPointer, idx + 1});
        }
        return value;
    }
    bool hasNext() {
        return q.size() > 0;
    }
};
```     