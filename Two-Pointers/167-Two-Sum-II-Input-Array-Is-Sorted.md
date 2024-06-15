# Link:
- [167-Two-Sum-II-Input-Array-Is-Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

# Intuition
This problem is a straightforward two-pointer problem.

Input: `numbers = [2, 7, 11, 15]`, `target = 9`

Output: `[1, 2]`

Explanation: The sum of `2` and `7` is `9`. Therefore, `index1 = 1`, `index2 = 2`. We return `[1, 2]`.

We initialize the left pointer at the start of the array and the right pointer at the end of the array. The while loop condition is `while l < r`. If the sum of `nums[l] + nums[r]` is less than the target, we move the left pointer to the right, since the array is sorted in increasing order. If the sum is greater than the target, we move the right pointer to the left to decrease the sum. If the sum is equal to the target, we return the indices `[l + 1, r + 1]`.

We should move either the left or right pointer only once during each iteration of the loop. If not, we might miss the correct pair. For example, the following is an incorrect solution:

```python
  def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        l = 0
        r = len(numbers) - 1
        while numbers[l] + numbers[r] > target:
            r -= 1
        while numbers[l] + numbers[r] < target:
            l -= 1
        return [l+1, r+1]
```
This solution is incorrect. Consider [1, 2, 3, 4, 4, 9] with a target of 8. It will return [0, 5], but it should return [4, 5]. The pointer movement logic doesn't account for checking both pointers simultaneously. Adjusting only one pointer at a time might miss valid pairs, and it does not handle boundary conditions properly.

# Approach

1. Set two pointers: the left pointer at the start of the array (`l = 0`) and the right pointer at the end of the array (`r = len(numbers) - 1`).
2. Iterate while `l < r`:
    - If the sum of `numbers[l] + numbers[r]` is less than the target, move the left pointer to the right (`l += 1`).
    - If the sum is greater than the target, move the right pointer to the left (`r -= 1`).
    - If the sum is equal to the target, return the indices `[l + 1, r + 1]` (1-based index).

# Complexity
- Time complexity:
  $$O(n)$$
  - We traverse the list at most once with the two pointers, resulting in a linear time complexity.

- Space complexity:
  $$O(1)$$
  - We only use a constant amount of extra space for the pointers and temporary variables.

# Code
```
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        l = 0
        r = len(numbers) -1
        while l < r:
            if numbers[l] + numbers[r] < target:
                l+=1
            elif numbers[l] + numbers[r] > target:
                r-=1
            else:
                return[l+1, r+1]
```
