🌟🌟🌟🌟🌟 **Base Case for dfs**: I will use climbing stairs to illustrate it. At every given point, we have 2 decisions to make, either climb one or two. **When we reach 5**, it is our base case, we're gonna solve this recursively. When reach 5, **return 1**, this is when we find one way. And if this number of steps ever **exceeds five**, this is also the base case, we're going to **return 0**. https://leetcode.com/problems/climbing-stairs/description/

___

102. Binary Tree Level Order Traversal: https://leetcode.com/problems/binary-tree-level-order-traversal/description/

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res = []
        q = collections.deque()
        if root:
            q.append(root)

        while q:
            val = []
            for i in range(len(q)):
                node = q.popleft()
                val.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(val)
        return res
```
___
```python
# inefficient solution
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        def dfs(i):
            if i >= n:
                return i == n
            return dfs(i + 1) + dfs(i + 2)
        return dfs(0)
```
Time Complexity: O($2^n$) 
Space Complexity: O(n)

> 🌟🌟🌟🌟🌟🌟🌟🌟🌟🌟 Time Complexity: When analyzing recursion, **time complexity** accounts for the **total number of calls** made to the function. In this case, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**. 
> - At each call to `dfs(i)`, the function does work in the form of making **two recursive calls**: `dfs(i + 1)` and `dfs(i + 2)`.
> -   These recursive calls are **new computations** — they explore different paths in the recursion tree and **add to the total number of operations performed**.
> -   Therefore, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**, which grows exponentially as $O(2^n)$.
> 
> Space Complexity: Each recursive call pushes the current state of the function onto the stack. The maximum depth of the recursion stack is equal to the **depth of the recursion tree**, which is O(n) in this case.
___
