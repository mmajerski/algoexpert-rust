## Validate Subsequence

### Description

Given two non-empty arrays of integers, write a function that determines whether the second array is a subsequence of the first one.

A subsequence of an array is a set of numbers that aren't necessarily adjacent in the array but that are in the same order as they appear in the array. For instance, the numbers `[1, 3, 4]` `[1, 2, 3, 4]`, and so do the numbers `[2, 4]`. Note that a single number in an array and the array itself are both valid subsequences of the array.

### Sample Input

```
array = [5, 1, 22, 25, 6, -1, 8, 10]
sequence = [1, 6, -1, 10]
```

### Sample Output

```
true
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

```rust
pub struct Solution;

impl Solution {
    pub fn is_valid_subsequence(array: Vec<i32>, sequence: Vec<i32>) -> bool {
        let mut sequence_index = 0;

        for (_, array_value) in array.iter().enumerate() {
            if let Some(sequence_value) = sequence.get(sequence_index) {
                if *sequence_value == *array_value && sequence_index < sequence.len() {
                    sequence_index += 1;
                }
            }
        }

        sequence_index == sequence.len()
    }
}

fn main() {
    assert_eq!(
        Solution::is_valid_subsequence(vec![5, 1, 22, 25, 6, -1, 8, 10], vec![1, 6, -1, 10]),
        true
    );
    assert_eq!(
        Solution::is_valid_subsequence(
            vec![5, 1, 22, 25, 6, -1, 8, 10],
            vec![5, 1, 22, 25, 6, -1, 8, 10, 12]
        ),
        false
    );
}
```
