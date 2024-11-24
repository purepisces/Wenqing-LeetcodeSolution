```python
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if not grid or not grid[0]:
            return 0
        area = 0
        row = len(grid)
        col = len(grid[0])
        visit = set()
        def dfs(r,c):
            if (r,c) in visit or r not in range(row) or c not in range(col) or grid[r][c] == 0:
                return 0
            visit.add((r,c))
            directions = [[0,-1],[0,1],[-1,0],[1,0]]
            area = 1
            for dr, dc in directions:
                area += dfs(r+dr, c+dc)
            return area
        for r in range(row):
            for c in range(col):
                if grid[r][c] == 1 and (r,c) not in visit:
                    area = max(area,dfs(r,c))
        return area
```
___
My bad but accepted solution:

I don't need to also pass area in dfs function, since I can just make a local variable area = 1, and then add it to be += dfs(r+dr, c+dc) in the for loop. Since in each direction, it should add it's neighbor's area.
```python
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        res = 0
        row = len(grid)
        col = len(grid[0])
        visit = set()
        def dfs(r,c,area):
            if r not in range(row) or c not in range(col) or (r,c) in visit or grid[r][c] == 0:
                return
            directions = [[0,1], [0,-1],[1,0],[-1,0]]
            visit.add((r,c))
            for dr, dc in directions:
                area = max(dfs(r+dr,c+dc, area+1), area)        
            return area
        for r in range(row):
            for c in range(col):
                if grid[r][c] == 1 and (r,c) not in visit:
                    area = dfs(r,c,1)
                    res = max(res,area)
        return res
```
