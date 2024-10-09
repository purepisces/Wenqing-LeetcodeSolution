```python
class TrieNode():
    def __init__(self):
        self.children = {}
        self.endOfWord = False

class WordDictionary(object):

    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word):
        """
        :type word: str
        :rtype: None
        """
        cur = self.root
        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode()
            cur = cur.children[c]
        cur.endOfWord = True
        
    def search(self, word):
        """
        :type word: str
        :rtype: bool
        """
        def dfs(j, root):
            cur = root
            for i in range(j,len(word)):
                c = word[i]
                if c == ".":
                    for child in cur.children.values():
                        if dfs(i+1, child):
                            return True
                    return False
                else:
                    if c not in cur.children:
                        return False
                    cur = cur.children[c]
            return cur.endOfWord
        return dfs(0, self.root)



# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```



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
