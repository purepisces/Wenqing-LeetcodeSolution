I love this question, it is really typical and kind of brainstrom, really good!
```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        stack = []
        result = []
        def backtrack(openN, closeN):
            if openN == closeN == n:
                result.append("".join(stack))
            if openN < n:
                stack.append("(")
                backtrack(openN+1, closeN)
                stack.pop()
            if closeN < openN:
                stack.append(")")
                backtrack(openN, closeN+1)
                stack.pop()
        backtrack(0,0)
        return result
```
