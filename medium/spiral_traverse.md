## Spiral Traverse

### Description

Write a function that takes in an n x m two-dimensional array (that can be square-shaped when n == m) and returns a one-dimensional array of all the array's elements in spiral order.

Spiral order starts at the top left corner of the two-dimensional array, goes to the right, and proceeds in a spiral pattern all the way until every element has been visited.

### Sample Input

```
array =  [
    [1,    2, 3, 4],
    [12, 13, 14, 5],
    [11, 16, 15, 6],
    [10,   9, 8, 7]
  ]
```

### Sample Output

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the total number of elements in the outer array.

```rust
pub struct Solution;

impl Solution {
    pub fn spiral_traverse(array: Vec<Vec<i32>>) -> Vec<i32> {
        let mut result = vec![];
        let mut start_row = 0 as usize;
        let mut end_row = array.len() - 1;
        let mut start_col = 0 as usize;
        let mut end_col = array[0].len() - 1;

        while start_row <= end_row && start_col <= end_col {
            for col in start_col..(end_col + 1) {
                result.push(array[start_row][col]);
            }

            for row in (start_row + 1)..(end_row + 1) {
                result.push(array[row][end_col]);
            }

            for col in (start_col..end_col).rev() {
                if start_row == end_row {
                    break;
                }

                result.push(array[end_row][col]);
            }

            for row in (start_row + 1..end_row).rev() {
                if start_col == end_col {
                    break;
                }

                result.push(array[row][start_col]);
            }

            start_row += 1;
            start_col += 1;
            if end_col > 0 && end_row > 0 {
                end_row -= 1;
                end_col -= 1;
            }
        }

        result
    }
}

fn main() {
    assert_eq!(
        Solution::spiral_traverse(vec![
            vec![1, 2, 3, 4],
            vec![12, 13, 14, 5],
            vec![11, 16, 15, 6],
            vec![10, 9, 8, 7]
        ]),
        vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]
    );
    assert_eq!(
        Solution::spiral_traverse(vec![
            vec![1, 2, 3, 4],
            vec![10, 11, 12, 5],
            vec![9, 8, 7, 6],
        ]),
        vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    );
    assert_eq!(
        Solution::spiral_traverse(vec![
            vec![1],
            vec![3],
            vec![2],
            vec![5],
            vec![4],
            vec![7],
            vec![6]
        ]),
        vec![1, 3, 2, 5, 4, 7, 6]
    );
}
```
