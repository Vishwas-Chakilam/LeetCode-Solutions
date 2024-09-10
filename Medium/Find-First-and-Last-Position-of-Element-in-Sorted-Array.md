# Find First and Last Position of Element in Sorted Array

## Description

Given an array of integers `nums` sorted in non-decreasing order, and an integer `target`, find the starting and ending position of the `target` in the array.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with **O(log n)** runtime complexity.

**Example:**

**Input:**
```python
nums = [5, 7, 7, 8, 8, 10]
target = 8
```

**Output:**
```python
[3, 4]
```

**Explanation:**
The target `8` first appears at index `3` and last appears at index `4`.

---

## Solution

### Approach

To solve this problem efficiently with **O(log n)** time complexity:
1. **Binary Search:** Since the array is sorted, use binary search to find the first and last positions of the `target`.
2. **Find First Position:** Perform a binary search to find the first occurrence of the `target`.
3. **Find Last Position:** Perform a second binary search to find the last occurrence of the `target`.

### Code

```python
def search_range(nums, target):
    # Helper function to find the first or last position
    def binary_search(nums, target, find_first):
        left, right = 0, len(nums) - 1
        result = -1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if nums[mid] == target:
                result = mid
                if find_first:
                    right = mid - 1  # Search the left side for the first occurrence
                else:
                    left = mid + 1  # Search the right side for the last occurrence
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return result
    
    first_position = binary_search(nums, target, True)
    last_position = binary_search(nums, target, False)
    
    return [first_position, last_position]
```

### Complexity Analysis

- **Time Complexity:** O(log n) for each binary search, and since we perform two binary searches, the overall time complexity is O(log n).
- **Space Complexity:** O(1), since no extra space is used except for variables.

---

## Edge Cases

- **Empty Array:** If `nums` is empty, return `[-1, -1]`.
- **Target Not Found:** If the `target` is not found in `nums`, return `[-1, -1]`.
- **Single Occurrence:** If the `target` appears only once, the first and last positions should be the same.

---

## Additional Notes

- Binary search ensures that we achieve the desired O(log n) time complexity, making the solution efficient for large arrays.
- This solution works well even when the `target` appears multiple times or not at all in the array.

---

## References

**LeetCode Problem Link:** [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

---
