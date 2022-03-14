## Nth Fibonacci

### Description

The Fibonacci sequence is defined as follows: the first number of the sequence is `0`, the second number is `1`, and the nth number is the sum of the (n - 1)th and (n - 2)th numbers. Write a function that takes in an integer `n` and returns the nth Fibonacci number.

Important note: the Fibonacci sequence is often defined with its first two numbers as `F0 = 0` and `F1 = 1`. For the purpose of this question, the first Fibonacci number is `F0`; therefore, `getNthFib(1)` is equal to `F0`, `getNthFib(2)` is equal to `F1`, etc..

### Sample Input

```
n = 2
```

### Sample Output

```
1 // 0, 1
```

## Solution using hash tables

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the input number

```rust
pub struct Solution;

impl Solution {
    pub fn get_nth_fib(n: i32) -> i32 {
        if n == 1 {
            return 0;
        }

        if n == 2 {
            return 1;
        }

        Solution::get_nth_fib(n - 1) + Solution::get_nth_fib(n - 2)
    }
}

fn main() {
    assert_eq!(Solution::get_nth_fib(6), 5);
    assert_eq!(Solution::get_nth_fib(18), 1597);
}
```
