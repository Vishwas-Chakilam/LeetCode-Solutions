# Balanced Binary Tree

## Problem Description
The **Balanced Binary Tree** problem is a classic algorithm challenge where we determine whether a given binary tree is height-balanced.  

### Definition of a Balanced Binary Tree:
A binary tree is height-balanced if:
1. The left and right subtrees of every node differ in height by no more than `1`.
2. Both the left and right subtrees are also balanced.

---

## Problem Statement
Given the `root` of a binary tree, return `true` if the tree is height-balanced, otherwise return `false`.

---

## Example

### Input:
```
       3
      / \
     9  20
        /  \
       15   7
```

### Output:
```
true
```

---

### Input:
```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

### Output:
```
false
```

---

## Solution Explanation

### Approach
We use recursion to check both:
1. The height of the left and right subtrees.
2. Whether each subtree is balanced.  

Instead of calculating the height of subtrees repeatedly, we combine the height calculation and balance check into a single recursive function for efficiency.  

### Algorithm:
1. Define a helper function `check_height(node)`:
   - If the node is `None`, return `0` (an empty tree is balanced).
   - Recursively compute the heights of the left and right subtrees.
   - If either subtree is unbalanced (returns `-1`), propagate `-1` upwards.
   - If the difference in height between the left and right subtrees is greater than `1`, return `-1` (unbalanced).
   - Otherwise, return the height of the current subtree as `max(left_height, right_height) + 1`.
2. Use the helper function in the main method to determine if the tree is balanced.

---

## Code

### Python Implementation

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def check_height(node):
            if not node:
                return 0  # Base case: height of an empty tree is 0
            
            # Check heights of left and right subtrees
            left_height = check_height(node.left)
            right_height = check_height(node.right)
            
            # If either subtree is unbalanced, propagate -1 upwards
            if left_height == -1 or right_height == -1:
                return -1
            
            # If the current node is unbalanced, return -1
            if abs(left_height - right_height) > 1:
                return -1
            
            # Return the height of the current subtree
            return max(left_height, right_height) + 1
        
        # If the helper function returns -1, the tree is not balanced
        return check_height(root) != -1
```

---

## Example Walkthrough

### Input:
```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

#### Walkthrough:
1. Compute the height of the left subtree rooted at `2`:
   - Subtree rooted at `3` → Height of `4` = `1`.
   - Subtree rooted at `3` → Height of `4` = `1`.
   - Height of subtree rooted at `2` = `1 + max(1, 1) = 2`.
2. Compute the height of the right subtree rooted at `2` → Height = `0` (leaf).
3. The difference in height between the left and right subtrees = `2 - 0 = 2`.
4. Since the difference exceeds `1`, the tree is **not balanced**.

### Output:
```
false
```

---

## Complexity Analysis

### Time Complexity:
- **O(n)**: Each node is visited once to calculate its height and balance status.

### Space Complexity:
- **O(h)**: The recursion stack uses space proportional to the height of the tree, which can be `O(n)` in the worst case for a skewed tree or `O(log n)` for a balanced tree.

---

## Alternative Approaches
### Iterative Solution:
Although recursion is the most intuitive approach, an iterative approach using a stack can also solve the problem. However, it is generally more complex to implement.

---

## Resources
- [LeetCode Problem #110 - Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)
- [Binary Tree Basics](https://en.wikipedia.org/wiki/Binary_tree)

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

## Author
[Vishwas Chakilam](https://github.com/Vishwas-Chakilam)  
Transforming Data into Actionable Insights and Innovative Solutions 🚀

---
