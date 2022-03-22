## Palindrome Check

### Description

Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.

A palindrome is defined as a string that's written the same forward and backward. Note that single-character strings are palindromes.

### Sample Input

```
string = "abcdcba"
```

### Sample Output

```
true // it's written the same forward and backward
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the length of the input string.

```rust
pub struct Solution;

impl Solution {
    pub fn is_palindrome(str: &str) -> bool {
        let str: Vec<char> = str.chars().collect();

        let mut left_index: usize = 0;
        let mut right_index: usize = str.len() - 1;

        while left_index < right_index {
            if str[left_index].to_ascii_lowercase() != str[right_index].to_ascii_lowercase() {
                return false;
            }

            left_index += 1;
            right_index -= 1;
        }

        true
    }
}

fn main() {
    assert_eq!(Solution::is_palindrome("abcdcba"), true);
    assert_eq!(Solution::is_palindrome("abcdefghhgfedcba"), true);
    assert_eq!(Solution::is_palindrome("abcdefghihgfeddcba"), false);
}
```
