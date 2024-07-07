```python3
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        subset = []
        def dfs(i):
            print("i is ", i)
            if i == len(nums):
                res.append(subset[:])
                print("res is", res)
                return 
            subset.append(nums[i])
            print("subset append is", subset)
            dfs(i+1) 
            print("subset pop element is", subset[-1])
            print("nums[i] is ", nums[i])
            subset.pop()
            print("subset pop is", subset)
            dfs(i+1) 
        dfs(0)
        return res
```
