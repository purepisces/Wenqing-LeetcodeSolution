```python
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        count = {}
        l = 0
        maxf = 0
        for r in range(len(s)):
            count[s[r]] = 1 + count.get(s[r], 0)
            maxf = max(maxf, count[s[r]])
            if (r - l + 1) - maxf > k:
                count[s[l]] -= 1
                l += 1
        return (r - l + 1)
```
The difficult point is the sliding window we final return r-l+1
-   **Valid Window Check**: A window is valid if `(r - l + 1) - maxf <= k`.
-   **Why return `(r - l + 1)`?**: By the time we exit the loop, the longest valid window size will have been found, whether it was in the middle or the end.
