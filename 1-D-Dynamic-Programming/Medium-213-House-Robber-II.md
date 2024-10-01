```python
class Solution(object):
    def rob(self, nums):
        if len(nums) == 1:
            return nums[0]
        rob_move_last = nums[:len(nums)-1]
        rob_move_first = nums[1:]
        return max(self.helper(rob_move_last), self.helper(rob_move_first))

    def helper(self, nums):
        rob1, rob2 = 0, 0
        for n in nums:
            newRob = max(rob1 + n, rob2)
            rob1 = rob2
            rob2 = newRob
        return rob2
```
