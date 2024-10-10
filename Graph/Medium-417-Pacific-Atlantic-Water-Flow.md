https://leetcode.com/problems/pacific-atlantic-water-flow/description/










___
wrong implementation
```python
# wrong thought
class Solution(object):
    def pacificAtlantic(self, heights):
        """
        :type heights: List[List[int]]
        :rtype: List[List[int]]
        """
        rows = len(heights[0])
        columns = (heights[0][0])
        visit = set()
        pac = set()
        atl = set()
        def dfs(r,c,curmax):
            if r > rows or c > columns or (r,c) in visit or heights[r][c] > max:
                return False
            visit.add((r,c))
            curmax = max(curmax, heights[r][c])
            temp = [(0,1),(0,-1),(-1,0),(1,0)]
            for dr, dl in temp:
                if dfs(dr+r, dc+c, curmax):
                    return True
            return False
        for i in range(len(cols)):
            if dfs(0,i):
                pac.add((0,i))
```
