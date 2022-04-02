## Merge Overlapping Intervals

### Description

Write a function that takes in a non-empty array of arbitrary intervals, merges any overlapping intervals, and returns the new intervals in no particular order.

Each interval `interval` is an array of two integers, with `interval[0]` as the start of the interval and `interval[1]` as the end of the interval.

Note that back-to-back intervals aren't considered to be overlapping. For example, `[1, 5]` and `[6, 7]` aren't overlapping; however, `[1, 6]` and `[6, 7]` are indeed overlapping.

Also note that the start of any particular interval will always be less than or equal to the end of that interval.

### Sample Input

```
intervals = [[1, 2], [3, 5], [4, 7], [6, 8], [9, 10]]
```

### Sample Output

```
[[1, 2], [3, 8], [9, 10]]
// Merge the intervals [3, 5], [4, 7], and [6, 8].
// The intervals could be ordered differently.
```

## Solution

Time and space complexity:

- time **O(nlong(n))**
- space **O(n)**

where `n` is the length of the input array.

```rust
use std::cmp;

pub struct Solution;

impl Solution {
    pub fn merge_overlapping_intervals(intervals: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let mut sorted_intervals = intervals.clone();
        sorted_intervals.sort_by(|a, b| a[0].cmp(&b[0]));

        let mut merged_intervals: Vec<Vec<i32>> = Vec::new();
        merged_intervals.push(sorted_intervals[0].clone());

        for i in 1..sorted_intervals.len() {
            let current_interval = sorted_intervals[i].clone();
            let j = merged_intervals.len() - 1;

            if current_interval[0] <= merged_intervals[j][1] {
                merged_intervals[j][1] = cmp::max(current_interval[1], merged_intervals[j][1]);
            } else {
                merged_intervals.push(current_interval)
            }
        }

        merged_intervals
    }
}

fn main() {
    assert_eq!(
        Solution::merge_overlapping_intervals(vec![
            vec![1, 2],
            vec![3, 5],
            vec![4, 7],
            vec![6, 8],
            vec![9, 10]
        ]),
        vec![vec![1, 2], vec![3, 8], vec![9, 10]]
    );
    assert_eq!(
        Solution::merge_overlapping_intervals(vec![
            vec![89, 90],
            vec![-10, 20],
            vec![-50, 0],
            vec![70, 90],
            vec![90, 91],
            vec![90, 95]
        ]),
        vec![vec![-50, 20], vec![70, 95]]
    );
    assert_eq!(
        Solution::merge_overlapping_intervals(vec![
            vec![20, 21],
            vec![22, 23],
            vec![0, 1],
            vec![3, 4],
            vec![23, 24],
            vec![25, 27],
            vec![5, 6],
            vec![7, 19]
        ]),
        vec![
            vec![0, 1],
            vec![3, 4],
            vec![5, 6],
            vec![7, 19],
            vec![20, 21],
            vec![22, 24],
            vec![25, 27]
        ]
    );
}
```
