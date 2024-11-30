Don't need to return boolean value in dfs function, could just use `if grid[r][c] == "1" and (r, c) not in visit`.

```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid or not grid[0]:
            return 0

        islands = 0
        visit = set()
        rows, cols = len(grid), len(grid[0])

        def dfs(r, c):
            if (
                r not in range(rows)
                or c not in range(cols)
                or grid[r][c] == "0"
                or (r, c) in visit
            ):
                return

            visit.add((r, c))
            directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
            for dr, dc in directions:
                dfs(r + dr, c + dc)

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == "1" and (r, c) not in visit:
                    islands += 1
                    dfs(r, c)
        return islands


    # BFS Version From Video
    def numIslands(self, grid):
        if not grid:
            return 0

        rows, cols = len(grid), len(grid[0])
        visited=set()
        islands=0

        def bfs(r,c):
            q = deque()
            visited.add((r,c))
            q.append((r,c))
        
            while q:
                row,col = q.popleft()
                directions= [[1,0],[-1,0],[0,1],[0,-1]]
            
                for dr,dc in directions:
                    r,c = row + dr, col + dc
                    if (r) in range(rows) and (c) in range(cols) and grid[r][c] == '1' and (r ,c) not in visited:
                    
                        q.append((r , c ))
                        visited.add((r, c ))

        for r in range(rows):
            for c in range(cols):
            
                if grid[r][c] == "1" and (r,c) not in visited:
                    bfs(r,c)
                    islands +=1 

        return islands
```
___
My bad implementation, but accepted:

I don't need to return True or False, instead, I can just add a check that `if grid[r][c] == "1" and (r, c) not in visit:`
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        res = 0
        row = len(grid)
        col = len(grid[0])
        visit = set()
        def dfs(r,c):
            if r not in range(row) or c not in range(col) or (r,c) in visit or grid[r][c] == "0":
                return False
            visit.add((r,c))
            directions = [[0,-1],[0,1],[-1,0],[1,0]]
            for dr, dc in directions:
                dfs(r+dr, c+dc)
            return True
        for r in range(row):
            for c in range(col):
                if dfs(r,c):
                    res+=1
        return res
```

