```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        rob1, rob2 = 0, 0
        # [rob1, rob2, n, n+1, ...]
        for n in nums:
            temp = max(rob1 + n, rob2)
            rob1 = rob2
            rob2 = temp
        return rob2
```

My solution inspired by 746. Min Cost Climbing Stairs:
```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.append(0)
        for i in range(len(nums)-3,-1,-1):
            nums[i] = max(nums[i]+ nums[i+2], nums[i+1])
        return max(nums[0], nums[1])
```
