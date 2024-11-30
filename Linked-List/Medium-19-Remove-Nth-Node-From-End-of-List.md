Finally, **`return dummy.next`.**

The dummy node is used in this problem to simplify edge cases, particularly when we need to remove the head of the list. Consider the example [1,2,3] and n = 3, which we need to move head, which is node1.

First, move the `right` pointer `n` steps forward. Then, move `right` another `length - n` steps. Starting `left` from the `dummy` node allows us to position it right before the node we want to remove after moving `length - n` steps. For example, if the length of the list is 8 and `n = 2`, we first move `right` 2 steps. Then, we move `right` an additional `8 - 2 = 6` steps until it reaches the end (`None`). Starting from the `dummy` node, moving `left` 6 steps will place it just before the node we want to remove, which is the 3rd-to-last node.

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

___
not good answer, but accepted

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: Optional[ListNode]
        :type n: int
        :rtype: Optional[ListNode]
        """
        # find the last n
        # means move l - n - 1 time to find
        tmp = head
        while tmp:
            if n == 0:
                break
            tmp = tmp.next
            n-=1
        dummy = ListNode()
        dummy.next = head
        cur = dummy
        while tmp:
            cur = cur.next
            tmp = tmp.next
        cur.next = cur.next.next
        return dummy.next
```
My wrong implementation, just need to modify the return statement, not return `head` but should `return dummy.next`.

It not work when head = [1] and n = 1, the expected output is [], however, the output it returned is [1].
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: Optional[ListNode]
        :type n: int
        :rtype: Optional[ListNode]
        """
        temp = head
        while n > 0:
            temp = temp.next
            n -=1
        print(temp)
        dummy = ListNode()
        cur = dummy
        cur.next = head
        while temp:
            cur = cur.next
            temp = temp.next
        print(cur)
        temp = cur.next.next
        cur.next = temp
        return head
```
