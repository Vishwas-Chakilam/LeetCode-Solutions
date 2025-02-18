# LeetCode: Same Tree
### Problem Statement
Given the roots of two binary trees, `p` and `q`, determine if they are the same tree. Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

### Solution Approach
The solution uses a **Breadth-First Search (BFS)** approach with two queues to traverse both trees level by level. The key checks include:
- If both nodes are `None`, continue traversal.
- If one node is `None` or their values differ, return `False`.
- Otherwise, enqueue the left and right children of both nodes.

### Code Implementation
```python
from collections import deque
from typing import Optional

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        q1 = deque([p])
        q2 = deque([q])
        while q1 and q2:
            node1 = q1.popleft()
            node2 = q2.popleft()
            if not node1 and not node2:
                continue
            if not node1 or not node2 or node1.val != node2.val:
                return False
            q1.append(node1.left)
            q1.append(node1.right)
            q2.append(node2.left)
            q2.append(node2.right)
        return not q1 and not q2
```

### Complexity Analysis
- **Time Complexity:** O(N), where N is the number of nodes in the trees, as each node is visited once.
- **Space Complexity:** O(N), due to the queue storage for level-order traversal.

## How to Run
1. Clone this repository:
   ```sh
   git clone https://github.com/Vishwas-Chakilam/LeetCode-Solutions.git
   ```

## Contributions
Feel free to submit pull requests for improvements or additional LeetCode solutions!

## License
This project is licensed under the MIT License.

