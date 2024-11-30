We will Sort cars based on their starting position in descending order (cars closer to the target come first), then stack is used to store the time, where time is calculated by `float(target - p)/s`, it calculate the time taken for the current car to reach the target. If the current car's time is less than or equal to the previous fleet's time, it means the current car merges into the previous fleet, remove the current car's time since it joins the previous fleet.

Finally, the size of the stack represents the number of fleets.

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
