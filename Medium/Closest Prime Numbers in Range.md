# Closest Prime Numbers

## Problem Statement

Given two integers `left` and `right`, find the pair of prime numbers in the range `[left, right]` that have the smallest difference. If there are no such pairs, return `[-1, -1]`.

## Approach

The solution uses the **Sieve of Eratosthenes** to efficiently find all prime numbers in the range `[left, right]`. Then, it iterates through the prime numbers to determine the closest pair.

### Steps:

1. **Use the Sieve of Eratosthenes** to mark all prime numbers up to `right`.
2. **Extract the prime numbers** in the given range `[left, right]`.
3. **Find the closest pair** by iterating through the list of primes.
4. **Return the closest pair** or `[-1, -1]` if there are fewer than two primes.

## Code

```python
from typing import List

class Solution:
    def closestPrimes(self, left: int, right: int) -> List[int]:
        # Step 1: Sieve of Eratosthenes
        p = [True] * (right + 1)
        p[0] = p[1] = False  # 0 and 1 are not prime
        for i in range(2, int((right + 1) ** 0.5) + 1):
            if p[i]:
                for j in range(i * i, right + 1, i):
                    p[j] = False

        # Step 2: Collect prime numbers in the given range
        prime = [i for i in range(left, right + 1) if p[i]]

        # Step 3: Find the closest prime pair
        if len(prime) < 2:
            return [-1, -1]

        n1, n2 = 0, float('inf')
        for i in range(1, len(prime)):
            if (n2 - n1) > (prime[i] - prime[i - 1]):
                n1, n2 = prime[i - 1], prime[i]

        return [n1, n2]
```

## Complexity Analysis

- **Sieve of Eratosthenes:** \(O(N \log \log N)\)
- **Collecting primes:** \(O(N)\)
- **Finding the closest pair:** \(O(N)\)
- **Overall complexity:** \(O(N \log \log N)\)

## Example Usage

```python
sol = Solution()
print(sol.closestPrimes(10, 50))  # Output: [11, 13]
```

## Edge Cases Considered

- When `left` and `right` are very small (e.g., 1 to 10).
- When there are no prime numbers in the range.
- When `left` and `right` are the same number.
- When the range contains only two prime numbers.

## Summary

This solution efficiently finds the closest pair of prime numbers using a combination of the **Sieve of Eratosthenes** and **linear search**. It is optimized for large values of `right` and works within reasonable time constraints. 🚀
