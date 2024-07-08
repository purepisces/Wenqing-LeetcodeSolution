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
