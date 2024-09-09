# String to Integer (atoi)

## Description

Implement the `myAtoi` function that converts a string to an integer. The function should handle leading/trailing spaces, optional signs, and overflow conditions.

The algorithm should ignore any leading whitespace characters and process the string until it encounters a non-numeric character or the end of the string. The result should fit within a 32-bit signed integer range.

**Example:**

**Input:**
```python
s = "  -42"
```

**Output:**
```python
-42
```

**Explanation:**
The string represents the number `-42`, so the function returns `-42`.

---

## Solution

### Approach

To solve this problem, follow these steps:

1. **Trim Whitespace:** Remove any leading and trailing whitespace from the input string.
2. **Check for Sign:** Determine if the number is positive or negative based on the optional sign at the beginning of the string.
3. **Convert to Integer:** Convert the remaining numeric characters to an integer while handling potential overflow conditions.
4. **Return Result:** Ensure the result fits within the 32-bit signed integer range and return it.

### Code

```python
def myAtoi(s):
    # Define the bounds for 32-bit signed integer
    INT_MIN, INT_MAX = -2**31, 2**31 - 1

    # Initialize index and result
    i, result, sign = 0, 0, 1

    # Strip leading whitespaces
    s = s.strip()
    if not s:
        return 0

    # Check the sign
    if s[i] == '+' or s[i] == '-':
        sign = -1 if s[i] == '-' else 1
        i += 1

    # Convert characters to integer
    while i < len(s) and s[i].isdigit():
        digit = int(s[i])
        # Handle overflow
        if result > (INT_MAX - digit) // 10:
            return INT_MAX if sign == 1 else INT_MIN
        result = result * 10 + digit
        i += 1

    return sign * result
```

### Complexity Analysis

- **Time Complexity:** O(n), where n is the length of the string. The algorithm processes each character at most once.
- **Space Complexity:** O(1), as the algorithm uses a constant amount of extra space.

---

## Edge Cases

- **Empty String:** The function should return 0.
- **Whitespace Handling:** The function correctly trims leading and trailing spaces.
- **Overflow:** The function handles overflow conditions for 32-bit signed integers by returning `INT_MAX` or `INT_MIN`.

---

## Additional Notes

- The function handles optional signs and ensures that the final integer result fits within the specified bounds.
- This approach provides a straightforward and efficient solution for the problem.

---

## References

**LeetCode Problem Link:** [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

---
