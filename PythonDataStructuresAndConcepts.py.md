
```python
countT = {}
for c in t:
    countT[c] = 1 + countT.get(c, 0)
```
same to 
```python
countT = {}
for c in t:
    if c not in countT:
        countT[c] = 1
    else:
        countT[c] += 1
```
-----------------------
The expression ",".join(res) is used in Python to concatenate a list of strings into a single string, with each element separated by a comma.
```python
res = ["apple", "banana", "cherry"]
result = ",".join(res)
print(result)
```
output
```
apple,banana,cherry
```

The expression vals = data.split(",") is used in Python to split a string into a list of substrings based on a specified delimiter, in this case, a comma.
```python
data = "apple,banana,cherry"
vals = data.split(",")
print(vals)
```
output
```
['apple', 'banana', 'cherry']
```




-----------------------
```
q = deque()
```

stands for "double-ended queue." It is a part of the collections module in Python and provides an efficient way to work with a sequence of elements that can be added or removed from both ends.

Efficient O(1) Operations: Appending and popping from both ends of a deque are O(1) operations. This is more efficient than using a list where these operations are O(n) at the front.
Flexible Data Structure: You can use it as a queue (FIFO - First In, First Out) or as a stack (LIFO - Last In, First Out).

Append Elements:

q.append(x): Adds x to the right end of the deque.
q.appendleft(x): Adds x to the left end of the deque.

Pop Elements:

q.pop(): Removes and returns the element from the right end.
q.popleft(): Removes and returns the element from the left end.

both q.append(x), q.appendleft(x), q.pop(), and q.popleft() operations on a deque are O(1) operations.


-----------------------

In number of islands, when we make visit = set()
and  visit.add((r,c))
we should not visit.add([r,c]) since type 'list' is unhashable

-----------------------

Mutable Objects: Lists in Python are mutable. When you modify a list (e.g., by appending or popping elements), these modifications affect the original list. This behavior is different from modifying immutable objects (like integers), where you would need to declare the variable as nonlocal to modify it in an inner function.

correct:
```
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
incorrect: UnboundLocalError: local variable 'res' referenced before assignment

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = 0
        def dfs(root):
            if not root:
                return -1
            left = dfs(root.left)
            right = dfs(root.right)
            res = max(res, 2+left+right)
            return 1 + max(left, right)
        dfs(root)
        return res
```

-----------------------
