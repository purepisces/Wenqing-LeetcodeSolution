```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(0, head)
        left = dummy
        right = head
        while n > 0:
            right = right.next
            n -= 1
        while right:
            left = left.next
            right = right.next
        # delete
        left.next = left.next.next
        return dummy.next
```
### Example

```css
12345678910
n = 3
```

```python
 while n > 0:
            right = right.next
            n -= 1
```
right point first remove n times, which is 3 times, that starting from element1, move to 2, move to 3, move to 4.
```python
  while right:
            left = left.next
            right = right.next
```
then right and left point remove length -n times, which for right pointer, starting at 4, then move to 5, move to 6, move to 7, move to 8, move to 9, move to 10, move to None, which is moving length -n = 10-3 = 7times.

For left pointer, it moves from dummy, then move to 1, move to 2, move to 3, 4, 5, 6, 7, which also moves length - n times as right pointer, which is 10-3 = 7 times.

For the removing node, it will at position the nth node from the end of the list, since we move length-n times starting from dummy, then we are now at the n+1th node from the end of the list. If we move length-n times from head, then we are now at nth node from the end of the list.

Why we are at n+1th node from the end of the list, which is in front of the nth node from the end of the list, is that we need to delete the nth node from the end of the list, and it is making the node which in fromn of the delete node's next node be its next.next node.

The reason that we are using dummy is that that time when we are removing length-n times, we could be at the n+1th node from the end of the list so it will make us achieve the goal to delete the nth node from the end of the list.

