## Sorted Squared Array

### Description

Write a function that takes in a non-empty array of integers that are sorted in ascending order and returns a new array of the same length with the squares of the original integers also sorted in ascending order.

### Sample Input

```
array = [1, 2, 3, 5, 6, 8, 9]
```

### Sample Output

```
[1, 4, 9, 25, 36, 64, 81]
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

```rust
pub struct Solution;

impl Solution {
    pub fn sorted_squared_array(array: Vec<i32>) -> Vec<i32> {
        let mut tmp_array = vec![0; array.len()];

        let mut smaller_index = 0;
        let mut larger_index = array.len() - 1;

        for (i, _) in array.iter().enumerate().rev() {
            let smaller_index_value = array[smaller_index] * array[smaller_index];
            let larger_index_value = array[larger_index] * array[larger_index];

            if smaller_index_value > larger_index_value {
                tmp_array[i] = smaller_index_value;
                smaller_index += 1;
            } else {
                tmp_array[i] = larger_index_value;
                // this if statement is required because usize values cannot be negative
                if larger_index > 0 {
                    larger_index -= 1;
                }
            }
        }

        tmp_array
    }
}

fn main() {
    assert_eq!(
        Solution::sorted_squared_array(vec![1, 2, 3, 5, 6, 8, 9]),
        vec![1, 4, 9, 25, 36, 64, 81]
    );
    assert_eq!(
        Solution::sorted_squared_array(vec![-50, -13, -2, -1, 0, 0, 1, 1, 2, 3, 19, 20]),
        vec![0, 0, 1, 1, 1, 4, 4, 9, 169, 361, 400, 2500]
    );
}
```
