## Two Number Sum

### Description

Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. If any two numbers in the input array sum up to the target sum, the function should return them in an array, in any order. If no two numbers sum up to the target sum, the function should return an empty array.

Note that the target sum has to be obtained by summing two different integers in the array; you can't add a single integer to itself in order to obtain the target sum.

You can assume that there will be at most one pair of numbers summing up to the target sum.

### Sample Input

```
array = [3, 5, -4, 8, 11, 1, -1, 6]
targetSum = 10
```

### Sample Output

```
[-1, 11] // the numbers could be in reverse order
```

## Solution using hash tables

Time and space complexity:

- time **O(n)**
- space **O(n)**

```rust
use std::collections::HashMap;

pub struct Solution;

impl Solution {
    pub fn two_number_sum(array: Vec<i32>, target: i32) -> Vec<i32> {
        let mut hash_table: HashMap<i32, bool> = HashMap::new();

        for (_, num) in array.iter().enumerate() {
            let complement = target - num;

            if let Some(_) = hash_table.get(&complement) {
                return vec![*num, complement];
            } else {
                hash_table.insert(*num, true);
            }
        }

        vec![]
    }
}

fn main() {
    assert_eq!(
        Solution::two_number_sum(vec![3, 5, -4, 8, 11, 1, -1, 6], 10),
        vec![-1, 11]
    );
    assert_eq!(
        Solution::two_number_sum(vec![-21, 301, 12, 4, 65, 56, 210, 356, 9, -47], 163),
        vec![-47, 210]
    );
}
```
