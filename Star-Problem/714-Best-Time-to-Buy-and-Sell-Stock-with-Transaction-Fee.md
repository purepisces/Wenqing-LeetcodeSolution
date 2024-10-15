https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

Sliding window approach:

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        res = 0
        l = 0
        r = 1
        while r <= len(prices) -1:
            if prices[r] > prices[l]:
                res = max(res, prices[r] - prices[l])
            else:
                l = r
            r+=1
        return res
        
```
Dynamic Programming approach:
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        buy, sell = -sys.maxsize, 0
        for price in prices:
            # Update the "buy" to be the maximum of either the current buy or the negative of the current price
            buy = max(buy, -price)
            # Update the "sell" to be the maximum of either the current sell or the profit from this price
            sell = max(sell, buy + price)
        return sell
```

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/
```python
class Solution(object):
    def maxProfit(self, prices, fee):
        """
        :type prices: List[int]
        :type fee: int
        :rtype: int
        """
        n = len(prices)
        # dp array with two states: 0 -> not holding stock, 1 -> holding stock
        dp = [[0] * 2 for _ in range(n)]
        #print(dp)
        # [[0, 0], [0, 0], [0, 0]]

        
        # Base case
        dp[0][0] = 0  # No stock on day 0 means no profit
        dp[0][1] = -prices[0]  # Holding stock on day 0 means we bought it
        
        # Fill the dp table
        for i in range(1, n):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1] + prices[i] - fee)  # Sell stock today or do nothing
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] - prices[i])  # Buy stock today or do nothing
        
        # The result is the profit without holding any stock at the last day
        return dp[n-1][0]
```
