# 641. Design Circular Deque

## 1. Problem Statement

Design your implementation of the circular double-ended queue (deque).

Your implementation should support the following operations:

1. `MyCircularDeque(k)` Initializes the deque with a maximum size `k`.
2. `insertFront()`: Adds an item at the front of the deque. Return `true` if the operation is successful, `false` otherwise.
3. `insertLast()`: Adds an item at the rear of the deque. Return `true` if the operation is successful, `false` otherwise.
4. `deleteFront()`: Deletes an item from the front of the deque. Return `true` if the operation is successful, `false` otherwise.
5. `deleteLast()`: Deletes an item from the rear of the deque. Return `true` if the operation is successful, `false` otherwise.
6. `getFront()`: Gets the front item from the deque. If the deque is empty, return `-1`.
7. `getRear()`: Gets the last item from the deque. If the deque is empty, return `-1`.
8. `isEmpty()`: Checks whether the deque is empty or not.
9. `isFull()`: Checks whether the deque is full or not.

### Example:
```python
myCircularDeque = MyCircularDeque(3); // set the size to be 3
myCircularDeque.insertLast(1);  // return True
myCircularDeque.insertLast(2);  // return True
myCircularDeque.insertFront(3); // return True
myCircularDeque.insertFront(4); // return False, the deque is full
myCircularDeque.getRear();      // return 2
myCircularDeque.isFull();       // return True
myCircularDeque.deleteLast();   // return True
myCircularDeque.insertFront(4); // return True
myCircularDeque.getFront();     // return 4
```

### Constraints:
- All values of `insertFront`, `insertLast`, `deleteFront`, and `deleteLast` will be in the range `[-1000, 1000]`.
- The number of calls to these operations will not exceed `2000`.
- `0 <= k <= 1000`.

---

## 2. Test Cases

### Test Case 1:
```python
deque = MyCircularDeque(3)
assert deque.insertLast(1) == True
assert deque.insertLast(2) == True
assert deque.insertFront(3) == True
assert deque.insertFront(4) == False
assert deque.getRear() == 2
assert deque.isFull() == True
assert deque.deleteLast() == True
assert deque.insertFront(4) == True
assert deque.getFront() == 4
```

### Test Case 2:
```python
deque = MyCircularDeque(5)
assert deque.insertLast(9) == True
assert deque.insertFront(7) == True
assert deque.getFront() == 7
assert deque.getRear() == 9
assert deque.deleteFront() == True
assert deque.isEmpty() == False
assert deque.isFull() == False
```

---

## 3. Approach

### 3a. Brute Force Approach

To implement the circular deque, we can use a list of fixed size `k` and maintain two pointers, `front` and `rear`. These pointers help track the current positions in the deque, and all operations are handled with circular indexing.

#### Time Complexity:
- **Insertion and Deletion**: O(1) because operations only involve updating pointers and values.
- **Get Front/Rear**: O(1).
  
#### Space Complexity:
- **Space**: O(k) where `k` is the size of the deque.

### Code Implementation (Python):
```python
class MyCircularDeque:

    def __init__(self, k: int):
        self.k = k
        self.deque = [-1] * k
        self.front = 0
        self.rear = 0
        self.size = 0

    def insertFront(self, value: int) -> bool:
        if self.isFull():
            return False
        self.front = (self.front - 1) % self.k
        self.deque[self.front] = value
        self.size += 1
        return True

    def insertLast(self, value: int) -> bool:
        if self.isFull():
            return False
        self.deque[self.rear] = value
        self.rear = (self.rear + 1) % self.k
        self.size += 1
        return True

    def deleteFront(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.k
        self.size -= 1
        return True

    def deleteLast(self) -> bool:
        if self.isEmpty():
            return False
        self.rear = (self.rear - 1 + self.k) % self.k
        self.size -= 1
        return True

    def getFront(self) -> int:
        if self.isEmpty():
            return -1
        return self.deque[self.front]

    def getRear(self) -> int:
        if self.isEmpty():
            return -1
        return self.deque[(self.rear - 1 + self.k) % self.k]

    def isEmpty(self) -> bool:
        return self.size == 0

    def isFull(self) -> bool:
        return self.size == self.k
```

---

## 4. Edge Cases

- Inserting into an already full deque should return `false`.
- Deleting from an empty deque should return `false`.
- Accessing the front or rear of an empty deque should return `-1`.
- Deque with size 0 should be handled correctly, i.e., always returning empty and not allowing any insertions.

---

## 5. References

- **Circular Queue/Deque Concepts**: [GeeksforGeeks - Circular Queue](https://www.geeksforgeeks.org/circular-queue-set-1-introduction-array-implementation/)
- **LeetCode Problem**: [Design Circular Deque](https://leetcode.com/problems/design-circular-deque/)
