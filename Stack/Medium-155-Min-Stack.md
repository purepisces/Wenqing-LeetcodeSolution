```python
class MinStack(object):

    def __init__(self):
        self.minstack = []
        
    def push(self, val):
        """
        :type val: int
        :rtype: None
        """
        self.minstack.append(val)
        
    def pop(self):
        """
        :rtype: None
        """
        self.minstack = self.minstack[0:len(self.minstack)-1]
        

    def top(self):
        """
        :rtype: int
        """
        return self.minstack[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return min(self.minstack)

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
