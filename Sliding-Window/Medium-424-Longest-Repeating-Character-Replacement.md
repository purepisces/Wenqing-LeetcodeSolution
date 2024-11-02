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


Example: 
Input: s = "AABABBA", k = 1

```python
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        l = 0
        maxf = 0
        count = {}
        for r in range(len(s)):
            print('r is', r)
            count[s[r]] = 1 + count.get(s[r], 0)
            maxf = max(maxf, count[s[r]])
            if (r-l+1) - maxf > k:
                count[s[l]] -= 1
                l+=1
                print("l is", l)
        return r-l+1
```
print result
```css
('r is', 0)
('r is', 1)
('r is', 2)
('r is', 3)
('r is', 4)
('l is', 1)
('r is', 5)
('l is', 2)
('r is', 6)
('l is', 3)
```
Note that in the final loop, when it goes to l =2, r = 6, with window size = 5, which is "BABBA", but finally it will move left point to the right, and which makes sure the final window size is the valid window.
