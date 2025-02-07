# LeetCode Problem 48: Rotate Image - Python Solution

## Overview

This repository provides a Python solution to **LeetCode problem 48: Rotate Image**. The challenge requires rotating an **n x n** 2D square matrix by **90 degrees clockwise** in-place, meaning the original matrix must be modified directly without allocating additional memory for another matrix.

## Problem Statement

Given an **n x n** 2D matrix representing an image, rotate it by **90 degrees clockwise** in-place.

### Constraints:

- `matrix.length == n`
- `matrix[i].length == n`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

### Example:

#### **Input:**
```python
matrix = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]
```
#### **Output:**
```python
[[7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]]
```

---

## Solution Approach

The in-place rotation is achieved in two steps:

1. **Transpose the Matrix**: Convert rows into columns by swapping elements across the main diagonal (from top-left to bottom-right).
2. **Reverse Each Row**: Reverse the elements of each row to complete the rotation.

This approach ensures an efficient and space-optimized solution.

---

## Python Implementation

```python
from typing import List

class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Rotates a square matrix by 90 degrees clockwise in-place.
        
        Args:
            matrix: A List[List[int]] representing the square matrix.
        
        Returns:
            None: Modifies the matrix in-place.
        """
        n = len(matrix)

        # Step 1: Transpose the matrix
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # Step 2: Reverse each row
        for i in range(n):
            matrix[i].reverse()
```

---

## Code Explanation

### **Step 1: Transposing the Matrix**
- Iterate through the matrix using two nested loops.
- Swap `matrix[i][j]` with `matrix[j][i]`, ensuring elements are flipped across the diagonal.

### **Step 2: Reversing Each Row**
- Iterate through each row and apply the `.reverse()` method to swap elements horizontally.
- This final step completes the 90-degree clockwise rotation.

---

## Complexity Analysis

- **Time Complexity:** **O(n²)** - We iterate over roughly half the elements during transposition and all elements during row reversal.
- **Space Complexity:** **O(1)** - The algorithm operates in-place without requiring extra memory.

---

## Usage

### **1. Clone the Repository**
```sh
git clone <repository_url>
cd <repository_directory>
```

### **2. Run the Code**
```python
from typing import List

matrix = [[1, 2, 3],
          [4, 5, 6],
          [7, 8, 9]]

solution = Solution()
solution.rotate(matrix)
print(matrix)  # Output: [[7, 4, 1], [8, 5, 2], [9, 6, 3]]
```

---

## Additional Notes

- The `typing` module import ensures clarity in function annotations when running the code outside the LeetCode environment.
- This solution is **only valid for square matrices**; it won’t work correctly for non-square matrices.
- The algorithm strictly adheres to the **in-place** constraint, ensuring optimal memory usage.
- The method `reverse()` is used for row flipping, making the implementation concise and efficient.

---

## Enhancements & Best Practices

✅ **Clear Code Structure:** Organized explanation for better readability.
✅ **Comprehensive Example:** Includes input-output examples for clarity.
✅ **Best Practices:** Uses type hints and docstrings for maintainability.
✅ **Git Clone Instructions:** Step-by-step guide for running the solution.
✅ **Efficiency Considerations:** Explanation of time and space complexity.

---

## Contributing

Contributions, bug fixes, and optimizations are welcome! Feel free to fork the repository, create a pull request, or open an issue for discussions.

### **Steps to Contribute:**
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make necessary changes and commit (`git commit -m 'Added new feature'`).
4. Push the changes (`git push origin feature-branch`).
5. Create a pull request.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Happy Coding! 🚀**

