```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if not lists or len(lists) == 0:
            return None
        while len(lists) > 1:
            mergedlist = []
            for i in range(0, len(lists), 2):
                list1 = lists[i]
                list2 = lists[i+1] if i+1 < len(lists) else None
                mergedlist.append(self.mergelist(list1,list2))
            lists = mergedlist
        return lists[0]
    def mergelist(self, list1, list2):
        dummy = ListNode()
        cur = dummy
        while list1 and list2:
            val1 = list1.val
            val2 = list2.val
            if val1 < val2:
                cur.next = list1
                list1 = list1.next
            else:
                cur.next = list2
                list2 = list2.next
            cur = cur.next
        if list1:
            cur.next = list1
        if list2:
            cur.next = list2
        return dummy.next
```
