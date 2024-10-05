# 567. Permutations in String

## 1. Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

### Example 1:
```python
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

### Example 2:
```python
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: s1 = "abc", s2 = "bbbca"
Output: true
Explanation: s2 contains a permutation of s1 ("bca").
```

### Test Case 2:
```python
Input: s1 = "abcd", s2 = "aabbccdd"
Output: false
Explanation: No permutation of s1 is found in s2.
```

### Test Case 3:
```python
Input: s1 = "xyz", s2 = "yzx"
Output: true
Explanation: s2 contains the permutation "xyz".
```

---

## 3. Approach

### 3a. Brute Force Approach
- Generate all permutations of `s1`.
- Check if any permutation is a substring of `s2`.
- This is inefficient because generating all permutations has a time complexity of **O(n!)**, where `n` is the length of `s1`.

#### Time Complexity:
- **O(n! * m)** where `n` is the length of `s1` and `m` is the length of `s2`.

#### Space Complexity:
- **O(n)** for storing permutations.

### 3b. Sliding Window Approach (Optimized)
- Instead of generating permutations, use a sliding window over `s2`.
- Keep a frequency count of characters in `s1` and compare it with the frequency count of the current window of length `s1` in `s2`.
- If the two counts match, it means there’s a permutation of `s1` in the current window of `s2`.

#### Time Complexity:
- **O(n + m)**, where `n` is the length of `s1` and `m` is the length of `s2`.

#### Space Complexity:
- **O(1)**, as we only need a fixed amount of space for the frequency counts.

---

## 4. Code Implementation

### Python Implementation:
```python
from collections import Counter

def checkInclusion(s1: str, s2: str) -> bool:
    n, m = len(s1), len(s2)
    if n > m:
        return False
    
    s1_count = Counter(s1)
    window_count = Counter(s2[:n])
    
    if s1_count == window_count:
        return True
    
    for i in range(n, m):
        window_count[s2[i]] += 1
        window_count[s2[i - n]] -= 1
        
        if window_count[s2[i - n]] == 0:
            del window_count[s2[i - n]]
        
        if window_count == s1_count:
            return True
    
    return False

# Example
s1 = "ab"
s2 = "eidbaooo"
print(checkInclusion(s1, s2))  # Output: True
```

### Java Implementation:
```java
import java.util.HashMap;

public class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) return false;
        
        int[] s1Count = new int[26];
        int[] s2Count = new int[26];
        
        for (int i = 0; i < s1.length(); i++) {
            s1Count[s1.charAt(i) - 'a']++;
            s2Count[s2.charAt(i) - 'a']++;
        }
        
        for (int i = 0; i < s2.length() - s1.length(); i++) {
            if (matches(s1Count, s2Count)) return true;
            s2Count[s2.charAt(i + s1.length()) - 'a']++;
            s2Count[s2.charAt(i) - 'a']--;
        }
        
        return matches(s1Count, s2Count);
    }
    
    private boolean matches(int[] s1Count, int[] s2Count) {
        for (int i = 0; i < 26; i++) {
            if (s1Count[i] != s2Count[i]) return false;
        }
        return true;
    }
}
```

---

## 5. Edge Cases
- **Empty Strings**: If either `s1` or `s2` is empty, return `false`.
- **s1 longer than s2**: If the length of `s1` is greater than the length of `s2`, return `false`.
- **Exact match**: If `s1` is exactly the same as a substring in `s2`, return `true`.

---

## 6. References
- **LeetCode Problem**: [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
---
