## Run-Length Encoding

### Description

Write a function that takes in a non-empty string and returns its run-length encoding.

From Wikipedia, "run-length encoding is a form of lossless data compression in which runs of data are stored as a single data value and count, rather than as the original run." For this problem, a run of data is any sequence of consecutive, identical characters. So the run `"AAA"` would be run-length-encoded as `"3A"`.

To make things more complicated, however, the input string can contain all sorts of special characters, including numbers. And since encoded data must be decodable, this means that we can't naively run-length-encode long runs. For example, the run `"AAAAAAAAAAAA"` (12 `A`s), can't naively be encoded as `"12A"`, since this string can be decoded as either `"AAAAAAAAAAAA"` or `"1AA"`. Thus, long runs (runs of 10 or more characters) should be encoded in a split fashion; the aforementioned run should be encoded as `"9A3A"`.

### Sample Input

```
string = "AAAAAAAAAAAAABBCCCCDD",
```

### Sample Output

```
"9A4A2B4C2D"
```

## Solution using hash tables

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the length of the input string.

```rust
pub struct Solution;

impl Solution {
    pub fn run_length_encoding(str: &str) -> String {
        let str: Vec<char> = str.chars().collect();

        let mut encoded_string = String::from("");
        let mut current_length = 1;

        for (i, _) in str.iter().enumerate().skip(1) {
            let prev_char = str[i - 1];
            let cur_char = str[i];

            if prev_char != cur_char || current_length == 9 {
                encoded_string.push(char::from_digit(current_length, 10).unwrap());
                encoded_string.push(prev_char);

                current_length = 0;
            }

            current_length += 1;
        }

        encoded_string.push(char::from_digit(current_length, 10).unwrap());
        encoded_string.push(str[str.len() - 1]);

        encoded_string
    }
}

fn main() {
    assert_eq!(
        Solution::run_length_encoding("AAAAAAAAAAAAABBCCCCDD"),
        String::from("9A4A2B4C2D")
    );
    assert_eq!(
        Solution::run_length_encoding("........______=========AAAA   AAABBBB   BBB"),
        String::from("8.6_9=4A3 3A4B3 3B")
    );
    assert_eq!(
        Solution::run_length_encoding("AAAAAAAAAAAAABBCCCCDDDDDDDDDDD"),
        String::from("9A4A2B4C9D2D")
    );
}
```
