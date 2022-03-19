## Insertion Sort

### Description

Write a function that takes in an array of integers and returns a sorted version of that array. Use the Insertion Sort algorithm to sort the array.

### Sample Input

```
array = [8, 5, 2, 9, 5, 6, 3]
```

### Sample Output

```
[2, 3, 5, 5, 6, 8, 9]
```

## Solution

Time and space complexity:

- time **O(n<sup>2</sup>)**
- space **O(1)**

where `n` is the length of the input array.

```rust
pub struct Solution;

impl Solution {
    pub fn insertion_sort(mut array: Vec<i32>) -> Vec<i32> {
        for i in 1..array.len() {
            let mut j = i;
            while j > 0 && array[j] < array[j - 1] {
                array.swap(j, j - 1);
                j -= 1;
            }
        }

        array
    }
}

fn main() {
    assert_eq!(
        Solution::insertion_sort(vec![8, 5, 2, 9, 5, 6, 3]),
        vec![2, 3, 5, 5, 6, 8, 9]
    );
    assert_eq!(Solution::insertion_sort(vec![1, 2]), vec![1, 2]);
    assert_eq!(
        Solution::insertion_sort(vec![
            -823, 164, 48, -987, 323, 399, -293, 183, -908, -376, 14, 980, 965, 842, 422, 829, 59,
            724, -415, -733, 356, -855, -155, 52, 328, -544, -371, -160, -942, -51, 700, -363,
            -353, -359, 238, 892, -730, -575, 892, 490, 490, 995, 572, 888, -935, 919, -191, 646,
            -120, 125, -817, 341, -575, 372, -874, 243, 610, -36, -685, -337, -13, 295, 800, -950,
            -949, -257, 631, -542, 201, -796, 157, 950, 540, -846, -265, 746, 355, -578, -441,
            -254, -941, -738, -469, -167, -420, -126, -410, 59
        ]),
        vec![
            -987, -950, -949, -942, -941, -935, -908, -874, -855, -846, -823, -817, -796, -738,
            -733, -730, -685, -578, -575, -575, -544, -542, -469, -441, -420, -415, -410, -376,
            -371, -363, -359, -353, -337, -293, -265, -257, -254, -191, -167, -160, -155, -126,
            -120, -51, -36, -13, 14, 48, 52, 59, 59, 125, 157, 164, 183, 201, 238, 243, 295, 323,
            328, 341, 355, 356, 372, 399, 422, 490, 490, 540, 572, 610, 631, 646, 700, 724, 746,
            800, 829, 842, 888, 892, 892, 919, 950, 965, 980, 995
        ]
    );
}
```
