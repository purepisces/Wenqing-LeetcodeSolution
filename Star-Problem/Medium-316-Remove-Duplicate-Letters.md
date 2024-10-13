https://leetcode.com/problems/remove-duplicate-letters/description/
```python
class Solution(object):
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        last_occurrence = {char: idx for idx, char in enumerate(s)}  # Store last occurrence of each character
        stack = []
        visited = set()  # To track the characters already in the stack
        
        for i, char in enumerate(s):
            if char in visited:
                continue  # Skip if the character is already in the stack
            
            # Remove characters from the stack if they are greater than the current character and 
            # they appear later in the string (based on their last occurrence)
            while stack and stack[-1] > char and last_occurrence[stack[-1]] > i:
                removed_char = stack.pop()
                visited.remove(removed_char)
            
            # Add current character to stack and mark it as visited
            stack.append(char)
            visited.add(char)
        
        return ''.join(stack)
```

space complexity:

time complexity:

