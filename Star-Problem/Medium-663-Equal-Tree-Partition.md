```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def checkEqualTree(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        def calculate_sum(node):
            if not node:
                return 0
            current_sum = node.val + calculate_sum(node.left) + calculate_sum(node.right)
            subtree_sums.append(current_sum)
            return current_sum

        subtree_sums = []
        total_sum = calculate_sum(root)

        if total_sum % 2 != 0:
            return False
        
        half_sum = total_sum // 2
        subtree_sums.pop()  
        return half_sum in subtree_sums
```
