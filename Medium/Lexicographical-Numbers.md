# Lexicographical Numbers

## Description

Given an integer `n`, return all the numbers in the range `[1, n]` sorted in lexicographical order.

**Example 1:**

**Input:**
```python
n = 13
```

**Output:**
```python
[1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Example 2:**

**Input:**
```python
n = 20
```

**Output:**
```python
[1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 2, 20, 3, 4, 5, 6, 7, 8, 9]
```

---

## Solution

### Approach

This problem can be solved using **depth-first search (DFS)** in the range `[1, n]`:

1. **Depth-First Search (DFS):** Starting from 1, we explore all numbers in lexicographical order by recursively generating the next lexicographical number.
   - If the current number multiplied by 10 is less than or equal to `n`, we move deeper.
   - If the current number + 1 is within the bounds and doesn’t violate lexicographical order, we proceed.

### Code

```python
def lexicalOrder(n):
    result = []

    def dfs(current):
        if current > n:
            return
        result.append(current)
        for i in range(10):
            next_number = current * 10 + i
            if next_number <= n:
                dfs(next_number)
            else:
                break

    for i in range(1, 10):
        dfs(i)

    return result
```

### Complexity Analysis

- **Time Complexity:** O(n). We visit each number from 1 to `n` exactly once.
- **Space Complexity:** O(n), due to the recursion stack and the result array holding the numbers.

---

## Edge Cases

- **Single Number:** If `n = 1`, the result will simply be `[1]`.
- **Power of Ten:** If `n` is a power of 10 (e.g., `n = 10, 100, 1000`), the lexicographical order will include numbers starting from `1` to `n` in sorted order.
- **Large `n`:** The DFS approach will handle large values of `n` efficiently without generating all numbers at once.

---

## Additional Notes

- This problem can also be solved by directly generating the numbers in lexicographical order and sorting them. However, the DFS approach is more efficient since it avoids unnecessary number generation and sorting.
- The recursive approach ensures that we generate the numbers in the correct order naturally.

---

## References

**LeetCode Problem Link:** [Lexicographical Numbers](https://leetcode.com/problems/lexicographical-numbers/)
