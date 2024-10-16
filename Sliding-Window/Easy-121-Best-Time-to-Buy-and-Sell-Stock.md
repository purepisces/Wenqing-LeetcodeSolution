Sliding window approach:


Consider the example `[2, 15, 1, 21, 5, 6, 9]`. The sliding window moves from `[2, 15]` to `[1, 21]`, not considering `[2, 21]` because `1` is the minimum value before `21`. The left pointer always points to the minimum value before the right pointer, allowing us to determine the maximum profit in this window. For `21`, since the minimum value before it is the element `1` at index 2, we update `l` accordingly. If `1` is less than `2`, then for any value greater than `1`, the maximum profit will be `prices[i] - 1`, not `prices[i] - 2`.

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
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        res = 0
        lowest = prices[0]
        for price in prices:
            if price < lowest:
                lowest = price
            res = max(res, price - lowest)
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
