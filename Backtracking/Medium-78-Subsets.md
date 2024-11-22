We need to use `res.append(subset[:])`, not `res.append(subset)` since when subset is appended to res, the reference to the subset list is stored, not its current value or a copy of it.

```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        subset = []
        def dfs(i):
            if i == len(nums):
                res.append(subset[:])
                return
            subset.append(nums[i])
            dfs(i+1)
            subset.pop()
            dfs(i+1)
        dfs(0)
        return res
```
```python3
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        subset = []
        def dfs(i):
            print("i is ", i)
            if i == len(nums):
                res.append(subset[:])
                print("res is", res)
                return 
            subset.append(nums[i])
            print("subset append is", subset)
            dfs(i+1) 
            print("subset pop element is", subset[-1])
            print("nums[i] is ", nums[i])
            subset.pop()
            print("subset pop is", subset)
            dfs(i+1) 
        dfs(0)
        return res
```
```python
('i is ', 0)
('subset append is', [0])
('i is ', 1)
('subset append is', [0, 1])
('i is ', 2)
('subset append is', [0, 1, 2])
('i is ', 3)
('res is', [[0, 1, 2]])
('subset pop element is', 2)
('nums[i] is ', 2)
('subset pop is', [0, 1])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1]])
('subset pop element is', 1)
('nums[i] is ', 1)
('subset pop is', [0])
('i is ', 2)
('subset append is', [0, 2])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2]])
('subset pop element is', 2)
('nums[i] is ', 2)
('subset pop is', [0])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2], [0]])
('subset pop element is', 0)
('nums[i] is ', 0)
('subset pop is', [])
('i is ', 1)
('subset append is', [1])
('i is ', 2)
('subset append is', [1, 2])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2], [0], [1, 2]])
('subset pop element is', 2)
('nums[i] is ', 2)
('subset pop is', [1])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2], [0], [1, 2], [1]])
('subset pop element is', 1)
('nums[i] is ', 1)
('subset pop is', [])
('i is ', 2)
('subset append is', [2])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2], [0], [1, 2], [1], [2]])
('subset pop element is', 2)
('nums[i] is ', 2)
('subset pop is', [])
('i is ', 3)
('res is', [[0, 1, 2], [0, 1], [0, 2], [0], [1, 2], [1], [2], []])
```
