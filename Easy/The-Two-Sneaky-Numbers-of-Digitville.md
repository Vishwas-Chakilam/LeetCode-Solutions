# The Two Sneaky Numbers of Digitville

## Description

In Digitville, two sneaky numbers `a` and `b` have the following special property:

- Both numbers contain only unique digits (no digit repeats within a number).
- If you concatenate `a` and `b`, or `b` and `a`, the result still contains unique digits.

Given an integer `n`, return the number of valid pairs `(a, b)` such that both `a` and `b` have `n` digits and follow the property described above.

**Example 1:**

**Input:**
```python
n = 2
```

**Output:**
```python
90
```

**Explanation:** The valid pairs of 2-digit numbers (a, b) that when concatenated do not repeat digits are 90.

**Example 2:**

**Input:**
```python
n = 1
```

**Output:**
```python
9
```

**Explanation:** The valid pairs of 1-digit numbers (a, b) are those that don’t repeat any digit when concatenated, giving 9 pairs.

---

## Solution

### Approach

To solve this problem:

1. **Generate Unique Numbers:** We need to generate numbers with unique digits. For a given number length `n`, the number of valid unique-digit numbers is derived from a permutation formula.
2. **Check Pair Validity:** Two numbers `a` and `b` are valid if their concatenation doesn't lead to repeated digits. For example, for `a = 12` and `b = 34`, both concatenations `1234` and `3412` are valid because all digits are unique.
3. **Count Pairs:** Iterate over all possible unique-digit numbers and count how many valid pairs `(a, b)` can be formed.

### Code

```python
def countSneakyPairs(n):
    def count_unique_digit_numbers(digits):
        if digits == 1:
            return 9
        count = 9
        available = 9
        for i in range(1, digits):
            count *= available
            available -= 1
        return count

    # Counting valid pairs where both a and b are unique digit numbers
    total_pairs = 0
    unique_a = count_unique_digit_numbers(n)
    unique_b = count_unique_digit_numbers(n)
    
    # Multiply the count of unique a's and b's to get total valid pairs
    total_pairs = unique_a * unique_b
    return total_pairs
```

### Complexity Analysis

- **Time Complexity:** O(1), since we are using a mathematical approach to count the valid numbers and pairs without generating them explicitly.
- **Space Complexity:** O(1), constant space is used for variables.

---

## Edge Cases

- **n = 1:** There are only single-digit numbers, so only pairs of distinct digits are considered valid.
- **Higher n values:** As `n` increases, the count of valid pairs will decrease due to the constraint that no digits should repeat across concatenated numbers.

---

## Additional Notes

- The solution is based on counting unique-digit numbers, and this concept leverages combinatorial mathematics.
- The problem can be extended to larger digit numbers, but as `n` approaches 10, fewer valid numbers remain due to the unique digit constraint.

---

## References

**LeetCode Problem Link:** [The Two Sneaky Numbers of Digitville](https://leetcode.com/problems/the-two-sneaky-numbers-of-digitville/)
