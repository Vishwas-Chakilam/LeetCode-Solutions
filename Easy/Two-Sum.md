# Two Sum

## Description

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**

**Input:**
```python
nums = [2, 7, 11, 15]
target = 9
```

**Output:**
```python
[0, 1]
```

**Explanation:**
Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.

---

## Solution

### Approach

A common approach to solve this problem efficiently is to use a hash map (dictionary) to keep track of the indices of the elements as you iterate through the array. This allows you to check in constant time if the complement of the current element (i.e., `target - nums[i]`) exists in the hash map.

### Code

```python
def two_sum(nums, target):
    # Dictionary to store the complement and its index
    num_map = {}
    
    for index, num in enumerate(nums):
        # Calculate complement
        complement = target - num
        
        # Check if complement is already in the dictionary
        if complement in num_map:
            return [num_map[complement], index]
        
        # Store the index of the current number
        num_map[num] = index
    
    # If no solution is found, though the problem guarantees exactly one solution
    return []
```

### Complexity Analysis

- **Time Complexity:** O(n), where n is the number of elements in the `nums` array. Each element is processed once.
- **Space Complexity:** O(n), as we are storing elements in the hash map.

---

## Edge Cases

- **Single Pair Solution:** The problem guarantees exactly one solution, so no need to handle cases with no solutions.
- **Duplicate Elements:** Ensure that the indices returned are for different elements.

---

## Additional Notes

- This solution is efficient and utilizes a hash map to achieve linear time complexity. 
- Alternative approaches, like the brute-force method, involve nested loops and have O(n^2) time complexity.

---
## References

**LeetCode Problem Link:** [Two Sum](https://leetcode.com/problems/two-sum/)

