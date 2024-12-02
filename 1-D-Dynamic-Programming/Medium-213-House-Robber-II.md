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
___
My also good solution:
```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 1:
            return nums[0]
        def amount(nums):
            rob1 = 0
            rob2 = 0
            for num in nums:
                temp = rob2
                rob2 = max(rob1+num, rob2)
                rob1 = temp
            return rob2
        return max(amount(nums[1:]), amount(nums[:-1]))
```
