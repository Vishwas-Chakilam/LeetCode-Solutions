# Merge Intervals Problem (LeetCode 56)

## Problem Statement
This repository contains a Python solution for solving the **Merge Intervals** problem from LeetCode.

## Solution Approach

### Problem Description
Given a collection of intervals, merge all overlapping intervals and return an array of non-overlapping intervals that cover all the intervals in the input.

### Approach
- Sort the intervals based on their starting times.
- Iterate through the list and merge overlapping intervals.

## Code Implementation
```python
from typing import List

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        arr = sorted(intervals)
        res = []
        for ele in arr:
            if not res or res[-1][1] < ele[0]:
                res.append(ele)
            else:
                res[-1][1] = max(ele[1], res[-1][1])
        return res
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
print(sol.merge([[1,3],[2,6],[8,10],[15,18]]))  # Example input for merge
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.
