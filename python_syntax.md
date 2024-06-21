1.
```python
countT = {}
for c in t:
    countT[c] = 1 + countT.get(c, 0)
```
same to 
```python
countT = {}
for c in t:
    if c not in countT:
        countT[c] = 1
    else:
        countT[c] += 1
```
