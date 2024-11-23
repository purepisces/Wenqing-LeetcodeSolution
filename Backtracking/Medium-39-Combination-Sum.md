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
Time Complexity: $O(2^{\frac{\text{target}}{\text{min(candidates)}}})$

Space Complexity: $O(\text{target} / \text{min(candidates)})$ for the recursion stack.

___
My wrong implementation

Forget to write return after `res.append(subset[:])`.
```python
#Wrong implementation
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
            if val == target:
                res.append(subset[:])
            if i == len(candidates) or val > target:
                return
            val += candidates[i]
            subset.append(candidates[i])
            dfs(i, val)
            val -= candidates[i]
            subset.pop()
            dfs(i+1, val)
        dfs(0,0)
        return res
```
