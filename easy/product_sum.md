## Product Sum

### Description

Write a function that takes in a "special" array and returns its product sum.

A "special" array is a non-empty array that contains either integers or other "special" arrays. The product sum of a "special" array is the sum of its elements, where "special" arrays inside it are summed themselves and then multiplied by their level of depth.

The depth of a "special" array is how far nested it is. For instance, the depth of `[]` is `1`; the depth of the inner array in `[[]]` is `2`; the depth of the innermost array in `[[[]]]` is `3`.

Therefore, the product sum of `[x, y]` is `x + y`; the product sum of `[x, [y, z]]` is `x + 2 * (y + z)`; the product sum of `[x, [y, [z]]]` is `x + 2 * (y + 3z)`.

### Sample Input

```
array = [5, 2, [7, -1], 3, [6, [-13, 8], 4]]
```

### Sample Output

```
12 // calculated as: 5 + 2 + 2 * (7 - 1) + 3 + 2 * (6 + 3 * (-13 + 8) + 4)
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(d)**

where `n` is the total number of elements in the array, including sub-elements, and `d` is the greatest depth of "special" arrays in the array.

```rust
#[derive(Debug)]
pub enum SpecialArray {
    Integer(i32),
    Vector(Vec<SpecialArray>),
}

pub struct Solution;

impl Solution {
    pub fn product_sum(array: Vec<SpecialArray>) -> i32 {
        Solution::calculate_sum(array, 1)
    }

    fn calculate_sum(array: Vec<SpecialArray>, multiplier: i32) -> i32 {
        let mut sum = 0;

        for a in array {
            match a {
                SpecialArray::Integer(val) => {
                    sum += val;
                }
                SpecialArray::Vector(vec) => {
                    sum += Solution::calculate_sum(vec, multiplier + 1);
                }
            }
        }

        sum * multiplier
    }
}

fn main() {
    // [5, 2, [7, -1], 3, [6, [-13, 8], 4]]

    let special1 = vec![
        SpecialArray::Integer(5),
        SpecialArray::Integer(2),
        SpecialArray::Vector(vec![SpecialArray::Integer(7), SpecialArray::Integer(-1)]),
        SpecialArray::Integer(3),
        SpecialArray::Vector(vec![
            SpecialArray::Integer(6),
            SpecialArray::Vector(vec![SpecialArray::Integer(-13), SpecialArray::Integer(8)]),
            SpecialArray::Integer(4),
        ]),
    ];

    // [1, 2, [3], 4, 5]

    let special2 = vec![
        SpecialArray::Integer(1),
        SpecialArray::Integer(2),
        SpecialArray::Vector(vec![SpecialArray::Integer(3)]),
        SpecialArray::Integer(4),
        SpecialArray::Integer(5)
    ];

    assert_eq!(Solution::product_sum(special1), 12);
    assert_eq!(Solution::product_sum(special2), 18);
}
```
