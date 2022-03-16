## Binary Search

### Description

Write a function that takes in a sorted array of integers as well as a target integer. The function should use the Binary Search algorithm to determine if the target integer is contained in the array and should return its index if it is, otherwise `-1`.

If you're unfamiliar with Binary Search, we recommend watching the Conceptual Overview section of this question's video explanation before starting to code.

### Sample Input

```
array = [0, 1, 21, 33, 45, 45, 61, 71, 72, 73]
target = 33
```

### Sample Output

```
3
```

## Solution

Time and space complexity:

- time **O(log(n))**
- space **O(1)**

where `n` is the length of the input array.

```rust
pub struct Solution;

impl Solution {
    pub fn binary_search(array: Vec<i32>, target: i32) -> i32 {
        let mut left_idx = array[0] as usize;
        let mut right_idx = array.len() - 1;

        while left_idx <= right_idx {
            let middle_idx = (left_idx + right_idx) / 2;
            let middle_value = array[middle_idx];

            if middle_value == target {
                return middle_idx as i32;
            } else if middle_value > target {
                right_idx = middle_idx - 1;
            } else {
                left_idx = middle_idx + 1;
            }
        }

        -1
    }
}

fn main() {
    assert_eq!(
        Solution::binary_search(vec![0, 1, 21, 33, 45, 45, 61, 71, 72, 73], 33),
        3
    );
    assert_eq!(
        Solution::binary_search(vec![0, 1, 21, 33, 45, 45, 61, 71, 72, 73, 355], 354),
        -1
    );
}
```
