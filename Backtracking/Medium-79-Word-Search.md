Love this question!

For time limit issue:
```python
count = defaultdict(int, sum(map(Counter, board), Counter()))
    if count[word[0]] > count[word[-1]]:
        word = word[::-1]
```
```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        ROWS, COLS = len(board), len(board[0])
        path = set()

        def dfs(r, c, i):
            if i == len(word):
                return True
            if (
                min(r, c) < 0
                or r >= ROWS
                or c >= COLS
                or word[i] != board[r][c]
                or (r, c) in path
            ):
                return False
            path.add((r, c))
            res = (
                dfs(r + 1, c, i + 1)
                or dfs(r - 1, c, i + 1)
                or dfs(r, c + 1, i + 1)
                or dfs(r, c - 1, i + 1)
            )
            path.remove((r, c))
            return res

        count = defaultdict(int, sum(map(Counter, board), Counter()))
        if count[word[0]] > count[word[-1]]:
            word = word[::-1]
            
        for r in range(ROWS):
            for c in range(COLS):
                if dfs(r, c, 0):
                    return True
        return False
```
___
My wrong implementation, fails in [["A","B","C","E"],["S","F","E","S"],["A","D","E","E"]] "ABCESEEEFS". Since for ABCE, the letter E it has two E to select and it goes to a wrong way.
```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        row = len(board)
        col = len(board[0])
        def dfs(r,c,i, visit):
            if i == len(word):
                return True
            if r not in range(row) or c not in range(col) or (r,c) in visit:
                return 
            if board[r][c] != word[i]:
                return False
            visit.add((r,c))
            directions = [[1,0],[-1,0],[0,1],[0,-1]]
            for dr, dl in directions:
                if dfs(r + dr, c + dl, i+1, visit):
                    return True
        for r in range(len(board)):
            for c in range(len(board[0])):
                visit = set()
                if dfs(r,c,0,visit):
                    return True
        return False
```
