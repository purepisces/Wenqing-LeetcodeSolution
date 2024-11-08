**Need to set `groupnext = kth.next`**, if just using ` while cur != kth.next` will cause error `AttributeError: 'NoneType' object has no attribute 'next'
    tmp = cur.next` but don't know why, since groupnext == kth.next.
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        dummy = ListNode(0,head)
        groupprev = dummy
        while True:
            kth = self.findknode(groupprev,k)
            if not kth:
                break
            groupnext = kth.next
            prev = groupnext
            cur = groupprev.next
            while cur != groupnext:
                tmp = cur.next
                cur.next= prev
                prev = cur
                cur = tmp
            tmp = groupprev.next
            groupprev.next = kth
            groupprev = tmp
        return dummy.next
            
    def findknode(self,cur,k):
        while cur and k > 0:
            cur = cur.next
            k-=1
        return cur
```
___
My completely wrong version
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: Optional[ListNode]
        :type k: int
        :rtype: Optional[ListNode]
        """
        dummy = ListNode()
        dummy.next = head
        groupprev = dummy
        while True:
            kth = self.findkth(groupprev, k) # 3
            if kth:
                prev = kth.next # 4
                cur = head
                # 1 2 3
                # 3 2 1
                while cur != kth: # cur = 1
                    tmp = cur.next #2
                    cur.next = prev
                    prev = cur
                    cur = tmp
            tmp = groupprev.next
            groupprev.next = cur
            groupprev = tmp
        return dummy.next

    def findkth(self, node, k):
        while node and k > 0:
            node = node.next
            k-=1
        return node
```
