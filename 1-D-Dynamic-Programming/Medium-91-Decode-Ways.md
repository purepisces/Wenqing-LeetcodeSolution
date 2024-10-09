https://leetcode.com/problems/decode-ways/

I think it is just divided in to subproblems, for example 11106

For index = 0, it will have 2 possibilities either be 1 + (1106)'s way or 11 + (106)'s way

but if it is 0, then 0 cannot be the start, so dp[i] = 0

and for any other value, we will definitely make dp[i] = dp[i + 1]
 and for dp[i+2] it will depends if it in the range from 10 to 26.


```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        dp = {len(s): 1}
        for i in range(len(s) - 1, -1, -1):
            if s[i] == "0":
                dp[i] = 0
            else:
                dp[i] = dp[i + 1]

            if i + 1 < len(s) and (
                s[i] == "1" or s[i] == "2" and s[i + 1] in "0123456"
            ):
                dp[i] += dp[i + 2]
        return dp[0]
```
