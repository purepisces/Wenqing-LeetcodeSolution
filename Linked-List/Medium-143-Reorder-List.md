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
wrong version
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reorderList(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: None Do not return anything, modify head in-place instead.
        """
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            print(slow)
            fast = fast.next.next
        #[1,2,3,4,5] 3
        #[1,2,3,4,5,6] 4
        #[1,2,3] [5,4]
        #[1,2,3] [6,5,4]
        tmp = slow.next
        slow.next = None
        def reverse_list(head):
            prev = None
            cur = head
            while cur:
                tmp = cur.next
                cur.next = prev
                prev = cur
                cur = tmp
        return slow
        list1 = head
        list2 = reverse_list(tmp)
        dummy = ListNode()
        cur = dummy
        while list1 and list2:
            dummy.next = list1
```
