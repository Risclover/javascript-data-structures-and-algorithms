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

```javascript
class Node {
  constructor(value) {
    this.value = value; // The data this node holds
    this.next = null;   // Pointer to the next node (null by default)
  }
}
```

## List Constructor

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

| Operation          | Time | Space | Details |
| ------------------ | --- | --- | --- |
| Traversal          | `O(n)` | `O(1)` | --- |
| Insert head        | `O(1)` | `O(1)` | --- |
| Insert tail        | `O(1)` | `O(1)` | --- |
| Insert at position | `O(n)` | `O(1)` | --- |
| Delete head        | `O(1)` | `O(1)` | --- |
| Delete tail        | `O(n)` | `O(1)` | --- |
| Delete at position | `O(n)` | `O(1)` | --- |
| Search             | `O(n)` | `O(1)` | --- |
| Update             | `O(n)` | `O(1)` | --- |
| Reverse            | `O(n)` | `O(1)` | --- |