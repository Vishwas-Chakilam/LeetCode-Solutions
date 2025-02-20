# Evaluate Division

## Problem Statement
This repository contains a Python solution for the problem of evaluating division using a graph-based approach. Given a list of equations representing relationships between variables and their corresponding values, this solution efficiently answers queries regarding these relationships.

## Approach
The solution uses **Depth First Search (DFS)** and a **graph representation** to compute division queries efficiently.

### Steps:
1. **Graph Construction**:
   - A graph is built using a dictionary where each variable maps to another dictionary containing its neighbors and corresponding weight (i.e., division value).
   - If `A / B = Value`, then `B / A = 1 / Value` is also stored.

2. **Depth First Search (DFS)**:
   - DFS is employed to search for a path between the queried variables.
   - If a path exists, the product of the weights along the path is computed.
   - If no path exists, `-1.0` is returned.

## Code
```python
from collections import defaultdict
from typing import List

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        graph = defaultdict(dict)
        
        # Build graph
        for (A, B), Value in zip(equations, values):
            graph[A][B] = Value
            graph[B][A] = 1 / Value
        
        def dfs(start, end, visited):
            if start not in graph or end not in graph:
                return -1.0
            if start == end:
                return 1.0
            
            visited.add(start)
            for neighbour, weight in graph[start].items():
                if neighbour not in visited:
                    result = dfs(neighbour, end, visited)
                    if result != -1.0:
                        return weight * result
            return -1.0
        
        results = []
        for X, Y in queries:
            results.append(dfs(X, Y, set()))
        
        return results
```

## Complexity Analysis
- **Graph Construction**: O(E) where E is the number of equations.
- **DFS Traversal**: O(Q * V) in the worst case, where Q is the number of queries and V is the number of unique variables.

## Example Usage
```python
sol = Solution()
equations = [["a", "b"], ["b", "c"]]
values = [2.0, 3.0]
queries = [["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"]]
print(sol.calcEquation(equations, values, queries))
```

## Expected Output
```
[6.0, 0.5, -1.0, 1.0, -1.0]
```

## Contributing
Feel free to open an issue or submit a pull request if you have improvements or find bugs!

## License
This project is licensed under the MIT License.

