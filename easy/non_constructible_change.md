## Non Constructible Change

### Description

Given an array of positive integers representing the values of coins in your possession, write a function that returns the minimum amount of change (the minimum sum of money) that you <b>cannot</b> create. The given coins can have any positive integer value and aren't necessarily unique (i.e., you can have multiple coins of the same value).

For example, if you're given `coins = [1, 2, 5]`, the minimum amount of change that you can't create is `4`. If you're given no coins, the minimum amount of change that you can't create is `1`.

### Sample Input

```
coins = [5, 7, 1, 1, 2, 3, 22]
```

### Sample Output

```
20
```

## Solution

Time and space complexity:

- time **O(nlogn)**
- space **O(n)**

where `n` is number of coins

```rust
pub struct Solution;

impl Solution {
    pub fn non_constructible_change(coins: Vec<i32>) -> i32 {
        let mut sorted_coins = coins;
        sorted_coins.sort();

        let mut current_change_created = 0;
        for coin in sorted_coins {
            if coin > current_change_created + 1 {
                return current_change_created + 1;
            }

            current_change_created += coin
        }

        current_change_created + 1
    }
}

fn main() {
    assert_eq!(
        Solution::non_constructible_change(vec![5, 7, 1, 1, 2, 3, 22]),
        20
    );
    assert_eq!(
        Solution::non_constructible_change(vec![109, 2000, 8765, 19, 18, 17, 16, 8, 1, 1, 2, 4]),
        87
    );
}
```
