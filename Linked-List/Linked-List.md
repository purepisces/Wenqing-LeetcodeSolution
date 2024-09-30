143. Reorder List: https://leetcode.com/problems/reorder-list/description/
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        # find middle
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # reverse second half
        second = slow.next
        prev = slow.next = None
        while second:
            tmp = second.next
            second.next = prev
            prev = second
            second = tmp
       
        # merge two halfs
        first, second = head, prev
        while second:
            tmp1, tmp2 = first.next, second.next
            first.next = second
            second.next = tmp1
            first, second = tmp1, tmp2
```
___
## Finding middle element
```python
slow, fast = head, head.next
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
```
For example, [1,2,3,4,5] the slow will stop at 3, fast will stop at None(after 5)

[1,2,3,4,5,6], the slow will stop at 3, fast will stop at 6.
