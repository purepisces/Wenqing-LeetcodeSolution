I love this question, it is really typical and kind of brainstrom, really good!

It also has the backtracking algorithm.
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
            print("(openN, closeN)", (openN, closeN))
            print(stack)
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
```css
# for n = 3
('(openN, closeN)', (0, 0))
[]
('(openN, closeN)', (1, 0))
['(']
('(openN, closeN)', (2, 0))
['(', '(']
('(openN, closeN)', (3, 0))
['(', '(', '(']
('(openN, closeN)', (3, 1))
['(', '(', '(', ')']
('(openN, closeN)', (3, 2))
['(', '(', '(', ')', ')']
('(openN, closeN)', (3, 3))
['(', '(', '(', ')', ')', ')']
('(openN, closeN)', (2, 1))
['(', '(', ')']
('(openN, closeN)', (3, 1))
['(', '(', ')', '(']
('(openN, closeN)', (3, 2))
['(', '(', ')', '(', ')']
('(openN, closeN)', (3, 3))
['(', '(', ')', '(', ')', ')']
('(openN, closeN)', (2, 2))
['(', '(', ')', ')']
('(openN, closeN)', (3, 2))
['(', '(', ')', ')', '(']
('(openN, closeN)', (3, 3))
['(', '(', ')', ')', '(', ')']
('(openN, closeN)', (1, 1))
['(', ')']
('(openN, closeN)', (2, 1))
['(', ')', '(']
('(openN, closeN)', (3, 1))
['(', ')', '(', '(']
('(openN, closeN)', (3, 2))
['(', ')', '(', '(', ')']
('(openN, closeN)', (3, 3))
['(', ')', '(', '(', ')', ')']
('(openN, closeN)', (2, 2))
['(', ')', '(', ')']
('(openN, closeN)', (3, 2))
['(', ')', '(', ')', '(']
('(openN, closeN)', (3, 3))
['(', ')', '(', ')', '(', ')']
```
