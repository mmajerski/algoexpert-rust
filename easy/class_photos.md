## Class Photos

### Description

It's photo day at the local school, and you're the photographer assigned to take class photos. The class that you'll be photographing has an even number of students, and all these students are wearing red or blue shirts. In fact, exactly half of the class is wearing red shirts, and the other half is wearing blue shirts. You're responsible for arranging the students in two rows before taking the photo. Each row should contain the same number of the students and should adhere to the following guidelines:

<ul>
  <li>All students wearing red shirts must be in the same row.</li>
  <li>All students wearing blue shirts must be in the same row.</li>
  <li>
    Each student in the back row must be strictly taller than the student
    directly in front of them in the front row.
  </li>
</ul>

You're given two input arrays: one containing the heights of all the students with red shirts and another one containing the heights of all the students with blue shirts. These arrays will always have the same length, and each height will be a positive integer. Write a function that returns whether or not a class photo that follows the stated guidelines can be taken.

Note: you can assume that each class has at least 2 students.

### Sample Input

```
redShirtHeights = [5, 8, 1, 3, 4],
blueShirtHeights = [6, 9, 2, 4, 5]
```

### Sample Output

```
true // Place all students with blue shirts in the back row.
```

## Solution

Time and space complexity:

- time **O(nlogn)**
- space **O(1)**

where `n` is the number of students

```rust
pub struct Solution;

impl Solution {
    pub fn class_photos(
        mut red_shirt_heights: Vec<usize>,
        mut blue_shirt_heights: Vec<usize>,
    ) -> bool {
        red_shirt_heights.sort();
        blue_shirt_heights.sort();

        if red_shirt_heights[0] < blue_shirt_heights[0] {
            for i in 0..red_shirt_heights.len() {
                if red_shirt_heights[i] >= blue_shirt_heights[i] {
                    return false;
                }
            }
        } else if red_shirt_heights[0] > blue_shirt_heights[0] {
            for i in 0..red_shirt_heights.len() {
                if red_shirt_heights[i] <= blue_shirt_heights[i] {
                    return false;
                }
            }
        } else {
            return false;
        }

        true
    }
}

fn main() {
    assert_eq!(
        Solution::class_photos(vec![5, 8, 1, 3, 4], vec![6, 9, 2, 4, 5]),
        true
    );
    assert_eq!(
        Solution::class_photos(
            vec![19, 2, 4, 6, 2, 3, 1, 1, 4],
            vec![21, 5, 4, 4, 4, 4, 4, 4, 4]
        ),
        false
    );
}
```
