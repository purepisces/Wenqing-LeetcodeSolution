For this problem, remember the use of `for i, t in enumerate(temperatures)`.

And for temperature `[76,73,77]`, the stack before element 77 will be `[(0, 76), (1, 73)]`

When temperature is 77, then it will goes into while loop and pop twice. The final stack will be `[(2, 77)]`

```python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        result = [0] * len(temperatures)
        stack = []
        for i, t in enumerate(temperatures):
            while stack and t > stack[-1][1]:
                index = stack.pop()[0]
                result[index] = i - index
            stack.append((i,t))
        return result
```
