# **Find Words Containing a Character**  

## **Problem Statement**  
Given a list of words and a character `x`, return a list of indices of words that contain `x`.  

## **Solution Explanation**  
The solution iterates through the list of words, checking if `x` is present in each word. If found, the index is added to the result list.  

---

## **Code Implementation**  
```python
from typing import List

class Solution:
    def findWordsContaining(self, words: List[str], x: str) -> List[int]:
        res = []
        for i in range(len(words)):
            if x in words[i]:  # Check if character x is in the word
                res.append(i)
        return res
```

---

## **Complexity Analysis**  
- **Iterating through words**: \( O(N) \)  
- **Checking character presence (`x in words[i]`)**: \( O(M) \) in the worst case (where M is the word length)  
- **Overall Complexity**: \( O(N \times M) \)  

---

## **Example Usage**  
```python
sol = Solution()
words = ["apple", "banana", "cherry", "date"]
x = "a"
print(sol.findWordsContaining(words, x))  # Output: [0, 1, 3] (indices of words containing 'a')
```

---

## **Edge Cases Considered**  
✅ `x` not present in any word → Returns an empty list  
✅ `x` appears multiple times → Still stores only the index once  
✅ `words` contains empty strings → Skips correctly  
✅ `x` is an empty string → No valid check, should return all indices  

---

## **Why This Solution Works Well?**  
✅ **Simple & Clear Logic**  
✅ **Direct Character Check for Efficiency**  
✅ **Works for Various Inputs & Edge Cases**  

---
