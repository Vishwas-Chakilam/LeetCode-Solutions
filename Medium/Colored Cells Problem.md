# Colored Cells Problem


## Problem Statement

You are given an integer `n`, which represents the number of operations performed on a grid. Starting with a single colored cell, each operation expands the grid by adding a layer of cells around the existing grid. The goal is to determine the total number of colored cells after `n` operations.

### Example
- **Input**: `n = 2`
- **Explanation**:
  - After the 1st operation, there are 5 colored cells.
  - After the 2nd operation, there are 13 colored cells.
- **Output**: `13`

## Solution

The solution uses a mathematical formula to calculate the number of colored cells efficiently. The formula is derived from the pattern observed in the grid expansion:

\[
\text{coloredCells}(n) = 1 + 4 \times \frac{n \times (n - 1)}{2}
\]

### Code Implementation
```python
class Solution:
    def coloredCells(self, n: int) -> int:
        return 1 + 4 * n * (n - 1) // 2
```

### Explanation
- The formula accounts for the initial cell (`1`) and the additional cells added in each layer.
- Each layer adds a ring of cells around the existing grid, and the number of cells in each ring follows a predictable pattern.

## Usage

### Prerequisites
- Python 3.x

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   cd LeetCode-Solutions/Medium
   ```

### Example
```python
solution = Solution()
print(solution.coloredCells(2))  # Output: 13
print(solution.coloredCells(3))  # Output: 25
```

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or submit a pull request.

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/YourFeatureName`).
3. Commit your changes (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/YourFeatureName`).
5. Open a pull request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact
For questions or feedback, feel free to reach out:
- **Name**: Vishwas Chakilam
- **GitHub**: [Vishwas-Chakilam](https://github.com/Vishwas-Chakilam)
- **LeetCode Profile**: [Vishwas-Chakilam](https://leetcode.com/Vishwas-Chakilam/)

---
