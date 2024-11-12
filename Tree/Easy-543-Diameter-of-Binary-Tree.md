在每个node点都需要算一下目前的self.res的值, 又因为每个node我们都会计算当前的高度,因此可以都放在这个depth funtion中计算.

when node is None, then height is -1, when one node, then height is 0. since we need to let when it is just 3 nodes, root, root.left root.right, we need it to be 2+left+right = 2+0+0 = 0, and for a single root, we need 2+left +right = 2-1-1 = 0.
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
        def depth(root):
            if not root:
                return -1
            left = depth(root.left)
            right = depth(root.right)
            self.res = max(self.res, 2+left+right)
            return 1 + max(left, right)
        depth(root)
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
my accepted solution
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
        self.res = 0
        self.depth(root)
        return self.res
    def depth(self, root):
        if not root:
            return -1
        left = self.depth(root.left)
        right = self.depth(root.right)
        self.res = max(self.res, 2 +left+ right)
        return 1 + max(left, right)
```
