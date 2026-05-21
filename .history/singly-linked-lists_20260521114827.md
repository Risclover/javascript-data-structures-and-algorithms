# Singly Linked Lists

## General Overview

- Simplest form of a linked list.
- Each node stores its data and a single pointer, `next`, which points to the following node.
- The last node's `next` pointer is `null`, signaling the end of the list.

```
 HEAD
  |
[ A | • ] —→ [ B | • ] —→ [ C | • ] —→ [ D | • ] —→ NULL
```

- Traversal is strictly one-directional - you can only move forward, never backward.
    - This simplicity comes with tradeoffs: Operations that need to reference a node's predecessor (like deleting the tail) require traversing the entire list to find the second-to-last node.

## Node Structure

```

```