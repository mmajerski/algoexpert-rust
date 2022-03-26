## Move Element To End

### Description

You're given an array of integers and an integer. Write a function that moves all instances of that integer in the array to the end of the array and returns the array.

The function should perform this in place (i.e., it should mutate the input array) and doesn't need to maintain the order of the other integers.

### Sample Input

```
array = [2, 1, 2, 2, 2, 3, 4, 2]
toMove = 2
```

### Sample Output

```
[1, 3, 4, 2, 2, 2, 2, 2] // the numbers 1, 3, and 4 could be ordered differently
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the length of the input array.

```rust
pub struct Solution;

impl Solution {
    pub fn move_element_to_end(mut array: Vec<i32>, to_move: i32) -> Vec<i32> {
        let mut movable_index = array.len() - 1;
        let mut i = 0;

        while i < array.len() && movable_index > i {
            if array[i] == to_move && array[movable_index] == to_move {
                movable_index -= 1;
                i -= 1;
            } else if array[i] == to_move && array[movable_index] != to_move {
                (array[i], array[movable_index]) = (array[movable_index], array[i]);
                movable_index -= 1;
            }

            i += 1;
        }

        array
    }
}

fn main() {
    assert_eq!(
        Solution::move_element_to_end(vec![2, 1, 2, 2, 2, 3, 4, 2], 2),
        vec![4, 1, 3, 2, 2, 2, 2, 2]
    );
    assert_eq!(Solution::move_element_to_end(vec![], 3), vec![]);
    assert_eq!(
        Solution::move_element_to_end(
            vec![5, 1, 2, 5, 5, 3, 4, 6, 7, 5, 8, 9, 10, 11, 5, 5, 12],
            5
        ),
        vec![12, 1, 2, 11, 10, 3, 4, 6, 7, 9, 8, 5, 5, 5, 5, 5, 5]
    );
}
```
