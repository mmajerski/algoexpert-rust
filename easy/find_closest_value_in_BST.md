## Find Closest Value In BST

### Description

Write a function that takes in a Binary Search Tree (BST) and a target integer value and returns the closest value to that target value contained in the BST.

You can assume that there will only be one closest value.

Each `BST` node has an integer `value`, a `left` child node, and a `right` child node. A node is said to be a valid `BST` node if and only if it satisfies the BST property: its `value` is strictly greater than the values of every node to its left; its `value` is less than or equal to the values of every node to its right; and its children nodes are either valid `BST` nodes themselves or `None` / `null`.

### Sample Input

```
tree =            10
              /        \
             5         15
           /  \       /  \
          2    5     13   22
         /            \
        1              14

target = 12
```

### Sample Output

```
13
```

## Solution

Time and space complexity:

- time **O(logn)**
- space **O(1)**

where `n` is the number of nodes in BST.

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
    pub fn find_closest_value(tree: Option<Rc<RefCell<TreeNode>>>, target: i32) -> i32 {
        let mut closest = i32::MAX;
        let mut current_node = tree;

        while current_node.is_some() {
            if let Some(node_ref) = current_node {
                let node = node_ref.borrow();
                if i32::abs(target - node.val) < i32::abs(target - closest) {
                    closest = node.val;
                }

                if node.val > target {
                    current_node = node.left.clone();
                } else if node.val < target {
                    current_node = node.right.clone();
                } else {
                    return closest;
                }
            }
        }

        closest
    }
}

fn main() {
    //            10
    //        /        \
    //       5         15
    //     /  \       /  \
    //    2    5     13   22
    //   /            \
    //  1              14

    let mut node1_1 = TreeNode::new(10);
    let mut node2_1 = TreeNode::new(5);
    let mut node3_1 = TreeNode::new(15);
    let mut node4_1 = TreeNode::new(2);
    let node5_1 = TreeNode::new(5);
    let mut node6_1 = TreeNode::new(13);
    let node7_1 = TreeNode::new(22);
    let node8_1 = TreeNode::new(1);
    let node9_1 = TreeNode::new(14);

    node6_1.right = Some(Rc::new(RefCell::new(node9_1)));
    node3_1.left = Some(Rc::new(RefCell::new(node6_1)));
    node3_1.right = Some(Rc::new(RefCell::new(node7_1)));
    node1_1.right = Some(Rc::new(RefCell::new(node3_1)));
    node4_1.left = Some(Rc::new(RefCell::new(node8_1)));
    node2_1.right = Some(Rc::new(RefCell::new(node5_1)));
    node2_1.left = Some(Rc::new(RefCell::new(node4_1)));
    node1_1.left = Some(Rc::new(RefCell::new(node2_1)));

    //                  100
    //           /             \
    //          5              502
    //        /  \          /      \
    //       2    15       204      55000
    //      / \   / \     /   \     /
    //     1   3  5  22  203  205  1001
    //    / \         \         \     \
    //  -51  1         57        207   4500
    //   /    \          \       /  \
    // -403    1          60    206  208
    //          \
    //           1
    //            \
    //             1

    let mut node1_2 = TreeNode::new(100);
    let mut node2_2 = TreeNode::new(5);
    let mut node3_2 = TreeNode::new(502);
    let mut node4_2 = TreeNode::new(2);
    let mut node5_2 = TreeNode::new(15);
    let mut node6_2 = TreeNode::new(204);
    let mut node7_2 = TreeNode::new(55000);
    let mut node8_2 = TreeNode::new(1);
    let node9_2 = TreeNode::new(3);
    let node10_2 = TreeNode::new(5);
    let mut node11_2 = TreeNode::new(22);
    let node12_2 = TreeNode::new(203);
    let mut node13_2 = TreeNode::new(205);
    let mut node14_2 = TreeNode::new(1001);
    let mut node15_2 = TreeNode::new(-51);
    let mut node16_2 = TreeNode::new(1);
    let mut node17_2 = TreeNode::new(57);
    let mut node18_2 = TreeNode::new(207);
    let node19_2 = TreeNode::new(4500);
    let node20_2 = TreeNode::new(-403);
    let mut node21_2 = TreeNode::new(1);
    let node22_2 = TreeNode::new(60);
    let node23_2 = TreeNode::new(206);
    let node24_2 = TreeNode::new(208);
    let mut node25_2 = TreeNode::new(1);
    let node26_2 = TreeNode::new(1);

    node25_2.right = Some(Rc::new(RefCell::new(node26_2)));
    node21_2.right = Some(Rc::new(RefCell::new(node25_2)));
    node15_2.left = Some(Rc::new(RefCell::new(node20_2)));
    node16_2.right = Some(Rc::new(RefCell::new(node21_2)));
    node17_2.right = Some(Rc::new(RefCell::new(node22_2)));
    node18_2.left = Some(Rc::new(RefCell::new(node23_2)));
    node18_2.right = Some(Rc::new(RefCell::new(node24_2)));
    node8_2.left = Some(Rc::new(RefCell::new(node15_2)));
    node8_2.right = Some(Rc::new(RefCell::new(node16_2)));
    node11_2.right = Some(Rc::new(RefCell::new(node17_2)));
    node13_2.right = Some(Rc::new(RefCell::new(node18_2)));
    node14_2.right = Some(Rc::new(RefCell::new(node19_2)));
    node4_2.left = Some(Rc::new(RefCell::new(node8_2)));
    node4_2.right = Some(Rc::new(RefCell::new(node9_2)));
    node5_2.left = Some(Rc::new(RefCell::new(node10_2)));
    node5_2.right = Some(Rc::new(RefCell::new(node11_2)));
    node6_2.left = Some(Rc::new(RefCell::new(node12_2)));
    node6_2.right = Some(Rc::new(RefCell::new(node13_2)));
    node7_2.left = Some(Rc::new(RefCell::new(node14_2)));
    node2_2.left = Some(Rc::new(RefCell::new(node4_2)));
    node2_2.right = Some(Rc::new(RefCell::new(node5_2)));
    node3_2.left = Some(Rc::new(RefCell::new(node6_2)));
    node3_2.right = Some(Rc::new(RefCell::new(node7_2)));
    node1_2.left = Some(Rc::new(RefCell::new(node2_2)));
    node1_2.right = Some(Rc::new(RefCell::new(node3_2)));

    assert_eq!(
        Solution::find_closest_value(Some(Rc::new(RefCell::new(node1_1))), 12),
        13
    );
    assert_eq!(
        Solution::find_closest_value(Some(Rc::new(RefCell::new(node1_2))), 208),
        208
    );
}
```
