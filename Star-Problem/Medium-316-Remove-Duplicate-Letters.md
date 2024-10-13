https://leetcode.com/problems/remove-duplicate-letters/description/
```python
class Solution(object):
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        # Keep track of the last occurrence of each character in the string
        last_occurrence = {ch: idx for idx, ch in enumerate(s)}
        
        stack = []
        
        for idx, ch in enumerate(s):
            # If the character is already in the stack, skip it
            if ch in stack:
                continue
            
            # While the stack is not empty, and the current character is smaller than the last character in the stack
            # and the last character will appear later, pop the stack
            while stack and ch < stack[-1] and idx < last_occurrence[stack[-1]]:
                stack.pop()
            
            # Add the current character to the stack
            stack.append(ch)
        
        # Join the stack to form the result string
        return ''.join(stack)
                
```

space complexity:

time complexity:

