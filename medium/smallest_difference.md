## Smallest Difference

### Description

Write a function that takes in two non-empty arrays of integers, finds the pair of numbers (one from each array) whose absolute difference is closest to zero, and returns an array containing these two numbers, with the number from the first array in the first position.

Note that the absolute difference of two integers is the distance between them on the real number line. For example, the absolute difference of -5 and 5 is 10, and the absolute difference of -5 and -4 is 1.

You can assume that there will only be one pair of numbers with the smallest difference.

### Sample Input

```
arrayOne = [-1, 5, 10, 20, 28, 3]
arrayTwo = [26, 134, 135, 15, 17]
```

### Sample Output

```
[28, 26]
```

## Solution

Time and space complexity:

- time **O(nlog(n) + mlog(m))**
- space **O(1)**

where `n` is the length of the first input array and `m` is the lentgth of second input array.

```rust
pub struct Solution;

impl Solution {
    pub fn smallest_difference(mut array1: Vec<i32>, mut array2: Vec<i32>) -> Vec<i32> {
        array1.sort();
        array2.sort();

        let mut idx1: usize = 0;
        let mut idx2: usize = 0;

        let mut smallest_distance = i32::MAX;
        let mut current_distance;

        let mut smallest_pair = vec![0; 2];

        while idx1 < array1.len() && idx2 < array2.len() {
            let first_arr_value = array1[idx1];
            let second_arr_value = array2[idx2];

            if first_arr_value < second_arr_value {
                current_distance = second_arr_value - first_arr_value;
                idx1 += 1;
            } else if second_arr_value < first_arr_value {
                current_distance = first_arr_value - second_arr_value;
                idx2 += 1;
            } else {
                smallest_pair[0] = first_arr_value;
                smallest_pair[1] = second_arr_value;

                return smallest_pair;
            }

            if current_distance < smallest_distance {
                smallest_distance = current_distance;
                smallest_pair[0] = first_arr_value;
                smallest_pair[1] = second_arr_value;
            }
        }

        smallest_pair
    }
}

fn main() {
    assert_eq!(
        Solution::smallest_difference(vec![-1, 5, 10, 20, 28, 3], vec![26, 134, 135, 15, 17]),
        vec![28, 26]
    );
    assert_eq!(
        Solution::smallest_difference(
            vec![240, 124, 86, 111, 2, 84, 954, 27, 89],
            vec![1, 3, 954, 19, 8]
        ),
        vec![954, 954]
    );
    assert_eq!(
        Solution::smallest_difference(
            vec![10, 1000, 9124, 2142, 59, 24, 596, 591, 124, -123],
            vec![-1441, -124, -25, 1014, 1500, 660, 410, 245, 530]
        ),
        vec![-123, -124]
    );
}
```
