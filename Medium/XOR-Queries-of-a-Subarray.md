# XOR Queries of a Subarray

## Description

You are given an array `arr` of integers, and an array `queries`, where `queries[i] = [Li, Ri]`. For each query `i`, compute the XOR of elements from index `Li` to `Ri` (inclusive) and return an array of the results.

**Example:**

**Input:**
```python
arr = [1, 3, 4, 8]
queries = [[0, 1], [1, 2], [0, 3], [3, 3]]
```

**Output:**
```python
[2, 7, 14, 8]
```

**Explanation:**
- The XOR of the subarray from index `0` to `1` is `1 ^ 3 = 2`.
- The XOR of the subarray from index `1` to `2` is `3 ^ 4 = 7`.
- The XOR of the subarray from index `0` to `3` is `1 ^ 3 ^ 4 ^ 8 = 14`.
- The XOR of the subarray from index `3` to `3` is `8`.

---

## Solution

### Approach

A **naive approach** would be to compute the XOR for each query by iterating through the subarray, but this would be inefficient with a time complexity of **O(n * m)**, where `n` is the length of `arr` and `m` is the number of queries.

A more **optimal approach** involves using a **prefix XOR** array:

1. **Prefix XOR:** Create a prefix XOR array such that `prefix[i]` represents the XOR of elements from the start of the array up to index `i`. This allows us to compute the XOR of any subarray `[L, R]` efficiently:
   \[
   \text{XOR}(L, R) = \text{prefix}[R] \oplus \text{prefix}[L-1]
   \]
   If `L == 0`, the XOR result is simply `prefix[R]`.

### Code

```python
def xor_queries(arr, queries):
    n = len(arr)
    # Create a prefix XOR array
    prefix = [0] * (n + 1)
    
    # Compute prefix XOR
    for i in range(n):
        prefix[i + 1] = prefix[i] ^ arr[i]
    
    result = []
    # Answer each query using the prefix XOR array
    for L, R in queries:
        result.append(prefix[R + 1] ^ prefix[L])
    
    return result
```

### Complexity Analysis

- **Time Complexity:** O(n + m), where `n` is the length of the array `arr` (for computing the prefix XOR) and `m` is the number of queries.
- **Space Complexity:** O(n), since we store the prefix XOR array of size `n + 1`.

---

## Edge Cases

- **Single Element Queries:** If the query is for a single element, the result will be the element itself (i.e., `arr[L]` when `L == R`).
- **Empty Array:** If `arr` is empty, the result should also be empty.

---

## Additional Notes

- Using a prefix XOR array significantly reduces the time complexity of each query to **O(1)**, making it efficient for large inputs.
- XOR operations have useful properties that help in these types of problems: `a ^ a = 0` and `a ^ 0 = a`.

---

## References

**LeetCode Problem Link:** [XOR Queries of a Subarray](https://leetcode.com/problems/xor-queries-of-a-subarray/)
