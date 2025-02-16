# **LeetCode Solution: Count Consistent Strings**  

## **Problem Statement**  
You are given a string `allowed` consisting of distinct characters and an array of strings `words`. A string is **consistent** if all characters in the string appear in `allowed`.  

Return the number of **consistent** strings in the array `words`.  

## **Solution Explanation**  
This solution efficiently determines the number of consistent strings using Python sets.  

### **Approach**  
1. Convert the `allowed` string into a set `allowed_set` for quick lookup.  
2. Use list comprehension and the `issubset()` method to check if each word consists only of characters from `allowed_set`.  
3. Count the number of words that are subsets of `allowed_set` using `sum()`.  

### **Code**  
```python
from typing import List

class Solution:
    def countConsistentStrings(self, allowed: str, words: List[str]) -> int:
        allowed_set = set(allowed)
        return sum(set(word).issubset(allowed_set) for word in words)
```

### **Complexity Analysis**  
- **Converting `allowed` to a set:** \( O(A) \), where \( A \) is the length of `allowed`.  
- **Checking each word:** \( O(W \cdot L) \), where \( W \) is the number of words and \( L \) is the average word length.  
- **Overall complexity:** \( O(A + W \cdot L) \), which is efficient for large inputs.  

### **Example Usage**  
```python
solution = Solution()
allowed = "ab"
words = ["ad","bd","aaab","baa","badab"]
print(solution.countConsistentStrings(allowed, words))  # Output: 2
```

### **Edge Cases Considered**  
- When `words` is empty  
- When `allowed` contains all possible characters  
- When none of the words are consistent  

### **Why This Solution Works Well?**  
- **Uses sets** for fast lookups.  
- **Simple and concise**, leveraging Python's `issubset()` method.  
- **Scales efficiently** with larger inputs.  

---
