## First Non Repeating Character

### Description

Write a function that takes in a string of lowercase English-alphabet letters and returns the index of the string's first non-repeating character.

The first non-repeating character is the first character in a string that occurs only once.

If the input string doesn't have any non-repeating characters, your function should return `-1`.

### Sample Input

```
string = "abcdcaf"
```

### Sample Output

```
1
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the length of input string.

```rust
use std::collections::HashMap;

pub struct Solution;

impl Solution {
    pub fn first_non_repeating_character(str: &str) -> i32 {
        let characters: Vec<char> = str.chars().collect();

        let mut chars_map = HashMap::new();

        for (_, ch) in characters.iter().enumerate() {
            let count = chars_map.entry(*ch).or_insert(0);
            *count += 1;
        }

        for (i, ch) in characters.iter().enumerate() {
            let count = chars_map.entry(*ch).or_insert(-1);
            if *count == 1 {
                return i as i32;
            }
        }

        -1
    }
}

fn main() {
    assert_eq!(Solution::first_non_repeating_character("abcdcaf"), 1);
    assert_eq!(
        Solution::first_non_repeating_character(
            "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxy"
        ),
        25
    );
    assert_eq!(Solution::first_non_repeating_character("aabbccddeeff"), -1);
}
```
