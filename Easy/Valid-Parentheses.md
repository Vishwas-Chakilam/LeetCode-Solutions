# Valid Parentheses

## Description

Given a string `s` containing just the characters `(`, `)`, `{`, `}`, `[` and `]`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

**Example:**

**Input:**
```python
s = "()[]{}"
```

**Output:**
```python
True
```

**Explanation:**
The string contains valid parentheses, where each opening bracket is closed in the correct order by the corresponding closing bracket.

---

## Solution

### Approach

To determine if the parentheses are valid:
1. **Use a Stack:** Iterate through the string and use a stack to keep track of opening brackets. 
   - For every closing bracket encountered, check if the top of the stack is the corresponding opening bracket. If so, pop the top of the stack.
   - If the stack is empty at the end and all brackets have been matched, the string is valid.
2. **Early Termination:** If at any point, the brackets do not match or the stack is empty while expecting a match, return `False`.

### Code

```python
def is_valid(s):
    # Map of closing to opening brackets
    bracket_map = {')': '(', '}': '{', ']': '['}
    stack = []
    
    # Traverse through the string
    for char in s:
        # If it's a closing bracket
        if char in bracket_map:
            # Pop the top of the stack if it's not empty, else assign a dummy value
            top_element = stack.pop() if stack else '#'
            
            # Check if the top matches the expected opening bracket
            if bracket_map[char] != top_element:
                return False
        else:
            # It's an opening bracket, push to the stack
            stack.append(char)
    
    # If the stack is empty, all brackets were matched correctly
    return not stack
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the string. Each character is pushed or popped from the stack at most once.
- **Space Complexity:** O(n), as we store all opening brackets in the stack.

---

## Edge Cases

- **Empty String:** An empty string is valid, so the output should be `True`.
- **Mismatched Brackets:** Handle cases where the number of opening and closing brackets does not match.
- **Unmatched Closing Brackets:** If a closing bracket appears without a matching opening bracket, return `False`.

---

## Additional Notes

- The stack-based approach ensures that brackets are properly matched and appear in the correct order.
- This solution works efficiently for any length of valid or invalid parentheses strings.

---

## References

**LeetCode Problem Link:** [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

---
