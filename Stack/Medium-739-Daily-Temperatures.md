For this problem, remember the use of `for i, t in enumerate(temperatures)`.

We store both the temperature and corresponding index to the stack, since we will use the index to make calculation to the result array. Only when temperature is higher than the previous, the stack will pop, otherwise the stack will append new element(e.g. [(0,76), (1,73), (2, 72)] ... 

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
___
My wrong implementation: I should update the result array when I pop from the stack.
```python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        # 75 73 71 76
        res = [0] * len(temperatures)
        stack = []
        for i, temperature in enumerate(temperatures):
            while stack and temperatures[i] > stack[-1][1]:
                index, temp = stack.pop()
            stack.append((i,temperature))
            res[i] = index - i
        return res
```
