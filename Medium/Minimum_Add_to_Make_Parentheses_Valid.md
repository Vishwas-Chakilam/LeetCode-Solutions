# 921. Minimum Add to Make Parentheses Valid

## 1. Problem Statement

Given a string `s` of `'('` and `')'` parentheses, you are asked to insert the minimum number of parentheses so that the resulting string is valid.

A string is valid if:
1. Open parentheses `'('` are closed by the corresponding close parentheses `')'` in the correct order.
2. Open and close parentheses must be balanced.

Return the minimum number of parentheses needed to make the string valid.

### Example 1:
```python
Input: s = "())"
Output: 1
Explanation: Add one '(' at the beginning to make the string valid: "(())"
```

### Example 2:
```python
Input: s = "((("
Output: 3
Explanation: Add three ')' at the end to make the string valid: "((()))"
```

---

## 2. Test Cases

### Test Case 1:
```python
Input: s = "()())("
Output: 2
Explanation: Add one `(` at the beginning and one `)` at the end.
```

### Test Case 2:
```python
Input: s = "())"
Output: 1
Explanation: Adding one `(` at the start will balance the string.
```

### Test Case 3:
```python
Input: s = "((("
Output: 3
Explanation: We need three `)` to balance the parentheses.
```

---

## 3. Approach

### 3a. Brute Force Approach

- For each character in the string, maintain a balance count.
- If we encounter a closing bracket without a preceding opening bracket, increment the required parentheses count.
- Time complexity: **O(n)** for traversing the string.
- Space complexity: **O(1)** since no additional space is required.

### 3b. Optimized Approach with Time and Space Complexity

- Traverse the string `s`. Keep track of unmatched opening brackets `open_needed` and unmatched closing brackets `close_needed`.
  - If a closing bracket `')'` appears without a matching opening bracket, increment `close_needed`.
  - If an opening bracket `'('` appears, increment `open_needed`. If there is an unmatched closing bracket, reduce `close_needed` instead.

- At the end of the traversal, return `open_needed + close_needed`, which gives the total number of parentheses required to balance the string.

#### Time Complexity:
- **O(n)**, where n is the length of the string (single pass).

#### Space Complexity:
- **O(1)**, constant space is used.

---

## 4. Code Implementation

### Python Implementation:
```python
def minAddToMakeValid(s: str) -> int:
    open_needed = 0
    close_needed = 0
    
    for char in s:
        if char == '(':
            open_needed += 1
        elif char == ')':
            if open_needed > 0:
                open_needed -= 1
            else:
                close_needed += 1
    
    return open_needed + close_needed

# Example usage:
s = "())"
print(minAddToMakeValid(s))  # Output: 1
```

### Java Implementation:
```java
public class Solution {
    public int minAddToMakeValid(String s) {
        int openNeeded = 0, closeNeeded = 0;
        
        for (char c : s.toCharArray()) {
            if (c == '(') {
                openNeeded++;
            } else if (c == ')') {
                if (openNeeded > 0) {
                    openNeeded--;
                } else {
                    closeNeeded++;
                }
            }
        }
        
        return openNeeded + closeNeeded;
    }
}
```

---

## 5. Edge Cases

- **Balanced String**: If the string is already valid, the result should be `0`.
- **Only Closing Parentheses**: If the string has only `)` characters, we need to add corresponding `(`.
- **Only Opening Parentheses**: If the string has only `(` characters, we need to add corresponding `)`.

---

## 6. References
- **LeetCode Problem**: [921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)
