```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def dfs(root):
            if not root:
                return [True, 0]
            left = dfs(root.left)
            right = dfs(root.right)
            depth = 1 + max(left[1],right[1])
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            return [balanced, depth]
        return dfs(root)[0]
```
___
My accepted solution, I think is better than needcode solution, since I add an early stop.
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def dfs(root):
            if not root:
                return [True, 0]
            left = dfs(root.left)
            right = dfs(root.right)
            depth = 1 + max(left[1],right[1])
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            if not balanced:
                return [False, depth]
            return [balanced, depth]
        return dfs(root)[0]
```
