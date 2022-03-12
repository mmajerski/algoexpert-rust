## Tandem Bicycle

### Description

A tandem bicycle is a bicycle that's operated by two people: person A and person B. Both people pedal the bicycle, but the person that pedals faster dictates the speed of the bicycle. So if person A pedals at a speed of `5`, and person B pedals at a speed of `4`, the tandem bicycle moves at a speed of `5` (i.e., `tandemSpeed = max(speedA, speedB)`).

You're given two lists of positive integers: one that contains the speeds of riders wearing red shirts and one that contains the speeds of riders wearing blue shirts. Each rider is represented by a single positive integer, which is the speed that they pedal a tandem bicycle at. Both lists have the same length, meaning that there are as many red-shirt riders as there are blue-shirt riders. Your goal is to pair every rider wearing a red shirt with a rider wearing a blue shirt to operate a tandem bicycle.

Write a function that returns the maximum possible total speed or the minimum possible total speed of all of the tandem bicycles being ridden based on an input parameter, `fastest`. If `fastest = true`, your function should return the maximum possible total speed; otherwise it should return the minimum total speed.

"Total speed" is defined as the sum of the speeds of all the tandem bicyclesbeing ridden. For example, if there are 4 riders (2 red-shirt riders and 2 blue-shirt riders) who have speeds of `1, 3, 4, 5`, and if they're paired on tandem bicycles as follows: `[1, 4], [5, 3]`, then the total speed of these tandem bicycles is `4 + 5 = 9`.

### Sample Input

```
redShirtSpeeds = [5, 5, 3, 9, 2]
blueShirtSpeeds = [3, 6, 7, 2, 1]
fastest = true
```

### Sample Output

```
32
```

## Solution

Time and space complexity:

- time **O(nlogn)**
- space **O(1)**

where `n` is the number of tandem bicycles.

```rust
pub struct Solution;

impl Solution {
    pub fn tandem_bicycle(
        mut red_shirt_speeds: Vec<usize>,
        mut blue_shirt_speeds: Vec<usize>,
        fastest: bool,
    ) -> i32 {
        red_shirt_speeds.sort();
        blue_shirt_speeds.sort();

        let mut red_idx = red_shirt_speeds.len() - 1;
        let mut blue_idx = red_shirt_speeds.len() - 1;
        let mut total_speed: usize = 0;

        if fastest {
            for _ in 0..red_shirt_speeds.len() {
                if red_shirt_speeds[red_idx] > blue_shirt_speeds[blue_idx] {
                    total_speed += red_shirt_speeds[red_idx];
                    red_idx = red_idx.checked_sub(1).unwrap_or_default();
                } else {
                    total_speed += blue_shirt_speeds[blue_idx];
                    blue_idx = blue_idx.checked_sub(1).unwrap_or_default();
                }
            }
        } else {
            for _ in 0..red_shirt_speeds.len() {
                if red_shirt_speeds[red_idx] > blue_shirt_speeds[blue_idx] {
                    total_speed += red_shirt_speeds[red_idx];
                    red_idx = red_idx.checked_sub(1).unwrap_or_default();
                    blue_idx = blue_idx.checked_sub(1).unwrap_or_default();
                } else {
                    total_speed += blue_shirt_speeds[blue_idx];
                    blue_idx = blue_idx.checked_sub(1).unwrap_or_default();
                    red_idx = red_idx.checked_sub(1).unwrap_or_default();
                }
            }
        }

        total_speed as i32
    }
}

fn main() {
    assert_eq!(
        Solution::tandem_bicycle(vec![5, 5, 3, 9, 2], vec![3, 6, 7, 2, 1], true),
        32
    );
    assert_eq!(
        Solution::tandem_bicycle(
            vec![1, 2, 1, 9, 12, 3, 1, 54, 21, 231, 32, 1],
            vec![3, 3, 4, 6, 1, 2, 5, 6, 34, 256, 123, 32],
            false
        ),
        484
    );
}
```
