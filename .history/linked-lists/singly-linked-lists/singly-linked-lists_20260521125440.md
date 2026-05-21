# Singly Linked Lists
[Back to Linked Lists](../linked-lists.md)
## General Overview
  ```
   HEAD
    |
  [ A | • ] —→ [ B | • ] —→ [ C | • ] —→ [ D | • ] —→ NULL
  ```
- Simplest form of a linked list.
- Each node stores its data and a single pointer, `next`, which points to the following node.
- The last node's `next` pointer is `null`, signaling the end of the list.
- Traversal is strictly one-directional - you can only move forward, never backward.
    - This simplicity comes with tradeoffs: Operations that need to reference a node's predecessor (like deleting the tail) require traversing the entire list to find the second-to-last node.

## Node Class

```javascript
class Node {
  constructor(value) {
    this.value = value; // The data this node holds
    this.next = null;   // Pointer to the next node (null by default)
  }
}
```

## Linked List Class Constructor

```javascript
class LinkedList {
    constructor() {
        this.head = null; // Points to the first node
        this.tail = null; // Points to the last node (optional but useful)
        this.length = 0;  // Tracks the number of nodes (optional but useful)
    }
}
```

## Common Operations

| Operation          | Time   | Space  | Details                                  |
|--------------------|--------|--------|------------------------------------------|
| Traversal          | `O(n)` | `O(1)` | [Link](operations/traversal.md)          |
| Insert head        | `O(1)` | `O(1)` | [Link](operations/insert-head.md)        |
| Insert tail        | `O(1)` | `O(1)` | [Link](operations/insert-tail.md)        |
| Insert at position | `O(n)` | `O(1)` | [Link](operations/insert-at-position.md) |
| Delete head        | `O(1)` | `O(1)` | [Link](operations/delete-head.md)        |
| Delete tail        | `O(n)` | `O(1)` | [Link](operations/delete-tail.md)        |
| Delete at position | `O(n)` | `O(1)` | [Link](operations/delete-at-position.md) |
| Search             | `O(n)` | `O(1)` | [Link](operations/search.md)             |
| Update             | `O(n)` | `O(1)` | [Link](operations/update.md)             |
| Reverse            | `O(n)` | `O(1)` | [Link](operations/reverse.md)            |

## Full Implementation

