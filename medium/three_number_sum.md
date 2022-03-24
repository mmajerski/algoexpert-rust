## Three Number Sum

### Description

Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. The function should find all triplets in the array that sum up to the target sum and return a two-dimensional array of all these triplets. The numbers in each triplet should be ordered in ascending order, and the triplets themselves should be ordered in ascending order with respect to the numbers they hold.

If no three numbers sum up to the target sum, the function should return an empty array.

### Sample Input

```
array = [12, 3, 1, 2, -6, 5, -8, 6]
targetSum = 0
```

### Sample Output

```
[[-8, 2, 6], [-8, 3, 5], [-6, 1, 5]]
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the length of the input array.

```rust
use std::ops::Add;

pub struct Solution;

impl Solution {
    pub fn three_number_sum(mut array: Vec<i32>, target: i32) -> Vec<Vec<i32>> {
        array.sort();
        let mut triplets = vec![];

        for i in 0..array.len() - 2 {
            let mut left = i.add(1);
            let mut right = array.len() - 1;

            while left < right {
                let current_sum = array[left] + array[right] + array[i];

                if current_sum == target {
                    triplets.push(vec![array[i], array[left], array[right]]);
                    left += 1;
                    right -= 1;
                } else if current_sum < target {
                    left += 1;
                } else if current_sum > target {
                    right -= 1;
                }
            }
        }

        triplets
    }
}

fn main() {
    let empty_vec: Vec<Vec<i32>> = Vec::new();

    assert_eq!(
        Solution::three_number_sum(vec![12, 3, 1, 2, -6, 5, -8, 6], 0),
        vec![vec![-8, 2, 6], vec![-8, 3, 5], vec![-6, 1, 5]]
    );
    assert_eq!(
        Solution::three_number_sum(vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 15], 32),
        vec![vec![8, 9, 15]]
    );
    assert_eq!(
        Solution::three_number_sum(vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 15], 5),
        empty_vec
    );
}
```
