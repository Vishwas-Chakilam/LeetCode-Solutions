# Remove Element

## Description

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place**. The relative order of the elements may be changed.

Return the number of elements that are not equal to `val`.

**Example:**

**Input:**
```python
nums = [3, 2, 2, 3]
val = 3
```

**Output:**
```python
2, nums = [2, 2, _, _]
```

**Explanation:**
The function should return `2`, indicating that there are two elements in the array not equal to `val`. The first two elements of `nums` should be modified to `[2, 2]`. It does not matter what is left beyond the returned length.

---

## Solution

### Approach

To solve this problem in-place:
1. **Two Pointers Technique:** 
   - Use one pointer (`i`) to keep track of the current position for elements that are not equal to `val`.
   - Iterate over the array with another pointer (`j`). 
   - Whenever `nums[j]` is not equal to `val`, move it to the `i` position and increment `i`.

### Code

```python
def remove_element(nums, val):
    i = 0
    
    # Iterate through the array
    for j in range(len(nums)):
        if nums[j] != val:
            nums[i] = nums[j]
            i += 1
            
    # Return the number of elements not equal to 'val'
    return i
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the array. We traverse the array once.
- **Space Complexity:** O(1), since the solution modifies the input array in place without using extra space.

---

## Edge Cases

- **Empty Array:** If the input array is empty, return 0.
- **All Elements are Equal to `val`:** If all elements are equal to `val`, return 0.
- **No Element Equals `val`:** If no element equals `val`, return the length of the array.

---

## Additional Notes

- This solution efficiently removes all instances of `val` in the array and returns the new length in O(n) time.
- The input array is modified in place, meaning no extra space is required apart from the original input array.

---

## References

**LeetCode Problem Link:** [Remove Element](https://leetcode.com/problems/remove-element/)
