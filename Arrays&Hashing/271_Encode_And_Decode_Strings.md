```python
class Solution:

    def encode(self, strs: List[str]) -> str:
        res = ''
        for s in strs:
            res += str(len(s)) + '#' + s
        print(res)
        return res

    def decode(self, s: str) -> List[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            i = j + 1
            j = i + length
            res.append(s[i:j])
            i = j
        return res
```

# Link:
- [271_Encode_And_Decode_Strings](https://leetcode.com/problems/encode-and-decode-strings/description/)

# Intuition

I watched Neetnode for this problem. If we just encode `['hello', 'world']` to `'helloworld'` and then decode it back, we will not know where to separate the words. We could consider using special characters to separate them. For example, we could add `#`, making it `'hello#world'`.

However, if the words are `['hello', 'wo#rld']`, encoding them would result in `'hello#wo#rld'`, and decoding it back would give `['hello', 'wo', 'rld']`. This means using only special characters is not a reliable method.

Instead, we should integrate the length of each word in the encoding information. For example, encoding `['hello', 'world']` as `'5hello5world'` might work, but if the input is `['1hello', 'world']`, it will encode to `'61hello5world'`, making it appear that the first word is of length 61. Thus, adding only integers or special characters is not sufficient.

A better approach is to combine the length information with a special character. For example, encoding `['hello', 'world']` would result in `'5#hello5#world'`.

We use two pointers, `i` and `j`, in the decoding process. Pointer `i` is used to traverse the encoded string, while pointer `j` is used to locate the `#` character that separates the length of each word from the word itself. This helps us determine the length of each word and extract the word accordingly.

# Approach

To encode a list of strings, we will concatenate each string with its length and a special character `#`. This way, during decoding, we can easily identify the length of each string and extract it accordingly.

## Encoding:
1. Initialize an empty result string.
2. For each string in the input list, append its length, a `#` character, and the string itself to the result string.

## Decoding:
1. Initialize an empty result list.
2. Use two pointers, `i` and `j`:
   - `i` traverses the encoded string.
   - `j` locates the `#` character to determine the length of each word.
3. Iterate through the encoded string, identifying lengths and corresponding substrings using the `#` character as a separator.
4. Extract the substrings based on their lengths and append them to the result list.

# Complexity

- **Time Complexity**:
  $$O(N)$$
  - where $N$ is the total length of all strings in the input list. We traverse each character once during both encoding and decoding.
- **Space Complexity**:
  $$O(N)$$
  - where $N$ is the total length of all strings in the input list. We use extra space for the encoded string and the result list during decoding.

# Code
```python
class Solution:

    def encode(self, strs: List[str]) -> str:
        res = ''
        for s in strs:
            res += str(len(s)) + '#' + s
        print(res)
        return res

    def decode(self, s: str) -> List[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            i = j + 1
            j = i + length
            res.append(s[i:j])
            i = j
        return res
```


