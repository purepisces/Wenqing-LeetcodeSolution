```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        one = 1
        two = 1
        for i in range(n-1):
            temp = two
            two = one + two
            one = temp
        return two   
```
fibonacci sequence, 1 1 2 3 5 8 etc, dp[i] = dp[i-1] + dp[i-2].
So can also write like this
```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 1:
            return 1
        dp = [0] * (n + 1) 
        dp[0] = 1  
        dp[1] = 1  
        for i in range(2, n + 1):  
            dp[i] = dp[i - 1] + dp[i - 2]  
        
        return dp[n]
```
