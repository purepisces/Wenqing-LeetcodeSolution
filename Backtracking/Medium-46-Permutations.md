
```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        # base case
        if len(nums) == 1:
            return [nums[:]]  # nums[:] is a deep copy

        for i in range(len(nums)):
            n = nums.pop(0)
            perms = self.permute(nums)

            for perm in perms:
                perm.append(n)
            res.extend(perms)
            nums.append(n)
        return res
```

```python
list1 = []
list2 = [[4, 5, 6],[7],[8]]
list1.extend(list2)
print(list1)
# list 1: [[4, 5, 6], [7], [8]]
```
My another correct version:
```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 1:
            return [nums[:]]
        res = []
        for i in range(len(nums)):
            temp = nums.pop()
            permutations = self.permute(nums)
            for per in permutations:
                per.append(temp)
                res.append(per)
            nums.insert(0, temp)
        return res
```
___
wrong version:    
`if len(nums) == 1: return [nums] `, should make a deep copy of nums, which should be `return [nums[:]]`, otherwise it will become a reference which cause problem.

