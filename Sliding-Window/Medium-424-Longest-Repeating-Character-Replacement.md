**Sliding window size**

Input: s = "AABABBA", k = 1

Output: 4

Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

From "A” to "AA" to "AAB" to "AABA" to "AABAB" to "ABABB" to "BABBA" to "ABBA"(due to  if (r-l+1) - maxf > k, l+=1)

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

Note that at the start of the final loop, when l = 2 and r = 6, the window size is 5, which corresponds to the substring 'BABBA'. However, the left pointer will goes to " if (r-l+1) - maxf > k:" and eventually move to the right, ensuring that the final window size remains valid.
