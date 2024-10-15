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
