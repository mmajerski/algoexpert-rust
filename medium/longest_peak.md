## Longest Peak

### Description

Write a function that takes in an array of integers and returns the length of the longest peak in the array.

A peak is defined as adjacent integers in the array that are <b>strictly</b> increasing until they reach a tip (the highest value in the peak), at which, point they become <b>strictly</b> decreasing. At least three integers are required to form a peak.

For example, the integers `1, 4, 10, 2` form a peak, but the integers `4, 0, 10` don't and neither do the integers `1, 2, 2, 0`. Similarly, the integers `1, 2, 3` don't form a peak because there aren't any strictly decreasing integers after the `3`.

### Sample Input

```
array = [1, 2, 3, 3, 4, 0, 10, 6, 5, -1, -3, 2, 3]
```

### Sample Output

```
6 // 0, 10, 6, 5, -1, -3
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the total number of elements in the array.

```rust
pub struct Solution;

impl Solution {
    pub fn longest_peak(array: Vec<i32>) -> i32 {
        let mut longest_peak = 0;
        let mut i = 1;

        while i < array.len() - 1 {
            let is_peak = array[i - 1] < array[i] && array[i] > array[i + 1];
            if !is_peak {
                i += 1;
                continue;
            }

            let mut left_idx = i as i32 - 2;
            while left_idx >= 0 && array[left_idx as usize] < array[left_idx as usize + 1] {
                left_idx -= 1;
            }

            let mut right_idx = i + 2;
            while right_idx < array.len() && array[right_idx] < array[right_idx - 1] {
                right_idx += 1;
            }

            let current_peak = right_idx as i32 - left_idx - 1;
            if current_peak > longest_peak {
                longest_peak = current_peak;
            }

            i = right_idx;
        }

        longest_peak as i32
    }
}

fn main() {
    assert_eq!(
        Solution::longest_peak(vec![1, 2, 3, 3, 4, 0, 10, 6, 5, -1, -3, 2, 3]),
        6
    );
    assert_eq!(Solution::longest_peak(vec![1, 2, 3, 3, 2, 1]), 0);
    assert_eq!(
        Solution::longest_peak(vec![
            1, 1, 1, 2, 3, 10, 12, -3, -3, 2, 3, 45, 800, 99, 98, 0, -1, -1, 2, 3, 4, 5, 0, -1, -1
        ]),
        9
    );
}
```
