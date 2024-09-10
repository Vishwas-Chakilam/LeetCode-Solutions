# Search Insert Position

## Description

Given a sorted array of distinct integers `nums` and a target value `target`, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with **O(log n)** runtime complexity.

**Example:**

**Input:**
```python
nums = [1, 3, 5, 6]
target = 5
```

**Output:**
```python
2
```

**Explanation:**
The target `5` is found at index `2` in the sorted array `nums`.

---

## Solution

### Approach

To solve this problem efficiently with **O(log n)** time complexity:
1. **Binary Search:** Since the array is sorted, we can use binary search to find either the exact index of `target` or the position where `target` would be inserted.

### Code

```python
def search_insert(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    # If not found, 'left' will be the insert position
    return left
```

### Complexity Analysis

- **Time Complexity:** O(log n), where `n` is the length of `nums` due to binary search.
- **Space Complexity:** O(1), as no extra space is used beyond the input variables.

---

## Edge Cases

- **Empty Array:** If `nums` is empty, return `0`, since the target would be inserted at the first position.
- **Target Greater Than All Elements:** If `target` is greater than all elements in `nums`, return the length of the array (`len(nums)`).
- **Target Smaller Than All Elements:** If `target` is smaller than all elements, return `0`.

---

## Additional Notes

- Binary search ensures the solution runs in O(log n), which is efficient even for large arrays.
- This approach guarantees that the index for either the found position or the insertion point is returned.

---

## References

**LeetCode Problem Link:** [Search Insert Position](https://leetcode.com/problems/search-insert-position/)

---
