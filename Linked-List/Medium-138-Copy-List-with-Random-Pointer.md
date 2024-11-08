```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x, next=None, random=None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        oldToCopy = {None:None}
        cur = head
        while cur:
            node = Node(cur.val)
            oldToCopy[cur] = node
            cur = cur.next
        cur = head
        while cur:
            copy =  oldToCopy[cur] 
            copy.next = oldToCopy[cur.next] 
            copy.random = oldToCopy[cur.random] 
            cur = cur.next
        return oldToCopy[head]
```
