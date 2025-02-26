# Insert Interval Problem (LeetCode 57)

## Problem Statement
This repository contains a Python solution for solving the **Insert Interval** problem from LeetCode, which involves inserting a new interval into an existing list of intervals and merging overlapping intervals.

## Solution Approach

### Problem Description
You are given an array of non-overlapping intervals, sorted in ascending order, and a new interval to insert. The goal is to merge overlapping intervals and return the resulting list of disjoint intervals.

### Approach
- Append the new interval to the list.
- Sort the list based on the start times.
- Iterate through the list and merge overlapping intervals.

## Code Implementation
```python
from typing import List

class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        intervals.append(newInterval)
        arr = sorted(intervals)
        res = []
        for i in arr:
            if not res or res[-1][1] < i[0]:
                res.append(i)
            else:
                res[-1][1] = max(i[1], res[-1][1])
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
print(sol.insert([[1,3],[6,9]], [2,5]))  # Example input
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.
