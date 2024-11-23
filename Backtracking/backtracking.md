We use `res.append(subset[:])` instead of `res.append(subset)` because appending `subset` directly to `res` only stores a reference to the same list object, not a snapshot of its current state. Using `subset[:]` ensures that a copy of the list is appended, preserving its contents at that specific moment.
```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        nums.sort()
        subset = []
        def dfs(i):
            if i == len(nums):
                res.append(subset[::])
                return
            subset.append(nums[i])
            dfs(i + 1)
            subset.pop()
            while i + 1 < len(nums) and nums[i] == nums[i + 1]:
                i += 1
            dfs(i + 1)
        dfs(0)
        return res
```
