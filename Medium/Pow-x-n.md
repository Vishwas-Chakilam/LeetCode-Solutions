# Pow(x, n)

## Description

Implement `pow(x, n)`, which calculates `x` raised to the power of `n` (i.e., `x^n`).

**Example 1:**

**Input:**
```python
x = 2.0
n = 10
```

**Output:**
```python
1024.0
```

**Example 2:**

**Input:**
```python
x = 2.1
n = 3
```

**Output:**
```python
9.261
```

**Example 3:**

**Input:**
```python
x = 2.0
n = -2
```

**Output:**
```python
0.25
```

**Explanation:**  
`2^(-2)` equals `1 / (2^2) = 1 / 4 = 0.25`.

---

## Solution

### Approach

To solve this problem efficiently, we use **Exponentiation by Squaring**, which reduces the time complexity to **O(log n)**. Here's the breakdown:

1. **For positive powers**:
   - If `n` is even, we can reduce the problem by calculating `(x^n) = (x^(n//2)) * (x^(n//2))`.
   - If `n` is odd, multiply one more `x` after reducing: `(x^n) = (x^(n//2)) * (x^(n//2)) * x`.

2. **For negative powers**, we simply calculate the reciprocal:  
   \[
   x^n = \frac{1}{x^{-n}}
   \]

### Code

```python
def my_pow(x, n):
    if n == 0:
        return 1
    if n < 0:
        x = 1 / x
        n = -n
    
    result = 1
    while n > 0:
        if n % 2 == 1:
            result *= x
        x *= x
        n //= 2
    
    return result
```

### Complexity Analysis

- **Time Complexity:** O(log n), because we reduce the power `n` by half with each recursive or iterative step.
- **Space Complexity:** O(1), since we are using a constant amount of space.

---

## Edge Cases

- **n = 0:** Any number raised to the power of `0` is `1`.
- **n < 0:** The solution needs to handle negative exponents by returning the reciprocal of the positive exponent.
- **x = 0:** If `x` is `0` and `n` is positive, the result is always `0`. For `x = 0` and `n = 0`, it’s undefined, but for programming purposes, we return `1`.

---

## Additional Notes

- This algorithm avoids direct multiplication `n` times and instead reduces the time complexity to logarithmic by breaking down the problem using exponentiation by squaring.
- When dealing with floating-point numbers, small precision errors might occur due to the nature of floating-point arithmetic.

---

## References

**LeetCode Problem Link:** [Pow(x, n)](https://leetcode.com/problems/powx-n/)
