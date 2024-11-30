```python
class Solution(object):
    def carFleet(self, target, position, speed):
        """
        :type target: int
        :type position: List[int]
        :type speed: List[int]
        :rtype: int
        """
        pair = [(p, s) for p, s in zip(position, speed)]
        pair.sort(reverse = True)
        stack = []
        for p, s in pair:
            stack.append(float(target - p)/s)
            if len(stack) >= 2 and stack[-1]<=stack[-2]:
                stack.pop()
        return len(stack)
```
