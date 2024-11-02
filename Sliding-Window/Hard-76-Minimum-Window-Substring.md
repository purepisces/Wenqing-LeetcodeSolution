```python
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if len(s) < len(t):
            return ""

        countT, window = {}, {}
        for c in t:
            countT[c] = 1 + countT.get(c, 0)

        have, need = 0, len(countT)
        res, resLen = [-1, -1], float("infinity")
        l = 0
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0)
            if c in countT and window[c] == countT[c]:
                have += 1
           
            while have == need:
               
                # update our result
                if (r - l + 1) < resLen:
                    res = [l, r]
                    resLen = r - l + 1
                # pop from the left of our window
                window[s[l]] -= 1
                if s[l] in countT and window[s[l]] < countT[s[l]]:
                    have -= 1
                    print(have)
                l += 1
        l, r = res
        return s[l : r + 1] if resLen != float("infinity") else ""
```
problem 1:
if change to  if s[l] in countT and window[s[l]] != countT[s[l]]:
                    have -= 1
Then for "aaaaaaaaaaaabbbbbcdd"
"abcdd", the result will be "aaaaaaaaaaaabbbbbcdd"
, which the expected output should be "abbbbbcdd"

problem 2:

if change  while have == need: to if have == need, then will have problem, which is for "ADOBECODEBANC"
 "ABC", the result is "ADOBEC", and expected is "BANC"

 when have == need, it could be "AABC" and "ABC" not directly the count number is the same.


Example:

s =
"ADOBECODEBANC"

t = "ABC"
```python
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if len(s) < len(t):
            return ""

        countT, window = {}, {}
        for c in t:
            countT[c] = 1 + countT.get(c, 0)

        have, need = 0, len(countT)
        res, resLen = [-1, -1], float("infinity")
        l = 0
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0)

            if c in countT and window[c] == countT[c]:
                have += 1

            while have == need:
                print("l is", l)
                print("r is", r)
                if (r - l + 1) < resLen:
                    res = [l, r]
                    resLen = r - l + 1
                    
                window[s[l]] -= 1
                if s[l] in countT and window[s[l]] < countT[s[l]]:
                    have -= 1
                l += 1
        l, r = res
        return s[l : r + 1] if resLen != float("infinity") else ""
```

```css
('l is', 0)
('r is', 5)
('l is', 1)
('r is', 10)
('l is', 2)
('r is', 10)
('l is', 3)
('r is', 10)
('l is', 4)
('r is', 10)
('l is', 5)
('r is', 10)
('l is', 6)
('r is', 12)
('l is', 7)
('r is', 12)
('l is', 8)
('r is', 12)
('l is', 9)
('r is', 12)
```

