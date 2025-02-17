# Number of Employees Who Met the Target

This repository contains a Python solution to count the number of employees who met or exceeded a given target number of working hours.

## Problem Statement

Given a list of working hours for employees and a target number of hours, the function determines how many employees met or exceeded the target.

## Implementation

The solution is implemented in Python using list comprehension.

### Code:
```python
from typing import List

class Solution:
    def numberOfEmployeesWhoMetTarget(self, hours: List[int], target: int) -> int:
        return len([x for x in hours if x >= target])
```

## Usage

1. Clone the repository:
   ```sh
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   ```

## Example
```python
solution = Solution()
print(solution.numberOfEmployeesWhoMetTarget([8, 6, 10, 5, 9], 7))  # Output: 3
```

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

## License

This project is licensed under the MIT License.

---

⭐️ Don't forget to **star** the repository if you find it useful!
