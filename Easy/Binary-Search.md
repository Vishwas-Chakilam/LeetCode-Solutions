# Binary Search

## Description

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search for `target` in `nums`. If `target` exists, return its index. Otherwise, return `-1`.

You must write an algorithm with **O(log n)** runtime complexity.

**Example:**

**Input:**
```python
nums = [-1, 0, 3, 5, 9, 12]
target = 9
```

**Output:**
```python
4
```

**Explanation:**
The target `9` is found at index `4` in the array.

---

## Solution

### Approach

To solve this problem efficiently with **O(log n)** time complexity:
1. **Binary Search:** Since the array is sorted, we can use binary search to find the target. 
2. **Steps:**
   - Initialize two pointers, `left` and `right`, which point to the beginning and the end of the array, respectively.
   - While `left <= right`, calculate the middle index `mid`.
   - Compare the `target` with `nums[mid]`.
     - If `target == nums[mid]`, return `mid`.
     - If `target < nums[mid]`, narrow the search to the left half by setting `right = mid - 1`.
     - If `target > nums[mid]`, narrow the search to the right half by setting `left = mid + 1`.
   - If the `target` is not found, return `-1`.

### Code

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

### Complexity Analysis

- **Time Complexity:** O(log n), where `n` is the length of the array. The binary search divides the array in half each time.
- **Space Complexity:** O(1), as the search is performed in-place without additional space.

---

## Edge Cases

- **Empty Array:** If `nums` is an empty array, return `-1` since the target cannot be found.
- **Target Not Found:** If the target is not present in the array, the function will return `-1`.

---

## Additional Notes

- Binary search is an efficient way to search for an element in a sorted array, making it an ideal algorithm with logarithmic time complexity.
- It’s crucial to use the `mid = left + (right - left) // 2` formula to avoid overflow issues in languages with fixed integer sizes.

---

## References

**LeetCode Problem Link:** [Binary Search](https://leetcode.com/problems/binary-search/)
