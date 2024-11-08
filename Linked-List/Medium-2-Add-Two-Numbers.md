```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy = ListNode()
        cur = dummy
        carry = 0
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            val = val1+val2+ carry
            carry = val // 10
            val = val % 10
            cur.next = ListNode(val)
            cur = cur.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
        return dummy.next
```
___
not good implementation, but accepted
```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: Optional[ListNode]
        :type l2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        carry = 0
        dummy = ListNode()
        cur = dummy
        while l1 and l2:
            val = l1.val+l2.val+carry
            carry = val//10
            temp = val%10
            cur.next = ListNode(temp)
            l1 = l1.next
            l2 = l2.next
            cur = cur.next
        while l1:
            val = l1.val+carry
            carry = val//10
            temp = val % 10
            cur.next = ListNode(temp)
            l1 = l1.next
            cur = cur.next
        while l2:
            val = l2.val+carry
            carry = val//10
            temp = val % 10
            cur.next = ListNode(temp)
            l2 = l2.next
            cur = cur.next
        if carry > 0:
            cur.next = ListNode(carry)
        return dummy.next
```
