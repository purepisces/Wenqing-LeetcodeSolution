```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        if (root.left and root.left.val >= root.val) or (root.right and root.right.val <= root.val):
            return False
        return self.isValidBST(root.left) and self.isValidBST(root.right)

        def dfs(left, root, right):
            if not root:
                return True
            if left >= root.val or right <= root.val:
                return False
            return dfs(left, root.left, root.val) and dfs(root.val, root.right, right)
        return dfs(float("-inf"), root,float("inf"))
```
