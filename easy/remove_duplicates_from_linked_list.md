## Remove Duplicates From Linked List

### Description

You're given the head of a Singly Linked List whose nodes are in sorted order with respect to their values. Write a function that returns a modified version of the Linked List that doesn't contain any nodes with duplicate values. The Linked List should be modified in place (i.e., you shouldn't create a brand new list), and the modified Linked List should still have its nodes sorted with respect to their values.

Each `LinkedList` node has an integer `value` as well as a `next` node pointing to the next node in the list or to `None` / `null` if it's the tail of the list.

### Sample Input

```
linkedList = 1 -> 1 -> 3 -> 4 -> 4 -> 4 -> 5 -> 6 -> 6 // the head node with value 1
```

### Sample Output

```
1 -> 3 -> 4 -> -> 5 -> 6 // the head node with value 1
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(1)**

where `n` is the number of nodes in the Linked List.

```rust
// Definition for singly-linked list.
#[derive(PartialEq, Eq, Clone, Debug)]
pub struct LinkedList {
    pub value: i32,
    pub next: Option<Box<LinkedList>>,
}

impl LinkedList {
    #[inline]
    fn new(value: i32) -> Self {
        LinkedList { next: None, value }
    }
}

pub struct Solution;

impl Solution {
    pub fn remove_duplicates_from_linked_list(
        linked_list: Option<Box<LinkedList>>,
    ) -> Option<Box<LinkedList>> {
        let mut linked_list = linked_list;
        let mut current_node = linked_list.as_mut();

        while let Some(node) = current_node {
            if let Some(n) = node.next.as_mut() {
                if node.value == n.value {
                    node.next = n.next.take();
                    current_node = Some(node);
                    continue;
                }
            }

            current_node = node.next.as_mut();
        }

        linked_list
    }
}

fn main() {
    // 1 -> 1 -> 3 -> 4 -> 4 -> 4 -> 5 -> 6 -> 6

    let node1_1 = LinkedList::new(6);
    let mut node2_1 = LinkedList::new(6);
    node2_1.next = Some(Box::new(node1_1));
    let mut node3_1 = LinkedList::new(5);
    node3_1.next = Some(Box::new(node2_1));
    let mut node4_1 = LinkedList::new(4);
    node4_1.next = Some(Box::new(node3_1));
    let mut node5_1 = LinkedList::new(4);
    node5_1.next = Some(Box::new(node4_1));
    let mut node6_1 = LinkedList::new(4);
    node6_1.next = Some(Box::new(node5_1));
    let mut node7_1 = LinkedList::new(3);
    node7_1.next = Some(Box::new(node6_1));
    let mut node8_1 = LinkedList::new(1);
    node8_1.next = Some(Box::new(node7_1));
    let mut node9_1 = LinkedList::new(1);
    node9_1.next = Some(Box::new(node8_1));

    // 1 -> 3 -> 4 -> 5 -> 6

    let node1_1_expected = LinkedList::new(6);
    let mut node2_1_expected = LinkedList::new(5);
    node2_1_expected.next = Some(Box::new(node1_1_expected));
    let mut node3_1_expected = LinkedList::new(4);
    node3_1_expected.next = Some(Box::new(node2_1_expected));
    let mut node4_1_expected = LinkedList::new(3);
    node4_1_expected.next = Some(Box::new(node3_1_expected));
    let mut node5_1_expected = LinkedList::new(1);
    node5_1_expected.next = Some(Box::new(node4_1_expected));

    assert_eq!(
        Solution::remove_duplicates_from_linked_list(Some(Box::new(node9_1))),
        Some(Box::new(node5_1_expected))
    );
}
```
