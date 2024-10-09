# Meeting Rooms 2

## Problem Statement
- Given an array of meeting time intervals `intervals` where `intervals[i] = [start[i], end[i]]`, return the minimum number of conference rooms required.
- The start time of two intervals could overlap each other.


## Constraints
- \(1 \leq \text{intervals.length} \leq 10^4\)
- \(0 \leq start_i < end_i \leq 10^6\)

## Test Cases
1. **Input:** intervals = \[[0,30],[5,10],[15,20]]<br>
**Output:** 2
2. **Input:** intervals = \[[7,10],[2,4]]<br>
**Output:** 1

## Approach / Intuition - 1
- Sort the meeting in non - descending order wrt start time
- Using the priority queue as min-heap to keep track of the end time of the meetings as it keeps the meeting that finishes earliest at the top.
- At the end time meetings left in the queue will tell us the minimum number of rooms required.

## Algorithm - 1
1. Sort the meeting intervals in ascending order by start time.
2. Create a min-heap / priority queue.
3. Iterate through the intervals
   3.1. If the queue is empty and the end time of the top meeting of the queue is less than or equal to start time of the current meeting then pop the top meeting out of the queue as the meeting is over and new meeting needs to be started.
   3.2. Push the end time of the current meeting.
4. Return the size of the queue as it will tell us about the minimum number of meeting rooms required.

## Complexity
##### Time Complexity
- \(O(N \log N)\)
##### Space Complexity
- \(O(N)\)

## Code
```cpp
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        priority_queue<int, vector<int>, greater<int>> pq;
        for(auto &i : intervals){
            if(!pq.empty() and pq.top() <= i[0])
                pq.pop();
            pq.push(i[1]);
        }
        return pq.size();
    }
};
```
<hr>

## Approach / Intuition - 2
- Store the start and end time of each meetings with +1 and -1 respectively as +1 represents requirement of room and -1 represents freeing of room.
- Sort the by time.
- Find maximum meeting going on simultaneously as this would tell us the minimum rooms required.

## Algorithm - 2
1. Store the start and end time of each meeting in the `meets` vector of pair with +1 for start time and -1 end time as its value.
2. Sort the meets array in non - descending order wrt to the time.
3. Find the maximum meeting running simultaneously and return it.

## Complexity
##### Time Complexity
- \(O(N \log N)\)
##### Space Complexity
- \(O(N)\)

## Code
```cpp
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        vector<pair<int, int>> meets;
        for(auto i : intervals){
            meets.push_back({i[0],1});
            meets.push_back({i[1],-1});
        }
        sort(meets.begin(), meets.end());
        int minRooms = 0;
        int curRooms = 0;
        for(auto i : meets){
            curRooms += i.second;
            minRooms = max(minRooms, curRooms);
        }
        return minRooms;
    }
};
```