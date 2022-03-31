## First Duplicate Value

### Description

Given an array of integers between `1` and `n`, inclusive, where `n` is the length of the array, write a function that returns the first integer that appears more than once (when the array is read from left to right).

In other words, out of all the integers that might occur more than once in the input array, your function should return the one whose first duplicate value has the minimum index.

If no integer appears more than once, your function should return `-1`.

Note that you're allowed to mutate the input array.

### Sample Input

```
array = [2, 1, 5, 2, 3, 3, 4]
```

### Sample Output

```
2 // 2 is the first integer that appears more than once.
  // 3 also appears more than once, but the second 3 appears after the second 2.
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the length of the input array.

```rust
pub struct Solution;

impl Solution {
    pub fn first_duplicate_value(mut array: Vec<i32>) -> i32 {
        for i in 0..array.len() {
            let abs_value = (array[i]).abs();
            if array[abs_value as usize - 1] < 0 {
                return abs_value;
            }
            array[abs_value as usize - 1] *= -1;
        }

        -1
    }
}

fn main() {
    assert_eq!(
        Solution::first_duplicate_value(vec![2, 1, 5, 2, 3, 3, 4]),
        2
    );
    assert_eq!(
        Solution::first_duplicate_value(vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10]),
        -1
    );
    assert_eq!(
        Solution::first_duplicate_value(vec![
            29, 3, 23, 16, 1, 22, 21, 14, 15, 21, 12, 27, 9, 12, 11, 3, 22, 5, 21, 24, 14, 26, 11,
            5, 21, 25, 15, 19, 13, 4
        ]),
        21
    );
}
```
