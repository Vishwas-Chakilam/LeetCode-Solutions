# Has Same Digits

## Problem Statement
This repository contains a Python solution for checking whether a given numeric string reduces to a two-digit number where both digits are the same through iterative pairwise summation.

## Solution Approach
The function `hasSameDigits(s: str) -> bool` follows these steps:
1. Iteratively sum adjacent digits in the string.
2. Take the sum modulo 10 and create a new string.
3. Repeat until the string length is reduced to 2.
4. Check if both digits in the final string are the same.

## Code Implementation
```python
class Solution:
    def hasSameDigits(self, s: str) -> bool:
        while len(s) > 2:
            res = ''
            for i in range(len(s) - 1):
                rem = (int(s[i]) + int(s[i + 1])) % 10
                res += str(rem)
            s = res
        return s[0] == s[1]
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
print(sol.hasSameDigits("12345"))  # Example input
```

## Contributions
Feel free to submit issues and pull requests to improve the implementation!

## License
This project is open-source and available under the MIT License.

