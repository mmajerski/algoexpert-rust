## Monotonic Array

### Description

Write a function that takes in an array of integers and returns a boolean representing whether the array is monotonic.

An array is said to be monotonic if its elements, from left to right, are entirely non-increasing or entirely non-decreasing.

Non-increasing elements aren't necessarily exclusively decreasing; they simply don't increase. Similarly, non-decreasing elements aren't necessarily exclusively increasing; they simply don't decrease.

Note that empty arrays and arrays of one element are monotonic.

### Sample Input

```
array = [-1, -5, -10, -1100, -1100, -1101, -1102, -9001]
```

### Sample Output

```
true
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the length of the input array.

```rust
pub struct Solution;

impl Solution {
    pub fn is_monotonic(array: Vec<i32>) -> bool {
        let mut is_non_decreasing = true;
        let mut is_non_increasing = true;

        for i in 1..array.len() {
            if array[i] > array[i - 1] {
                is_non_increasing = false;
            } else if array[i] < array[i - 1] {
                is_non_decreasing = false;
            }
        }

        return is_non_decreasing || is_non_increasing;
    }
}

fn main() {
    assert_eq!(
        Solution::is_monotonic(vec![-1, -5, -10, -1100, -1100, -1101, -1102, -9001]),
        true
    );
    assert_eq!(Solution::is_monotonic(vec![]), true);
    assert_eq!(Solution::is_monotonic(vec![1, 2, 3, 3, 2, 1]), false);
}
```
