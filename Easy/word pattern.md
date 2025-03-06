# Word Pattern Matching


## Problem Statement

Given a `pattern` and a string `s`, determine if `s` follows the same pattern. Here, "follow" means a full match, such that there is a bijection between a letter in `pattern` and a non-empty word in `s`.

### Example
- **Input**: `pattern = "abba"`, `s = "dog cat cat fish"`
- **Output**: `false`

## How It Works

The solution uses two hash maps to maintain a bijective mapping between characters in the pattern and words in the string. It ensures that:
1. Each character in the pattern maps to exactly one word in the string.
2. Each word in the string maps to exactly one character in the pattern.

If any mismatch is found during the iteration, the function returns `false`. Otherwise, it returns `true`.

## Usage

### Prerequisites
- Python 3.x

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/vishwas-Chakilam/LeetCode-Solutions.git
   ```
### Example Code
```python
def wordPattern(pattern: str, s: str) -> bool:
    words = s.split()
    if len(pattern) != len(words):
        return False
    
    char_to_word = {}
    word_to_char = {}
    
    for char, word in zip(pattern, words):
        if char in char_to_word:
            if char_to_word[char] != word:
                return False
        else:
            if word in word_to_char:
                return False
            char_to_word[char] = word
            word_to_char[word] = char
    
    return True

# Test case
pattern = "abba"
s = "dog cat cat fish"
print(wordPattern(pattern, s))  # Output: False
```

## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or submit a pull request.

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/YourFeatureName`).
3. Commit your changes (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/YourFeatureName`).
5. Open a pull request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact
For questions or feedback, feel free to reach out:
- **Vishwas Chakilam**
- **Email**: work.Vishwas1@gmail.com
- **GitHub**: [vishwas-Chakilam](https://github.com/vishwas-Chakilam)

---

