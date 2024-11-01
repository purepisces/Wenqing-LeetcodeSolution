```python
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        output = []
        q = deque()  # index
        l = r = 0

        while r < len(nums):
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)

            if l > q[0]:
                q.popleft()

            if (r + 1) >= k:
                output.append(nums[q[0]])
                l += 1
            r += 1

        return output
```

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]

If the values are 2, 3, 5, then the queue will store only 5. If the values are 5, 3, 2, then the queue will store 5, 3, and 2, since we only need to know the maximum value at the current index. If the current index holds the maximum, we don’t need to store previous values. However, if it does not, previous values may still be helpful in the next sliding window, so we keep them.

And wen l > q[0], which means this element no longer in the sliding window, we will popleft it.

q[0] will always be the maximum value in the sliding window.
