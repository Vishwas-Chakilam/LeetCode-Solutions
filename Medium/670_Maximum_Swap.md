# Problem: 670. Maximum Swap

#### Problem Statement:
You are given a non-negative integer represented as a string `num`. You can swap two digits at most once to get the largest possible value. Return the maximum value you can get.

#### Example 1:
```python
Input: num = "2736"
Output: 7236
Explanation: Swap the number 2 and 7.
```

#### Example 2:
```python
Input: num = "9973"
Output: 9973
Explanation: No swap needed since the number is already the largest possible.
```

#### Constraints:
- `num` consists of only digits.
- `1 <= num.length <= 10^4`
- `num` does not contain leading zeros.

---

## Approach 1: Greedy with Position Tracking

### Key Idea:
The goal is to maximize the number by swapping two digits. The largest possible value can be achieved by swapping a digit with a larger one to its right (closer to the end).

1. **Track the last occurrence of each digit**: We create an array `last` that stores the last position of each digit (0-9) in the number. 
2. **Find the first swap**: Traverse the number from left to right, and for each digit, check if there's a larger digit that occurs later in the number. If such a digit is found, swap them to get the largest number.

### Time Complexity:
- **O(n)** where `n` is the number of digits in the input, as we perform two passes over the number (one to track the last occurrence of digits and another to find the best swap).

### Space Complexity:
- **O(1)**, ignoring the space needed for the input since we are only using a fixed array of size 10.

### Python Code:
```python
class Solution:
    def maximumSwap(self, num: int) -> int:
        num = list(str(num))  # Convert the number to a list of characters for easy swapping
        last = {int(x): i for i, x in enumerate(num)}  # Store the last occurrence of each digit
        
        # Traverse through each digit in the number
        for i, digit in enumerate(num):
            # Check if there is a larger digit in the remaining part of the number
            for d in range(9, int(digit), -1):
                if last.get(d, -1) > i:
                    # Swap the current digit with the larger one
                    num[i], num[last[d]] = num[last[d]], num[i]
                    return int(''.join(num))  # Return the result as an integer
        
        return int(''.join(num))  # If no swap is made, return the original number
```

---

## Approach 2: Brute Force (Not Optimal)

### Key Idea:
In this approach, we try every possible swap of two digits in the number and check if the result is larger than the previous maximum. This approach is slower and inefficient for large inputs but easy to understand.

### Time Complexity:
- **O(n^2)**, as we perform a pairwise swap of digits for all possible combinations.

### Space Complexity:
- **O(1)**, since we are modifying the number in place and using only a few variables.

### Python Code:
```python
class Solution:
    def maximumSwap(self, num: int) -> int:
        num = list(str(num))
        max_num = int(''.join(num))  # Initialize max_num with the original number
        
        # Try swapping every pair of digits
        for i in range(len(num)):
            for j in range(i + 1, len(num)):
                # Swap digits at positions i and j
                num[i], num[j] = num[j], num[i]
                
                # Check if the new number is larger than the previous maximum
                max_num = max(max_num, int(''.join(num)))
                
                # Swap back to original order
                num[i], num[j] = num[j], num[i]
        
        return max_num
```

---

## Test Cases:

### Test Case 1:
```python
Input: num = "98368"
Output: 98863
Explanation: Swap 3 and 8 to get the largest number.
```

### Test Case 2:
```python
Input: num = "1993"
Output: 9913
Explanation: Swap the first 1 and 9 to get the largest number.
```

### Test Case 3:
```python
Input: num = "123456"
Output: 623451
Explanation: Swap the first 1 and 6 to maximize the value.
```

### Test Case 4:
```python
Input: num = "987654"
Output: 987654
Explanation: No swap is needed as the number is already the largest possible.
```

---

## Additional Approaches:
- **Dynamic Programming**: You can approach this problem using DP, but it would be overkill since the greedy approach with position tracking is both simpler and more efficient.
  
---
