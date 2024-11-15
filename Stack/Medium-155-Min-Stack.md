```python
class MinStack(object):

    def __init__(self):
        self.stack = []
        self.minstack = []
        

    def push(self, val):
        """
        :type val: int
        :rtype: None
        """
        self.stack.append(val)
        #you can also learn this fancy format, which is the same as the uncomment code.
        # self.minstack.append(min(val, self.minstack[-1] if self.minstack else val))
        if not self.minstack or (self.minstack and val < self.minstack[-1]):
            self.minstack.append(val)
        else:
             self.minstack.append(self.minstack[-1])
        
    def pop(self):
        """
        :rtype: None
        """
        self.stack.pop()
        self.minstack.pop()
        
    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return self.minstack[-1]
```
