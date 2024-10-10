https://leetcode.com/problems/pacific-atlantic-water-flow/description/


```python
class Solution(object):
    def pacificAtlantic(self, heights):
        """
        :type heights: List[List[int]]
        :rtype: List[List[int]]
        """
        rows, cols = len(heights), len(heights[0])
        pac, atl = set(), set()

        def dfs(r, c, visit, prevHeight):
            if (
                r not in range(rows)
                or c not in range(cols)
                or heights[r][c] < prevHeight
                or (r, c) in visit
            ):
                return

            visit.add((r, c))
            directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
            for dr, dc in directions:
                dfs(r + dr, c + dc, visit, heights[r][c])

        for c in range(cols):
            dfs(0, c, pac, heights[0][c])
            dfs(rows - 1, c, atl, heights[rows- 1][c])

        for r in range(rows):
            dfs(r, 0, pac, heights[r][0])
            dfs(r, cols - 1, atl, heights[r][cols - 1])

        res = []
        for r in range(rows):
            for c in range(cols):
                if (r, c) in pac and (r, c) in atl:
                    res.append([r, c])
        return res
```






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
