# Contains Nearby Duplicate Problem (LeetCode 219)

## Problem Statement
This repository contains a Python solution for solving the **Contains Duplicate II** problem from LeetCode.

## Solution Approach

### Problem Description
Given an integer array `nums` and an integer `k`, return `true` if there exist two distinct indices `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`. Otherwise, return `false`.

### Approach
- Use a dictionary to store the last seen index of each element.
- Iterate through the list, checking if the current number exists in the dictionary.
- If the absolute difference between the indices is `≤ k`, return `True`.
- Otherwise, update the dictionary with the current index.
- If no such pair is found, return `False`.

## Code Implementation
```python
from typing import List
import collections

class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        d = collections.defaultdict()
        for i in range(len(nums)):
            if nums[i] not in d:
                d[nums[i]] = i
            else:
                if abs(i - d[nums[i]]) <= k:
                    return True
                d[nums[i]] = i
        return False
```

## Usage
1. Clone this repository:
   ```sh
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   ```
2. Run the function in a Python environment.

## Example
```python
sol = Solution()
print(sol.containsNearbyDuplicate([1,2,3,1], 3))  # Example input
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.
