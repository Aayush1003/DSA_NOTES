# Tries (Prefix Trees)

## Overview
A Trie (pronounced "try" or "tree" depending on context, derived from re**trie**val) is a tree-like data structure used to store a dynamic set of strings where keys are usually strings. It is highly optimized for string matching operations and prefix lookups.

## Properties
- The root represents an empty string.
- Each node stores a character and an array (or hash map) of pointers to its child nodes.
- Each node may also feature a boolean flag (e.g., `is_end_of_word`) that indicates whether the string ending at that node constitutes a valid word within the dataset.
- Paths from the root to any node define strings that share common prefixes.

## Uses and Applications
- Prefix Matching / Autocomplete.
- Spell Checking.
- Longest Prefix Matching (used in IP routing algorithms).
- Solving word games (e.g., Boggle).

## Complexity
Let `L` be the length of the string being processed.
- **Insertion Time:** `O(L)`.
- **Search Time:** `O(L)`.
- **Space Complexity:** `O(N \cdot L)` where `N` is the number of words, meaning Tries can be very memory intensive compared to Hash Maps if there are few common prefixes.

## Implementation Example
```python
class TrieNode:
    def __init__(self):
        self.children = {}  # {char: TrieNode}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    # Time: O(L)
    def insert(self, word: str) -> None:
        curr = self.root
        for char in word:
            if char not in curr.children:
                curr.children[char] = TrieNode()
            curr = curr.children[char]
        curr.is_end_of_word = True

    # Time: O(L)
    def search(self, word: str) -> bool:
        curr = self.root
        for char in word:
            if char not in curr.children:
                return False
            curr = curr.children[char]
        return curr.is_end_of_word

    # Time: O(L)
    def starts_with(self, prefix: str) -> bool:
        curr = self.root
        for char in prefix:
            if char not in curr.children:
                return False
            curr = curr.children[char]
        return True
```

## Tries vs Hash Maps
- Hash maps typically provide `O(1)` time complexity for general lookups, but examining if a string contains a particular prefix requires `O(L)`. 
- Tries avoid hash collisions.
- Tries are inherently sorted alphabetically, enabling ordered traversal easily.
