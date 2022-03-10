## Minimum Waiting Time

### Description

You're given a non-empty array of positive integers representing the amounts of time that specific queries take to execute. Only one query can be executed at a time, but the queries can be executed in any order.

A query's `waiting time` is defined as the amount of time that it must wait before its execution starts. In other words, if a query is executed second, then its waiting time is the duration of the first query; if a query is executed third, then its waiting time is the sum of the durations of the first two queries.

Write a function that returns the minimum amount of total waiting time for all of the queries. For example, if you're given the queries of durations `[1, 4, 5]`, then the total waiting time if the queries were executed in the order of `[5, 1, 4]` would be `(0) + (5) + (5 + 1) = 11`. The first query of duration `5` would be executed immediately, so its waiting time would be `0`, the second query of duration `1` would have to wait `5` seconds (the duration of the first query) to be executed, and the last query would have to wait the duration of the first two queries before being executed.

Note: you're allowed to mutate the input array.

### Sample Input

```
queries = [3, 2, 1, 2, 6]
```

### Sample Output

```
17
```

## Solution

Time and space complexity:

- time **O(nlogn)**
- space **O(1)**

where `n` is the number of queries.

```rust
pub struct Solution;

impl Solution {
    pub fn minimum_waiting_time(mut queries: Vec<i32>) -> i32 {
        queries.sort();

        let mut total_waiting_time = 0;
        let mut queries_left = queries.len() as i32 - 1;

        for query in queries {
            total_waiting_time += query * queries_left;
            queries_left -= 1;
        }

        total_waiting_time
    }
}

fn main() {
    assert_eq!(Solution::minimum_waiting_time(vec![3, 2, 1, 2, 6]), 17);
    assert_eq!(
        Solution::minimum_waiting_time(vec![1, 1, 1, 4, 5, 6, 8, 1, 1, 2, 1]),
        81
    );
}
```
