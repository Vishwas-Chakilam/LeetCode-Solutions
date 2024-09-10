# 3Sum

## Description

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that:
- `i != j`, 
- `i != k`, 
- `j != k`, and
- `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example:**

**Input:**
```python
nums = [-1, 0, 1, 2, -1, -4]
```

**Output:**
```python
[[-1, -1, 2], [-1, 0, 1]]
```

**Explanation:**
- The triplets that sum up to zero are `[-1, -1, 2]` and `[-1, 0, 1]`.
- Notice that the solution set does not contain duplicate triplets.

---

## Solution

### Approach

To solve the 3Sum problem:
1. **Sort the Array:** First, sort the array to make it easier to avoid duplicates and to use the two-pointer approach.
2. **Iterate Through the Array:** For each element `nums[i]`, use two pointers to find the other two elements (`nums[j]` and `nums[k]`) such that `nums[i] + nums[j] + nums[k] == 0`.
   - Fix the first element `nums[i]`.
   - Use two pointers: one starting from the next element (`j = i + 1`) and another from the end (`k = len(nums) - 1`).
   - Adjust the pointers based on the sum of `nums[i] + nums[j] + nums[k]`.

### Code

```python
def three_sum(nums):
    # Sort the array
    nums.sort()
    res = []
    
    for i in range(len(nums)):
        # Avoid duplicates for the first element
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        
        # Initialize two pointers
        left, right = i + 1, len(nums) - 1
        
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            
            if total == 0:
                res.append([nums[i], nums[left], nums[right]])
                
                # Avoid duplicates for the second element
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                
                # Avoid duplicates for the third element
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                
                left += 1
                right -= 1
            
            # If sum is less than zero, move the left pointer to the right
            elif total < 0:
                left += 1
            
            # If sum is greater than zero, move the right pointer to the left
            else:
                right -= 1
    
    return res
```

### Complexity Analysis

- **Time Complexity:** O(n²), where `n` is the number of elements in the array. Sorting the array takes O(n * log n), and we use a two-pointer approach for each element, which takes O(n²) in total.
- **Space Complexity:** O(1), not counting the output array. Only a few extra variables are used.

---

## Edge Cases

- **Less than 3 elements:** If the input array has fewer than 3 elements, return an empty list.
- **All zeros:** If all elements are zero, ensure the function returns only one triplet `[0, 0, 0]`.
- **No triplets:** If no valid triplets exist that sum up to zero, return an empty list.

---

## Additional Notes

- Sorting the array simplifies the process of avoiding duplicates and applying the two-pointer technique.
- This approach ensures that each triplet is unique, even if the input array contains duplicate elements.

---

## References

**LeetCode Problem Link:** [3Sum](https://leetcode.com/problems/3sum/)

---
