# Link:
- [36_Valid_Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

# Intuition

To determine if a 9x9 Sudoku board is valid, we need to validate only the filled cells according to the following rules:
- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.


According to the description, for ensuring no repetition, we can think of using a set. This is similar to solving the "contains duplicate" problem. If a value does not exist in the set, we add it; if it already exists in the set, we return `False`. For each row, column, and square, we should create a set and add values to it, checking for duplicates as we go.

For the 3x3 sub-boxes, we can use `square[(r//3, c//3)]` to store values from different sub-boxes. This reminds us of an important point: lists are not hashable, so we need to use a tuple `(r//3, c//3)` instead.

Also, note that if `board[r][c] == "."`, we should simply continue and not store it in the set, as it's not relevant to solving the problem.

For each cell, if its value already exists in its corresponding row, column, or sub-box, we return `False`. If not, we add the value to its respective row, column, and sub-box sets. After looping through all the cells, if no duplicates are found, we can return `True`.


### About using `defaultdict(set)`:

Using `collections.defaultdict(set)` creates a dictionary where missing keys are automatically initialized with an empty set when accessed. If we don't use `defaultdict`, we would need to manually initialize the sets for each key, it will be cubersome:

```python
    row = {}
    row[0] = set()
    print(row[0])
    output: set()
```

`defaultdict` simplifies this by automatically initializing values for keys that haven't been accessed, thus avoiding KeyError, and providing a convenient way to handle missing keys in dictionaries.


### About Hash Functions

When a key-value pair is added to a dictionary, the key's hash code is calculated using the hash function specific to the key's type. The hash code is an integer value representing a concise representation of the key.

The hash code is then used as an index or address within the underlying data structure (usually a hash table) to determine where the corresponding value should be stored.

When you retrieve a value from the dictionary using a key, Python calculates the hash code for the key again and uses it to locate the position within the data structure where the value is stored.

# Approach

We will create three dictionaries of sets to store the seen values. The line of code `row = collections.defaultdict(set)` creates a defaultdict with a default value of an empty set, which effectively acts as a hash set.

Then, we loop through each cell and check if the cell's value already exists in its row, column, or sub-box. If it does, we return `False`. If not, we add the cell's value to its corresponding row, column, and sub-box sets. After looping through and checking all cells, we return `True`.
# Complexity
- Time complexity:

  $$O(n^2)$$

  - The board size is fixed (9x9), so the work is constant.

- Space complexity:

  $$O(n^2)$$

  - We only store sets of seen numbers, which is constant for a fixed 9x9 board.

# Code
```python
class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        row = defaultdict(set)
        col = defaultdict(set)
        square = defaultdict(set)
        
        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue
                if(board[r][c] in row[r] or board[r][c] in col[c] or board[r][c] in square[(r//3,c//3)]):
                    return False
                row[r].add(board[r][c])
                col[c].add(board[r][c])
                square[(r//3,c//3)].add(board[r][c])
        return True
```
