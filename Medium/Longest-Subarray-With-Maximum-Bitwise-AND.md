# Longest Subarray With Maximum Bitwise AND

## Description

You are given an integer array `nums`. Find the length of the longest subarray where the bitwise **AND** of all the elements is equal to the maximum possible bitwise **AND** of any subarray of `nums`.

**Example:**

**Input:**
```python
nums = [1, 2, 3, 3, 2, 2]
```

**Output:**
```python
2
```

**Explanation:**
- The maximum bitwise AND value is `3`.
- The subarray `[3, 3]` has the maximum bitwise AND value of `3` and its length is `2`.

---

## Solution

### Approach

To solve this problem, we need to break it down into the following steps:

1. **Maximum Bitwise AND Value:**
   - First, find the maximum element in the array. This is because the maximum bitwise AND of any subarray cannot be greater than the largest element of the array. If we find multiple instances of this maximum value in the array, the longest consecutive subarray of this maximum value will give us the answer.

2. **Longest Subarray Calculation:**
   - Traverse through the array and count the length of the subarray that contains consecutive maximum elements.
   - If you encounter a value less than the maximum, reset the count.

### Code

```python
def longest_subarray(nums):
    max_val = max(nums)
    longest = 0
    current_len = 0
    
    for num in nums:
        if num == max_val:
            current_len += 1
            longest = max(longest, current_len)
        else:
            current_len = 0
    
    return longest
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the array `nums`. We perform a single traversal to find the maximum value and another traversal to compute the longest subarray.
- **Space Complexity:** O(1), since we only use a few additional variables for counting and tracking the longest subarray.

---

## Edge Cases

- **Single Element Array:** If the array has only one element, the length of the longest subarray will be `1`.
- **All Elements Are the Same:** If all elements in `nums` are the same, the entire array will be the longest subarray.
- **All Elements Are Different:** If each element is different, and only one element is the maximum, the longest subarray will consist of just that one element.

---

## Additional Notes

- The bitwise AND of a number with itself is the number itself, which is why the maximum bitwise AND in any subarray will always be the maximum element of the array. Therefore, finding the longest subarray of consecutive maximum elements is the optimal solution.
  
---

## References

**LeetCode Problem Link:** [Longest Subarray With Maximum Bitwise AND](https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and/)
