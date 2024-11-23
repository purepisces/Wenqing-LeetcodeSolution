```python
class Solution(object):
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        res = []
        subset = []
        val = 0
        def dfs(i, val):
            if val == target:
                res.append(subset[:])
                return
            if i >= len(candidates) or val > target:
                return
            subset.append(candidates[i])
            val += candidates[i]
            dfs(i+1, val)
            subset.pop()
            val -= candidates[i]
            while i < len(candidates) -1 and candidates[i] == candidates[i+1]:
                i = i+1
            dfs(i+1, val)
        dfs(0,0)
        return res
```
