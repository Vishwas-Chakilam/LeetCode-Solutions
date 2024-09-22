# K-th Smallest in Lexicographical Order

## Description

Given an integer `n` and an integer `k`, return the k-th smallest integer in the range from `1` to `n`, sorted in lexicographical order.

**Example 1:**

**Input:**
```python
n = 13
k = 2
```

**Output:**
```python
10
```

**Explanation:** The numbers in lexicographical order are `[1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9]`, and the 2nd smallest is `10`.

**Example 2:**

**Input:**
```python
n = 1
k = 1
```

**Output:**
```python
1
```

---

## Solution

### Approach

To find the k-th smallest number in lexicographical order, we can use a **depth-first search (DFS)** approach:

1. **DFS Traversal:** Start from `1` and explore numbers in lexicographical order:
   - For each number, we generate the next lexicographical number by multiplying the current number by `10` and adding digits `0` through `9`.
   - Track how many numbers have been counted until reaching `k`.

2. **Count until k:** Whenever we reach a valid number, we increment a count. If we reach `k`, we return that number.

### Code

```python
def findKthNumber(n, k):
    current = 1
    k -= 1  # Since we are starting from the first number
    
    while k > 0:
        steps = calculate_steps(n, current, current + 1)
        
        if steps <= k:
            current += 1
            k -= steps
        else:
            current *= 10
            k -= 1
            
    return current

def calculate_steps(n, curr, next_curr):
    steps = 0
    while curr <= n:
        steps += min(n + 1, next_curr) - curr
        curr *= 10
        next_curr *= 10
    return steps
```

### Complexity Analysis

- **Time Complexity:** O(log n), where `n` is the maximum value. The DFS traversal effectively reduces the search space logarithmically.
- **Space Complexity:** O(1), since we are using a constant amount of space for variables.

---

## Edge Cases

- **k = 1:** The first smallest number is always `1`.
- **n is Small:** For small values of `n`, the result will simply be derived from the limited range of numbers.
- **Large k:** If `k` is larger than the total count of numbers, the logic ensures that it operates correctly within the bounds of `n`.

---

## Additional Notes

- The DFS-based approach is efficient as it directly computes how many numbers lie between two lexicographical boundaries without generating all of them.
- The function `calculate_steps` helps in determining how many numbers can be reached in a lexicographical path before exceeding `n`.

---

## References

**LeetCode Problem Link:** [K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)

---
