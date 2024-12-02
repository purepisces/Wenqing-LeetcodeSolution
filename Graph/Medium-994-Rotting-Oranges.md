quite similar as the question 286 walls and gates

```python
class Solution(object):
    def orangesRotting(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        row = len(grid)
        col = len(grid[0])
        time = 0
        fresh = 0
        q = deque()
        for r in range(row):
            for c in range(col):
                if grid[r][c] == 2:
                    q.append((r,c))
                if grid[r][c] == 1:
                    fresh+=1

        while fresh > 0 and q:
            time+=1
            for i in range(len(q)):
                r,c = q.popleft()
                directions = [[0,1],[0,-1],[1,0],[-1,0]]
                for dr, dc in directions:
                    new_r = r + dr
                    new_c = c + dc
                    if new_r not in range(row) or new_c not in range(col) or grid[new_r][new_c] != 1:
                        continue
                    grid[new_r][new_c] = 2
                    fresh -= 1
                    q.append((new_r,new_c))
        return time if fresh == 0 else -1
```
