## Generate Document

### Description

You're given a string of available characters and a string representing a document that you need to generate. Write a function that determines if you can generate the document using the available characters. If you can generate the document, your function should return `true`; otherwise, it should return `false`.

You're only able to generate the document if the frequency of unique characters in the characters string is greater than or equal to the frequency of unique characters in the document string. For example, if you're given `characters = "abcabc"` and `document = "aabbccc"` you `cannot` generate the document because you're missing one `c`.

The document that you need to create may contain any characters, including special characters, capital letters, numbers, and spaces.

Note: you can always generate the empty string (`""`).

### Sample Input

```
characters = "Bste!hetsi ogEAxpelrt x "
document = "AlgoExpert is the Best!"
```

### Sample Output

```
true
```

## Solution

Time and space complexity:

- time **O(n + m)**
- space **O(c)**

where `n` is the number of characters, `m` is the length of the document, and `c` is the number of unique characters in the characters string.

```rust
use std::collections::HashMap;

pub struct Solution;

impl Solution {
    pub fn generate_document(characters: &str, document: &str) -> bool {
        let characters: Vec<char> = characters.chars().collect();
        let document: Vec<char> = document.chars().collect();

        let mut chars_map = HashMap::new();

        for (_, ch) in characters.iter().enumerate() {
            let count = chars_map.entry(*ch).or_insert(0);
            *count += 1;
        }

        for (_, ch) in document.iter().enumerate() {
            let count = chars_map.entry(*ch).or_insert(-1);
            *count -= 1;
            if *count < 0 {
                return false;
            }
        }

        true
    }
}

fn main() {
    assert_eq!(
        Solution::generate_document("Bste!hetsi ogEAxpelrt x ", "AlgoExpert is the Best!"),
        true
    );
    assert_eq!(
        Solution::generate_document("helloworld ", "hello wOrld"),
        false
    );
    assert_eq!(
        Solution::generate_document(
            "&*&you^a%^&8766 _=-09     docanCMakemthisdocument",
            "Can you make this document &"
        ),
        true
    );
}
```
