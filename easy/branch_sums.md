## Branch Sums

### Description

Write a function that takes in a Binary Tree and returns a list of its branch sums ordered from leftmost branch sum to rightmost branch sum.

A branch sum is the sum of all values in a Binary Tree branch. A Binary Tree branch is a path of nodes in a tree that starts at the root node and ends at any leaf node.

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be `BinaryTree` nodes themselves or `None` / `null`.

### Sample Input

```
tree =            1
              /        \
             2         3
           /  \       /  \
          4    5     6    7
         / \   /
        8   9 10
```

### Sample Output

```
[15, 16, 18, 10, 11]
// 15 == 1 + 2 + 4 + 8
// 16 == 1 + 2 + 4 + 9
// 18 == 1 + 2 + 5 + 10
// 10 == 1 + 3 + 6
// 11 == 1 + 3 + 7
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(n)**

where `n` is the number of nodes in the Binary Tree.

```rust
use std::cell::RefCell;
use std::rc::Rc;

#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

impl TreeNode {
    #[inline]
    pub fn new(val: i32) -> Self {
        TreeNode {
            val,
            left: None,
            right: None,
        }
    }
}

pub struct Solution;

impl Solution {
    pub fn branch_sums(tree: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut sums: Vec<i32> = Vec::new();

        Solution::calculate_sum(tree, 0, &mut sums);

        sums
    }

    fn calculate_sum(node: Option<Rc<RefCell<TreeNode>>>, current_sum: i32, sums: &mut Vec<i32>) {
        if let Some(n) = node {
            let new_current_sum = current_sum + n.borrow().val;
            if n.borrow().left == None && n.borrow().right == None {
                sums.push(new_current_sum);
            }

            Solution::calculate_sum(n.borrow().left.clone(), new_current_sum, sums);
            Solution::calculate_sum(n.borrow().right.clone(), new_current_sum, sums);
        } else {
            return;
        }
    }
}

fn main() {
    //            1
    //        /        \
    //       2          3
    //     /  \        /  \
    //    4     5     6    7
    //   / \    /
    //  8   9  10

    let mut node1_1 = TreeNode::new(1);
    let mut node1_2 = TreeNode::new(2);
    let mut node1_3 = TreeNode::new(3);
    let mut node1_4 = TreeNode::new(4);
    let mut node1_5 = TreeNode::new(5);
    let node1_6 = TreeNode::new(6);
    let node1_7 = TreeNode::new(7);
    let node1_8 = TreeNode::new(8);
    let node1_9 = TreeNode::new(9);
    let node1_10 = TreeNode::new(10);

    node1_5.left = Some(Rc::new(RefCell::new(node1_10)));
    node1_4.left = Some(Rc::new(RefCell::new(node1_8)));
    node1_4.right = Some(Rc::new(RefCell::new(node1_9)));
    node1_3.left = Some(Rc::new(RefCell::new(node1_6)));
    node1_3.right = Some(Rc::new(RefCell::new(node1_7)));
    node1_2.left = Some(Rc::new(RefCell::new(node1_4)));
    node1_2.right = Some(Rc::new(RefCell::new(node1_5)));
    node1_1.right = Some(Rc::new(RefCell::new(node1_3)));
    node1_1.left = Some(Rc::new(RefCell::new(node1_2)));

    //                  0
    //              /       \
    //             9         1
    //                     /   \
    //                    15    10
    //                         /  \
    //                       100   200

    let mut node1_2 = TreeNode::new(0);
    let node2_2 = TreeNode::new(9);
    let mut node3_2 = TreeNode::new(1);
    let node4_2 = TreeNode::new(15);
    let mut node5_2 = TreeNode::new(10);
    let node6_2 = TreeNode::new(100);
    let node7_2 = TreeNode::new(200);

    node5_2.right = Some(Rc::new(RefCell::new(node7_2)));
    node5_2.left = Some(Rc::new(RefCell::new(node6_2)));
    node3_2.right = Some(Rc::new(RefCell::new(node5_2)));
    node3_2.left = Some(Rc::new(RefCell::new(node4_2)));
    node1_2.right = Some(Rc::new(RefCell::new(node3_2)));
    node1_2.left = Some(Rc::new(RefCell::new(node2_2)));

    assert_eq!(
        Solution::branch_sums(Some(Rc::new(RefCell::new(node1_1)))),
        vec![15, 16, 18, 10, 11]
    );
    assert_eq!(
        Solution::branch_sums(Some(Rc::new(RefCell::new(node1_2)))),
        vec![9, 16, 111, 211]
    );
}
```
