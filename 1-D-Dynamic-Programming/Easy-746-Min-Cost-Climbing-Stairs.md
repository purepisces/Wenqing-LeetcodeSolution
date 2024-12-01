**Logic for `cost[i]`:**

-   `cost[i] + cost[i + 1]`: Cost of stepping 1 step from `i`.
-   `cost[i] + cost[i + 2]`: Cost of stepping 2 steps from `i`.
-   Update `cost[i]` with the minimum of these two.
  
```python
class Solution(object):
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        cost.append(0)
        for i in range(len(cost)-3,-1,-1):
            cost[i] = min(cost[i]+cost[i+1], cost[i]+cost[i+2])
        return min(cost[0],cost[1])
```
___
My wrong implementation, the logic for cost[i] is wrong, we should choose the value in cost[i] and from there we will have two paths to choose. Also the final return statement should be `min(cost[0],cost[1])`. Since we don't know which index should we start.
```python
class Solution(object):
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        cost.append(0)
        for i in range(len(cost)-3, -1, -1):
            cost[i] = min(cost[i] + cost[i+2], cost[i+1])
        return cost[0]
```
