# Word Ladder Solution

## Problem Statement
The **Word Ladder** problem involves finding the shortest transformation sequence from a given start word to a target word, changing only one letter at a time, while ensuring that each intermediate word exists in a given dictionary.

## Approach
The solution employs **Breadth-First Search (BFS)** to find the shortest transformation sequence efficiently.

### Steps:
1. **Graph Representation**:
   - The words are treated as nodes in a graph where an edge exists between two words if they differ by exactly one letter.
   - A queue is used to perform BFS from the start word.
   
2. **Breadth-First Search (BFS)**:
   - BFS ensures that the shortest transformation sequence is found first.
   - A set is used to track visited words to prevent redundant computations.

## Code
```python
from collections import deque
from typing import List

def word_ladder(beginWord: str, endWord: str, wordList: List[str]) -> int:
    wordSet = set(wordList)
    if endWord not in wordSet:
        return 0
    
    queue = deque([(beginWord, 1)])
    
    while queue:
        word, length = queue.popleft()
        if word == endWord:
            return length
        
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                newWord = word[:i] + c + word[i+1:]
                if newWord in wordSet:
                    queue.append((newWord, length + 1))
                    wordSet.remove(newWord)
    
    return 0
```

## Complexity Analysis
- **BFS Traversal**: O(N * M * 26), where:
  - N is the number of words in the dictionary.
  - M is the length of the words.
  - 26 represents the number of possible letter transformations.

## Example Usage
```python
beginWord = "hit"
endWord = "cog"
wordList = ["hot", "dot", "dog", "lot", "log", "cog"]
print(word_ladder(beginWord, endWord, wordList))
```

## Expected Output
```
5
```

## Contributing
Feel free to open an issue or submit a pull request if you have improvements or find bugs!

## License
This project is licensed under the MIT License.

