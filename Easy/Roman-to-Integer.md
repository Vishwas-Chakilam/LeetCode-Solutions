# Roman to Integer

## Description

Convert a Roman numeral into an integer. Roman numerals are represented by the following symbols:

- `I` -> 1
- `V` -> 5
- `X` -> 10
- `L` -> 50
- `C` -> 100
- `D` -> 500
- `M` -> 1000

Roman numerals are typically written from largest to smallest from left to right. However, there are special cases where a smaller numeral precedes a larger one to indicate subtraction, such as:

- `IV` = 4
- `IX` = 9
- `XL` = 40
- `XC` = 90
- `CD` = 400
- `CM` = 900

**Example:**

**Input:**
```python
s = "MCMXCIV"
```

**Output:**
```python
1994
```

**Explanation:**
The Roman numeral `MCMXCIV` represents the integer `1994`, where:
- `M` = 1000
- `CM` = 900
- `XC` = 90
- `IV` = 4

---

## Solution

### Approach

To convert a Roman numeral to an integer, process the string from left to right:

1. **Mapping Roman Numerals to Values:** Create a dictionary to map each Roman numeral to its corresponding value.
2. **Iterate Over the String:** Traverse the string character by character.
   - If the current numeral is smaller than the next numeral, subtract its value.
   - Otherwise, add its value.

### Code

```python
def roman_to_int(s):
    # Map Roman numerals to their integer values
    roman_map = {
        'I': 1, 'V': 5, 'X': 10, 'L': 50,
        'C': 100, 'D': 500, 'M': 1000
    }
    
    total = 0
    prev_value = 0

    # Traverse the string from left to right
    for char in s:
        current_value = roman_map[char]
        
        # If the current value is greater than the previous, subtract twice the previous value
        if current_value > prev_value:
            total += current_value - 2 * prev_value
        else:
            total += current_value
        
        # Update the previous value
        prev_value = current_value
    
    return total
```

### Complexity Analysis

- **Time Complexity:** O(n), where `n` is the length of the Roman numeral string. Each character is processed once.
- **Space Complexity:** O(1), since we use a fixed number of variables and the dictionary has a constant size.

---

## Edge Cases

- **Empty String:** Handle cases where the input is an empty string.
- **Special Cases:** Ensure the function correctly handles subtractions such as `IV`, `IX`, `XL`, etc.
- **Single Character:** Handle cases where the Roman numeral consists of a single character, e.g., `I`, `V`, `X`.

---

## Additional Notes

- The solution leverages the fact that Roman numerals follow specific patterns, allowing us to handle both addition and subtraction efficiently.
- This approach ensures that all possible valid Roman numeral strings are handled correctly.

---

## References

**LeetCode Problem Link:** [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

---
