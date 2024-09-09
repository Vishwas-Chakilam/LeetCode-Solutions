# Add Two Numbers

## Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

**Input:**
```python
l1 = [2, 4, 3]
l2 = [5, 6, 4]
```

**Output:**
```python
[7, 0, 8]
```

**Explanation:**
The number represented by `l1` is 342 and the number represented by `l2` is 465. Adding these two gives 807, which is represented as `[7, 0, 8]`.

---

## Solution

### Approach

To solve this problem, we need to simulate the addition of two numbers digit by digit. We traverse both linked lists, add the corresponding digits along with any carry from the previous addition. If the sum exceeds 10, we handle the carry for the next digit.

### Code

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def add_two_numbers(l1, l2):
    dummy = ListNode(0)  # Placeholder for the result list
    current = dummy
    carry = 0
    
    while l1 or l2 or carry:
        # Get the values from the current nodes, or 0 if the node is None
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0
        
        # Calculate the sum and carry
        total = val1 + val2 + carry
        carry = total // 10
        digit = total % 10
        
        # Create a new node with the digit and attach it to the result list
        current.next = ListNode(digit)
        current = current.next
        
        # Move to the next nodes in the lists
        if l1:
            l1 = l1.next
        if l2:
            l2 = l2.next
    
    return dummy.next
```

### Complexity Analysis

- **Time Complexity:** O(max(m, n)), where m and n are the lengths of the two linked lists. We need to traverse both lists entirely.
- **Space Complexity:** O(max(m, n)), as we need to create a new linked list to store the result.

---

## Edge Cases

- **One List is Empty:** Handle cases where one of the lists is empty by treating its digits as 0.
- **Different Lengths:** The approach handles lists of different lengths by treating missing digits as 0.

---

## Additional Notes

- Ensure that the linked list nodes are properly handled to avoid errors during traversal and addition.
- This solution works for lists of varying lengths and ensures that carry is handled correctly throughout the process.

---

## References

**LeetCode Problem Link:** [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
