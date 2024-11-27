# [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)




## Problem Statement
- You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.
- Find the maximum profit you can achieve. You may complete at most two transactions.
- **Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).



## Constraints
- 1 <= prices.length <= 10<sup>5</sup>
- 0 <= prices[i] <= 10<sup>5</sup>



## Test Cases
1. **Input:** prices = [3,3,5,0,0,3,1,4] <br>
**Output:** 6
2. **Input:** prices = [1,2,3,4,5]  <br>
**Output:** 4
3. **Input:** prices = [7,6,4,3,1]<br>
**Output:** 0



## Approach / Intuition 
- Using **Dynamic programming approach**.
- Check for minimum cost to buy first stock.
- Find maximum profit after selling the stock.
- Same for second stock.
- `t2Profit` stores the total profit as `t1profit` is used to buy the second stock.




## Algorithm 
1. Traverse over `prices`.
2. Follow the above steps in the loop.
3. Return the `t2Profit` as sum for the 2 transactions.




## Complexity
##### Time Complexity
- \(O(N)\)
##### Space Complexity
- \(O(1)\)



## Code
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int t1Cost = INT_MAX, t2Cost = INT_MAX;
        int t1Profit = 0, t2Profit = 0;
        for (int price : prices) {
            t1Cost = min(t1Cost, price);
            t1Profit = max(t1Profit, price - t1Cost);
            t2Cost = min(t2Cost, price - t1Profit);
            t2Profit = max(t2Profit, price - t2Cost);
        }
        return t2Profit;
    }
};   
```