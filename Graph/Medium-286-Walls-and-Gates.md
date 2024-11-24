I love this question, it is using bfs, and it will store all the gates at first, then simultaneous updates from every door at the each step.
```python
class Solution(object):
    def wallsAndGates(self, rooms):
        """
        :type rooms: List[List[int]]
        :rtype: None Do not return anything, modify rooms in-place instead.
        """
        ROWS, COLS = len(rooms), len(rooms[0])
        q = deque()
        INF = 2147483647  

        for r in range(ROWS):
            for c in range(COLS):
                if rooms[r][c] == 0:
                    q.append((r, c))

        directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        while q:
            for i in range(len(q)):
                r, c = q.popleft()
                for dr, dc in directions:
                    row, col = r + dr, c + dc
                    if (not row in range(ROWS) or not col in range(COLS) 
                    or rooms[row][col] != INF ):
                        continue
                    else:
                        rooms[row][col] = rooms[r][c] + 1
                        q.append((row, col))
```
