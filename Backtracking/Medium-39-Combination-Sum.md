```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        res = []
        subset = []
        def dfs(i,val):
            if val == target :
                res.append(subset[:])
                return
            if i >= len(candidates) or val > target:
                return 
            subset.append(candidates[i])
            val+=candidates[i]
            dfs(i,val)
            subset.pop()
            val-=candidates[i]
            dfs(i+1,val)

        dfs(0,0)
        return res
```
