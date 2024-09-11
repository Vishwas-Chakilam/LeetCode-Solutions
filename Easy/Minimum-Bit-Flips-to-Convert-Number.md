# Minimum Bit Flips to Convert Number

## Description

Given two integers `start` and `goal`, return the **minimum number of bit flips** to convert `start` to `goal`.

A **bit flip** is changing a bit from `1` to `0` or from `0` to `1`.

**Example:**

**Input:**
```python
start = 10
goal = 7
```

**Output:**
```python
3
```

**Explanation:**
- Binary representation of `start = 10`: `1010`
- Binary representation of `goal = 7`: `0111`
- The number of differing bits is `3`.

---

## Solution

### Approach

To solve this problem:
1. **XOR Operation:** Use the XOR (`^`) operator between `start` and `goal`. XOR returns `1` for differing bits and `0` for matching bits.
2. **Count Set Bits:** The number of `1`s in the XOR result represents the number of differing bits, which is equivalent to the number of bit flips required.
3. **Hamming Weight:** Count the number of `1`s (bit flips) in the XOR result.

### Code

```python
def min_bit_flips(start, goal):
    # XOR to find differing bits
    xor_result = start ^ goal
    
    # Count the number of 1's in the XOR result (bit flips)
    return bin(xor_result).count('1')
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the number of bits in the binary representation of `start` and `goal`. In practice, this is O(1) because integers have a fixed number of bits.
- **Space Complexity:** O(1), since no extra space is used beyond the input variables.

---

## Edge Cases

- **Same Numbers:** If `start` and `goal` are the same, the result is `0` because no bit flips are required.
- **Different Lengths in Binary Representation:** The XOR operation handles binary representations of different lengths automatically, so no special handling is required.

---

## Additional Notes

- The use of the XOR operator simplifies the problem to just counting the differing bits.
- This problem can also be understood as finding the Hamming distance between the binary representations of the two numbers.

---

## References

**LeetCode Problem Link:** [Minimum Bit Flips to Convert Number](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/)
