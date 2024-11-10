```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        map = {")":"(", "}":"{","]":"["}
        stack = []
        for bracket in s:
            if bracket not in map:
                stack.append(bracket)
                continue
            if not stack or stack[-1]!= map[bracket]:
                return False
            stack.pop()
        return not stack
```
___
my version, also good
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        map = {")":"(", "}":"{", "]":"["}
        for c in s:
            if c not in map:
                stack.append(c)
                continue
            if not stack or map[c] != stack.pop():
                return False
        return True if not stack else False
```
