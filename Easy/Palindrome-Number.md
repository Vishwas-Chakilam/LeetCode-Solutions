# Palindrome Number

## Description

Determine whether an integer is a palindrome. An integer is a palindrome if it reads the same backward as forward.

**Example:**

**Input:**
```python
x = 121
```

**Output:**
```python
True
```

**Explanation:**
The number `121` reads the same backward and forward, so it is a palindrome.

---

## Solution

### Approach

To determine if a number is a palindrome, you can reverse the number and compare it to the original number. If they are the same, the number is a palindrome.

**Note:** We avoid reversing the number by converting it to a string to prevent potential overflow issues with very large numbers.

### Code

```python
def is_palindrome(x):
    # Negative numbers and numbers ending in 0 (except 0 itself) are not palindromes
    if x < 0 or (x % 10 == 0 and x != 0):
        return False
    
    reversed_num = 0
    original = x

    while x > 0:
        digit = x % 10
        reversed_num = reversed_num * 10 + digit
        x //= 10
    
    return reversed_num == original
```

### Complexity Analysis

- **Time Complexity:** O(log n), where n is the number of digits in the integer. This is because we process each digit once.
- **Space Complexity:** O(1), as we use a constant amount of extra space.

---

## Edge Cases

- **Negative Numbers:** Any negative number cannot be a palindrome by definition.
- **Numbers Ending in 0:** Numbers ending in 0 are not palindromes unless the number is exactly 0.

---

## Additional Notes

- This approach avoids the pitfalls of integer overflow by working with the digits directly rather than manipulating the entire number as a single entity.
- It’s important to handle negative numbers and special cases where the number ends in zero.

---

## References

**LeetCode Problem Link:** [Palindrome Number](https://leetcode.com/problems/palindrome-number/)

---
