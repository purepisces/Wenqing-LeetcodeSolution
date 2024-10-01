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
