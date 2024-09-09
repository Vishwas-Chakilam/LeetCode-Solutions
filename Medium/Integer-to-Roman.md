# Integer to Roman

## Description

Convert an integer to its Roman numeral representation. Roman numerals are represented by the following symbols:

- `I` -> 1
- `V` -> 5
- `X` -> 10
- `L` -> 50
- `C` -> 100
- `D` -> 500
- `M` -> 1000

For example, the integer `1994` is represented as `MCMXCIV`.

**Example:**

**Input:**
```python
num = 1994
```

**Output:**
```python
"MCMXCIV"
```

**Explanation:**
The integer `1994` is represented as `MCMXCIV` in Roman numerals, where:
- `M` = 1000
- `CM` = 900
- `XC` = 90
- `IV` = 4

---

## Solution

### Approach

To convert an integer to a Roman numeral, use a greedy algorithm that subtracts the largest possible values and appends the corresponding Roman numeral symbols.

1. **Define Mappings:** Create a list of tuples where each tuple contains a Roman numeral and its corresponding integer value.
2. **Greedy Conversion:** Iterate through the list, subtracting the values from the integer and appending the symbols to the result string.

### Code

```python
def int_to_roman(num):
    # Define the mappings from integers to Roman numerals
    val = [
        1000, 900, 500, 400,
        100, 90, 50, 40,
        10, 9, 5, 4,
        1
    ]
    syms = [
        "M", "CM", "D", "CD",
        "C", "XC", "L", "XL",
        "X", "IX", "V", "IV",
        "I"
    ]
    
    roman_num = ''
    i = 0
    
    # Process each value and its corresponding symbol
    while num > 0:
        for _ in range(num // val[i]):
            roman_num += syms[i]
            num -= val[i]
        i += 1
    
    return roman_num
```

### Complexity Analysis

- **Time Complexity:** O(1), since the algorithm processes a fixed number of Roman numeral symbols.
- **Space Complexity:** O(1), as the space used does not depend on the input size but on the fixed size of the Roman numeral mappings.

---

## Edge Cases

- **Boundary Values:** Ensure correct conversion for the smallest (1) and largest (3999) numbers within the valid range for Roman numerals.
- **Valid Input Range:** The algorithm assumes the input is between 1 and 3999, inclusive.

---

## Additional Notes

- This solution is efficient due to the fixed number of Roman numeral symbols and direct subtraction.
- The greedy algorithm ensures that the conversion is performed with minimal iterations and maximal efficiency.

---

## References

**LeetCode Problem Link:** [Integer to Roman](https://leetcode.com/problems/integer-to-roman/)

---
