# Median of Two Sorted Arrays

## Description

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be O(log (m+n)).

**Example:**

**Input:**
```python
nums1 = [1, 3]
nums2 = [2]
```

**Output:**
```python
2.0
```

**Explanation:**
The median is the middle value of the merged array `[1, 2, 3]`, which is `2`.

---

## Solution

### Approach

To find the median of two sorted arrays with the required time complexity, we use a binary search approach. We perform a binary search on the smaller of the two arrays to partition both arrays such that all elements in the left partition are less than or equal to all elements in the right partition.

The steps are:

1. **Partition Arrays:** Partition both arrays into two halves such that all elements in the left halves are less than all elements in the right halves.
2. **Check Valid Partition:** Ensure the maximum of the left partition is less than or equal to the minimum of the right partition.
3. **Calculate Median:** Depending on whether the total number of elements is odd or even, calculate the median based on the maximum of the left partition and the minimum of the right partition.

### Code

```python
def findMedianSortedArrays(nums1, nums2):
    # Ensure nums1 is the smaller array
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1

    x, y = len(nums1), len(nums2)
    low, high = 0, x

    while low <= high:
        partitionX = (low + high) // 2
        partitionY = (x + y + 1) // 2 - partitionX

        maxX = float('-inf') if partitionX == 0 else nums1[partitionX - 1]
        minX = float('inf') if partitionX == x else nums1[partitionX]
        maxY = float('-inf') if partitionY == 0 else nums2[partitionY - 1]
        minY = float('inf') if partitionY == y else nums2[partitionY]

        if maxX <= minY and maxY <= minX:
            if (x + y) % 2 == 0:
                return (max(maxX, maxY) + min(minX, minY)) / 2.0
            else:
                return max(maxX, maxY)
        elif maxX > minY:
            high = partitionX - 1
        else:
            low = partitionX + 1
```

### Complexity Analysis

- **Time Complexity:** O(log(min(m, n))), where m and n are the sizes of the two arrays. This is because we perform binary search on the smaller array.
- **Space Complexity:** O(1), as we are using only a few extra variables.

---

## Edge Cases

- **Arrays with Different Sizes:** The algorithm handles cases where the arrays have different lengths.
- **Empty Arrays:** The function assumes at least one of the arrays is non-empty, as per the problem constraints.

---

## Additional Notes

- The solution relies on binary search for partitioning, which ensures optimal time complexity.
- Handling edge cases and ensuring the correctness of the partitioning logic is crucial for accurate median calculation.

---

## References

**LeetCode Problem Link:** [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

---
