```python
class Solution(object):
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        res, part = [], []
        def dfs(i):
            if i >= len(s):
                res.append(part[:])
                return
            for j in range(i, len(s)):
                if self.isPali(s, i, j):
                    part.append(s[i : j + 1])
                    dfs(j + 1)
                    part.pop()
        dfs(0)
        return res

    def isPali(self, s, l, r):
        while l < r:
            if s[l] != s[r]:
                return False
            l, r = l + 1, r - 1
        return True
```
___
My wrong stuck version
```python
class Solution(object):
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        res = []
        subset = []
        def dfs(i):
            if i == len(s):
                res.append(subset[:])
            if isPalindrome(s[i]):
                subset.append(s[i])
        def isPalindrome(s):
            l = 0
            r = len(s) - 1
            while l <= r:
                if s[l] != s[r]:
                    return False
                l+=1
                r-=1
            return True
```
