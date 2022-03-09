## Node Depths

### Description

The distance between a node in a Binary Tree and the tree's root is called the node's depth.

Write a function that takes in a Binary Tree and returns the sum of its nodes' depths.

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be `BinaryTree` nodes themselves or `None` / `null`.

### Sample Input

```
tree =            1
              /        \
             2          3
           /  \        /  \
          4    5      6    7
         / \
        8   9
```

### Sample Output

```
16
// The depth of the node with value 2 is 1.
// The depth of the node with value 3 is 1.
// The depth of the node with value 4 is 2.
// The depth of the node with value 5 is 2.
// Etc..
// Summing all of these depths yields 16.
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(h)**

where `n` is the number of nodes in the Binary Tree and `h` is the height of the Binary Tree.

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
    pub fn node_depths(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
        Solution::calculate_depth(root, 0)
    }

    fn calculate_depth(node: Option<Rc<RefCell<TreeNode>>>, current_depth: i32) -> i32 {
        if let Some(n) = node {
            return current_depth
                + Solution::calculate_depth(n.borrow().left.clone(), current_depth + 1)
                + Solution::calculate_depth(n.borrow().right.clone(), current_depth + 1);
        }

        0
    }
}

fn main() {
    //            1
    //        /        \
    //       2          3
    //     /  \        /  \
    //    4     5     6    7
    //   / \
    //  8   9

    let mut node1_1 = TreeNode::new(1);
    let mut node1_2 = TreeNode::new(2);
    let mut node1_3 = TreeNode::new(3);
    let mut node1_4 = TreeNode::new(4);
    let node1_5 = TreeNode::new(5);
    let node1_6 = TreeNode::new(6);
    let node1_7 = TreeNode::new(7);
    let node1_8 = TreeNode::new(8);
    let node1_9 = TreeNode::new(9);

    node1_4.left = Some(Rc::new(RefCell::new(node1_8)));
    node1_4.right = Some(Rc::new(RefCell::new(node1_9)));
    node1_3.left = Some(Rc::new(RefCell::new(node1_6)));
    node1_3.right = Some(Rc::new(RefCell::new(node1_7)));
    node1_2.left = Some(Rc::new(RefCell::new(node1_4)));
    node1_2.right = Some(Rc::new(RefCell::new(node1_5)));
    node1_1.right = Some(Rc::new(RefCell::new(node1_3)));
    node1_1.left = Some(Rc::new(RefCell::new(node1_2)));

    //                  1
    //              /       \
    //             2         8
    //            /            \
    //           3              9
    //          /                 \
    //         4                   10
    //        /                      \
    //       5                        11
    //      /                           \
    //     6                             12
    //      \                            /
    //       7                          13

    let mut node1_2 = TreeNode::new(1);
    let mut node2_2 = TreeNode::new(2);
    let mut node3_2 = TreeNode::new(8);
    let mut node4_2 = TreeNode::new(3);
    let mut node5_2 = TreeNode::new(9);
    let mut node6_2 = TreeNode::new(4);
    let mut node7_2 = TreeNode::new(10);
    let mut node8_2 = TreeNode::new(5);
    let mut node9_2 = TreeNode::new(11);
    let mut node10_2 = TreeNode::new(6);
    let mut node11_2 = TreeNode::new(12);
    let node12_2 = TreeNode::new(7);
    let node13_2 = TreeNode::new(13);

    node11_2.left = Some(Rc::new(RefCell::new(node13_2)));
    node10_2.right = Some(Rc::new(RefCell::new(node12_2)));
    node9_2.right = Some(Rc::new(RefCell::new(node11_2)));
    node8_2.left = Some(Rc::new(RefCell::new(node10_2)));
    node7_2.right = Some(Rc::new(RefCell::new(node9_2)));
    node6_2.left = Some(Rc::new(RefCell::new(node8_2)));
    node5_2.right = Some(Rc::new(RefCell::new(node7_2)));
    node4_2.left = Some(Rc::new(RefCell::new(node6_2)));
    node3_2.right = Some(Rc::new(RefCell::new(node5_2)));
    node2_2.left = Some(Rc::new(RefCell::new(node4_2)));
    node1_2.right = Some(Rc::new(RefCell::new(node3_2)));
    node1_2.left = Some(Rc::new(RefCell::new(node2_2)));

    assert_eq!(
        Solution::node_depths(Some(Rc::new(RefCell::new(node1_1)))),
        16
    );
    assert_eq!(
        Solution::node_depths(Some(Rc::new(RefCell::new(node1_2)))),
        42
    );
}
```
