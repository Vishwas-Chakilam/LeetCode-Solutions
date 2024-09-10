# Remove Duplicates from Sorted Array

## Description

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be kept the same. 

Return the number of unique elements and modify the input array in-place to reflect these unique elements.

**Example:**

**Input:**
```python
nums = [1, 1, 2]
```

**Output:**
```python
2, nums = [1, 2, _]
```

**Explanation:**
The function should return 2, and the first two elements of `nums` should be modified to `[1, 2]`. It does not matter what you leave beyond the returned length.

---

## Solution

### Approach

To solve this problem in-place:
1. **Two Pointers Technique:**
   - Use one pointer (`i`) to track the position where the next unique element should go.
   - Use another pointer (`j`) to scan through the array.
   - Whenever a new unique element is found, move it to the correct position using the `i` pointer and increment `i`.

### Code

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    
    # Pointer for the next unique element
    i = 0
    
    # Iterate through the array
    for j in range(1, len(nums)):
        # If we find a new unique element
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]
    
    # Return the number of unique elements
    return i + 1
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the array. We traverse the array once.
- **Space Complexity:** O(1), since the solution modifies the input array in place without using extra space.

---

## Edge Cases

- **Empty Array:** If the input array is empty, return 0.
- **Single Element Array:** If the array has only one element, return 1.
- **No Duplicates:** If there are no duplicates in the array, the function should return the length of the array.

---

## Additional Notes

- The solution does not require any extra memory and works in O(n) time, making it efficient for large arrays.
- The function modifies the array in-place and returns the number of unique elements.

---

## References

**LeetCode Problem Link:** [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
