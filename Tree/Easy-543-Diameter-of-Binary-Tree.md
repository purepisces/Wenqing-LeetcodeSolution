```python
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
        self.res = 0
        def dfs(root):
            if not root:
                return -1
            left = dfs(root.left)
            right = dfs(root.right)
            self.res = max(self.res, 2+left+right)
            return 1 + max(left, right)
        dfs(root)
        return self.res
```
___

My wrong solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        if not root:
            return 0
        res = 0
        res = max(res, 2 + self.depth(root.left)+ self.depth(root.right))
        return res
    def depth(self, root):
        if not root:
            return -1
        return 1 + max(self.depth(root.left), self.depth(root.right))
```
