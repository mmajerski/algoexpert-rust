## Find Three Largest Numbers

### Description

Write a function that takes in an array of at least three integers and, without sorting the input array, returns a sorted array of the three largest integers in the input array.

The function should return duplicate integers if necessary; for example, it should return `[10, 10, 12]` for an input array of `[10, 5, 9, 10, 12]`.

### Sample Input

```
array = [141, 1, 17, -7, -17, -27, 18, 541, 8, 7, 7]
```

### Sample Output

```
[18, 141, 541]
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the number of elements in the array.

```rust
pub struct Solution;

impl Solution {
    pub fn find_three_largest_numbers(array: Vec<i32>) -> Vec<i32> {
        let mut max_arr = vec![i32::MIN, i32::MIN, i32::MIN];

        for number in array {
            Solution::update_array(&mut max_arr, number);
        }

        max_arr
    }

    fn update_array(array: &mut Vec<i32>, number: i32) -> Vec<i32> {
        if array[2] < number {
            Solution::assign_values(array, 2, number);
        } else if array[1] < number {
            Solution::assign_values(array, 1, number);
        } else if array[0] < number {
            Solution::assign_values(array, 0, number);
        }

        array.to_vec()
    }

    fn assign_values(array: &mut Vec<i32>, index: i32, number: i32) {
        for i in 0..index + 1 {
            if i == index {
                array[i as usize] = number;
            } else {
                array[i as usize] = array[(i + 1) as usize];
            }
        }
    }
}

fn main() {
    assert_eq!(
        Solution::find_three_largest_numbers(vec![141, 1, 17, -7, -17, -27, 18, 541, 8, 7, 7]),
        vec![18, 141, 541]
    );
    assert_eq!(
        Solution::find_three_largest_numbers(vec![-1, -2, -3, -7, -17, -27, -18, -541, -8, -7, 7]),
        vec![-2, -1, 7]
    );
    assert_eq!(
        Solution::find_three_largest_numbers(vec![7, 7, 7, 7, 7, 7, 8, 7, 7, 7, 7]),
        vec![7, 7, 8]
    );
}
```
