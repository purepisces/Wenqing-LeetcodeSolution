# Link:
- [125-Valid-Palindrome](https://leetcode.com/problems/valid-palindrome/description/)

# Intuition

This problem requires using some built-in functions like `s[l].isalnum()` and `s[l].lower()`. The basic requirement is straightforward and simple.

**Example:**

Input: `s = "A man, a plan, a canal: Panama"`

Output: `true`

Explanation: `"amanaplanacanalpanama"` is a palindrome.

We can set two pointers: one at the start of the input and the other at the end. The left pointer should always be less than the right pointer because if they are at the same location, we don't need to compare them. If the left pointer is greater than the right pointer, it doesn't make sense and will generate repeated comparisons.

We should skip non-alphanumeric characters. If initially, the left pointer points to a non-alphanumeric character, we should move it to the right until it meets the first alphanumeric character. However, we shouldn't keep moving to the right; we should ensure that the left pointer remains less than the right pointer and does not go out of bounds. The same applies to the right pointer. When they get to the correct positions, we convert the characters to their lowercase values and compare them. If they are not the same, we directly return `False`. If they are the same, we adjust the left and right pointers to new positions and continue the loop. If we traverse all the values, we simply return `True`.

# Approach
1. Set two pointers, `left` and `right`.
2. Initialize them to be `0` and `len(s) - 1` respectively.
3. Ensure the left pointer is less than the right pointer to avoid going out of bounds.
4. Compare the values of the characters at the left and right pointers.
5. If the left pointer is not alphanumeric, move it to the right; similarly for the right pointer.
6. Compare the lowercase values of the characters. If they are not the same, return `False`.
7. If they are the same, move the left and right pointers and continue the loop.


# Complexity
- Time complexity:
    $$O(n)$$
  - The algorithm traverses each character in the string at most once, resulting in linear time complexity.

- Space complexity:
    $$O(1)$$
  - The algorithm uses a constant amount of extra space for the pointers and variables, irrespective of the input size.

# Code
```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        l = 0
        r = len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l+=1
            while l < r and not s[r].isalnum():
                r-=1
            if s[l].lower() != s[r].lower():
                return False
            l+=1
            r-=1
        return True
```
___

my bad implementation
```python
#bad implementation
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        l = 0
        r = len(s) - 1
        while l < r:
            while not s[l].isalnum() and l < len(s)-1:
                l+=1
            while not s[r].isalnum() and r > 0:
                r-=1
            if l<r and s[l].isalnum() and s[r].isalnum() and s[l].lower()!=s[r].lower():
                return False
            l+=1
            r-=1
        return True
```
