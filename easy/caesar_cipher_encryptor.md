## Caesar Cipher Encryptor

### Description

Given a non-empty string of lowercase letters and a non-negative integer representing a key, write a function that returns a new string obtained by shifting every letter in the input string by k positions in the alphabet, where k is the key.

Note that letters should "wrap" around the alphabet; in other words, the letter `z` shifted by one returns the letter `a`.

### Sample Input

```
string = "xyz",
key = 2
```

### Sample Output

```
"zab"
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the length of the input string.

```rust
pub struct Solution;

impl Solution {
    pub fn caesar_cipher_encryptor(str: &str, key: i32) -> String {
        let str: Vec<char> = str.chars().collect();
        let key = key % 26;
        let mut new_str = String::from("");
        let alphabet = vec![
            'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q',
            'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
        ];

        for (_, s) in str.iter().enumerate() {
            let c = Solution::get_new_letter(s, &key, &alphabet);
            new_str.push(c);
        }

        new_str
    }

    fn get_new_letter(s: &char, key: &i32, alphabet: &Vec<char>) -> char {
        let new_letter_code = alphabet.iter().position(|r| r == s).unwrap() as i32 + key;

        if new_letter_code < 26 {
            return alphabet[new_letter_code as usize];
        } else {
            return alphabet[new_letter_code as usize % 26];
        }
    }
}

fn main() {
    assert_eq!(
        Solution::caesar_cipher_encryptor("xyz", 2),
        String::from("zab")
    );
    assert_eq!(
        Solution::caesar_cipher_encryptor("mvklahvjcnbwqvtutmfafkwiuagjkzmzwgf", 7),
        String::from("tcrshocqjuidxcabatmhmrdpbhnqrgtgdnm")
    );
    assert_eq!(
        Solution::caesar_cipher_encryptor(
            "kjwmntauvjjnmsagwgawkagfuaugjhawgnawgjhawjgawbfawghesh",
            15
        ),
        String::from("zylbcipjkyycbhpvlvplzpvujpjvywplvcplvywplyvplquplvwthw")
    );
}
```
