```python






___
wrong implementation
```python
# wrong
if c == ".":
  for children in cur.children.values():
      if not dfs(i+1, children):
          return False
      return True
```
correct
```python
# correct
if c == ".":
  for children in cur.children.values():
      if dfs(i+1, children):
          return True
  return False
```
