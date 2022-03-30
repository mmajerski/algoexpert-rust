## Array Of Products

### Description

Write a function that takes in a non-empty array of integers and returns an array of the same length, where each element in the output array is equal to the product of every other number in the input array.

In other words, the value at `output[i]` is equal to the product of every number in the input array other than `input[i]`

Note that you're expected to solve this problem without using division.

### Sample Input

```
array = [5, 1, 4, 2]
```

### Sample Output

```
[8, 40, 10, 20]
// 8 is equal to 1 x 4 x 2
// 40 is equal to 5 x 4 x 2
// 10 is equal to 5 x 1 x 2
// 20 is equal to 5 x 1 x 4
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the total number of elements in the array.

```rust
pub struct Solution;

impl Solution {
    pub fn array_of_products(array: Vec<i32>) -> Vec<i32> {
        let mut products_array = vec![1; array.len()];

        let mut left_running_product = 1;
        for i in 0..array.len() {
            products_array[i] = left_running_product;
            left_running_product *= array[i];
        }

        let mut right_running_prodcut = 1;
        for i in (0..array.len()).rev() {
            products_array[i] *= right_running_prodcut;
            right_running_prodcut *= array[i];
        }

        products_array
    }
}

fn main() {
    assert_eq!(
        Solution::array_of_products(vec![5, 1, 4, 2]),
        vec![8, 40, 10, 20]
    );
    assert_eq!(
        Solution::array_of_products(vec![0, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]),
        vec![0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    );
    assert_eq!(
        Solution::array_of_products(vec![0, 1, 2, 3, 4, 5, 6, 7, 8, 9]),
        vec![362880, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    );
}
```
