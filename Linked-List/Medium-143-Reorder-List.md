**Use `slow, fast = head, head.next`** not `slow, fast = head, head` for better division in first half and second half for even number.

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
wrong version: The issue is don't know how to finally merge these two halfs, the other part is correct.
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
        return prev
        list1 = head
        list2 = reverse_list(tmp)
        dummy = ListNode()
        cur = dummy
        while list1 and list2:
            dummy.next = list1
```

My correct and passed solution, but for even number it divided into first half: 123 and second half: 4, which is litter wierd although it is correct. For odd number, looks number, will divided into first half: 123 and second half: 45.

**Can just modify `slow, fast = head, head` to `slow, fast = head, head.next`.**

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
            fast = fast.next.next
        #123 #45
        print(slow)
        cur = slow.next #second half: 45
        slow.next = None # 123
        prev = None
        #reverse second half #12345
        while cur:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
        list1 = head
        list2 = prev
        while list2:
            temp1 = list1.next
            temp2 = list2.next
            list1.next = list2
            list2.next = temp1
            list1 = temp1
            list2 = temp2
        return list1
```
