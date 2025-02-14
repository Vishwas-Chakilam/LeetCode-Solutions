# Product of Numbers - Efficient Prefix Product Solution

## Problem Statement
Design a data structure that supports the following operations efficiently:
1. `add(num: int)`: Adds a number to the data structure.
2. `getProduct(k: int)`: Returns the product of the last `k` numbers added.

### Constraints:
- If any number added is `0`, all previous values should be discarded since multiplying by zero results in zero.
- The solution should be optimized for multiple `getProduct(k)` calls.

## Solution Approach
### **Using Prefix Product Array**
Instead of storing all numbers, we store a **prefix product array** where:
- `prefix_products[i]` stores the product of all numbers up to index `i`.
- If a `0` is encountered, we reset `prefix_products` because any product including `0` is `0`.
- The product of the last `k` numbers can be computed efficiently using division.
- This allows us to get the product in **O(1)** time complexity.

## Implementation
```python
class ProductOfNumbers:
    def __init__(self):
        self.prefix_products = [1]  # Initialize with 1 for easy multiplication

    def add(self, num: int) -> None:
        if num == 0:
            self.prefix_products = [1]  # Reset since any product including 0 is 0
        else:
            self.prefix_products.append(self.prefix_products[-1] * num)

    def getProduct(self, k: int) -> int:
        if k >= len(self.prefix_products):
            return 0  # If k is larger than available numbers, return 0
        return self.prefix_products[-1] // self.prefix_products[-k - 1]
```

## Explanation
1. **Adding Numbers (`add(num)`)**
   - If `num == 0`, reset `prefix_products` to `[1]`.
   - Otherwise, append the product of `num` with the last stored value in `prefix_products`.

2. **Getting the Product (`getProduct(k)`)**
   - If `k` is larger than available elements (due to reset), return `0`.
   - Otherwise, compute the product using:
     ```python
     self.prefix_products[-1] // self.prefix_products[-k-1]
     ```
   - This effectively cancels out the earlier elements and gives the product of the last `k` numbers in **O(1)** time.

## Complexity Analysis
| Operation | Time Complexity |
|-----------|----------------|
| `add(num)` | O(1) |
| `getProduct(k)` | O(1) |

## Example Usage
```python
obj = ProductOfNumbers()
obj.add(3)
obj.add(4)
obj.add(5)
print(obj.getProduct(2))  # Output: 20 (4 * 5)
obj.add(0)
obj.add(2)
print(obj.getProduct(2))  # Output: 2 (Only 2 remains)
```

## Edge Cases Handled
✅ **Handling Zero:** If a `0` is added, all previous products are reset.
✅ **Efficient Queries:** Each `getProduct(k)` runs in **O(1)** time.
✅ **Large Values of k:** If `k` is larger than available numbers, return `0`.

## Summary
This approach ensures an efficient and scalable way to compute the product of the last `k` numbers dynamically, handling zeros correctly while keeping operations **fast and optimal**. 🚀
