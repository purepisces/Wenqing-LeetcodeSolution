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
