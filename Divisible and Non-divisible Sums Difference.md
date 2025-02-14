# LeetCode 2894: Divisible and Non-divisible Sums Difference

## Problem Statement
You are given three positive integers: `n`, `m`, and `k`.
- Compute the sum of all integers from `1` to `n` that are **divisible** by `m`.
- Compute the sum of all integers from `1` to `n` that are **not divisible** by `k`.
- Return the absolute difference between these two sums.

## Example
### Example 1:
**Input:**
```python
n = 10, m = 3, k = 5
```
**Output:**
```python
19
```
**Explanation:**
- Numbers divisible by `m = 3` in the range `[1, 10]`: **3, 6, 9** → Sum = `3 + 6 + 9 = 18`
- Numbers **not** divisible by `k = 5` in the range `[1, 10]`: **1, 2, 3, 4, 6, 7, 8, 9** → Sum = `1 + 2 + 3 + 4 + 6 + 7 + 8 + 9 = 40`
- Absolute difference: `|40 - 18| = 22`

## Approach
1. **Iterate through numbers from `1` to `n`**:
   - Add numbers **divisible** by `m` to `sumDiv`.
   - Add numbers **not divisible** by `k` to `sumNonDiv`.
2. **Calculate absolute difference**: `abs(sumNonDiv - sumDiv)`
3. **Return the result**

## Code Implementation
### Python Solution
```python
def differenceOfSums(n: int, m: int, k: int) -> int:
    sumDiv, sumNonDiv = 0, 0
    
    for i in range(1, n + 1):
        if i % m == 0:
            sumDiv += i
        if i % k != 0:
            sumNonDiv += i
    
    return abs(sumNonDiv - sumDiv)

# Example Test Case
print(differenceOfSums(10, 3, 5))  # Output: 22
```

## Complexity Analysis
- **Time Complexity:** `O(n)`, since we iterate through all numbers from `1` to `n` once.
- **Space Complexity:** `O(1)`, as we use only a few integer variables.

## Optimized Approach
Instead of looping through all numbers from `1` to `n`, we can use arithmetic series formulas:
- Sum of numbers divisible by `m`: `m * (p * (p + 1)) / 2`, where `p = n // m`
- Sum of numbers **not** divisible by `k`: Total sum minus sum of numbers divisible by `k`

### Optimized Code
```python
def sum_divisible_by(n, x):
    p = n // x
    return x * (p * (p + 1)) // 2

def differenceOfSumsOptimized(n: int, m: int, k: int) -> int:
    total_sum = (n * (n + 1)) // 2
    sumDiv = sum_divisible_by(n, m)
    sumDivK = sum_divisible_by(n, k)
    sumNonDiv = total_sum - sumDivK
    
    return abs(sumNonDiv - sumDiv)

# Example Test Case
print(differenceOfSumsOptimized(10, 3, 5))  # Output: 22
```

## Complexity Analysis (Optimized)
- **Time Complexity:** `O(1)`, as we use mathematical formulas instead of looping.
- **Space Complexity:** `O(1)`, since we only store a few integer variables.

## Summary
- A simple approach iterates over numbers (`O(n)` complexity).
- An optimized approach uses mathematical formulas (`O(1)` complexity).
- This problem helps understand arithmetic progressions and modular conditions.

## Tags
`#Math` `#BruteForce` `#Optimization` `#Python` `#Modulo`

## Resources
- [LeetCode Problem Link](https://leetcode.com/problems/divisible-and-non-divisible-sums-difference/)

