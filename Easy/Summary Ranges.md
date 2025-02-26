# Summary Ranges Problem (LeetCode 228)

## Problem Statement
This repository contains a Python solution for solving the **Summary Ranges** problem from LeetCode.

## Solution Approach

### Problem Description
Given a sorted unique integer array `nums`, return the smallest sorted list of ranges that cover all the numbers in the array exactly. Each range `[a, b]` is represented as:
- `"a"` if `a == b`
- `"a->b"` if `a < b`

### Approach
- Initialize an empty list `result` to store the ranges.
- Track the start of the current range.
- Iterate through the list and determine where a new range starts.
- Append single numbers or range strings to the result list.

## Code Implementation
```python
class Solution:
    def summaryRanges(self, nums):
        result = []
        if not nums:
            return result

        start = nums[0]
        for i in range(1, len(nums) + 1):
            if i == len(nums) or nums[i] != nums[i - 1] + 1:
                if start == nums[i - 1]:
                    result.append(str(start))
                else:
                    result.append(f"{start}->{nums[i - 1]}")
                if i < len(nums):
                    start = nums[i]
        return result
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
print(sol.summaryRanges([0,1,2,4,5,7]))  # Output: ['0->2', '4->5', '7']
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.
