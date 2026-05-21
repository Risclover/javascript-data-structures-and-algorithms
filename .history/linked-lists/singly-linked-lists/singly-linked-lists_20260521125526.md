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

```jsx
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  traverse() {
    if (!this.head) {
      console.log("List is empty.");
      return;
    }

    let current = this.head;

    while (current !== null) {
      console.log(current.value);
      current = current.next;
    }
  }

  insertHead(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head = newNode;
    }

    this.length++;
  }

  insertTail(value) {
    const newNode = new Node(value);

    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }

    this.length++;
  }

  insertAtPosition(value, position) {
    if (position < 0 || position > this.length) {
      console.log("Invalid position.");
      return null;
    }

    if (position === 0) {
      this.insertHead(value);
      return;
    }

    if (position === this.length) {
      this.insertTail(value);
      return;
    }

    const newNode = new Node(value);
    let current = this.head;
    let index = 0;

    while (index < position - 1) {
      current = current.next;
      index++;
    }

    newNode.next = current.next;
    current.next = newNode;

    this.length++;
  }

  deleteHead() {
    if (!this.head) {
      console.log("List is empty.");
      return null;
    }

    const deletedNode = this.head;
    this.head = this.head.next;

    if (!this.head) {
      this.tail = null;
    }

    this.length--;
    return deletedNode.value;
  }

  deleteTail() {
    if (!this.head) {
      console.log("List is empty.");
      return null;
    }

    if (this.head === this.tail) {
      const deletedValue = this.head.value;
      this.head = null;
      this.tail = null;
      this.length--;
      return deletedValue;
    }

    let current = this.head;

    while (current.next !== this.tail) {
      current = current.next;
    }

    const deletedValue = this.tail.value;
    current.next = null;
    this.tail = current;

    this.length--;
    return deletedValue;
  }

  deleteAtPosition(position) {
    if (position < 0 || position >= this.length) {
      console.log("Invalid position.");
      return null;
    }

    if (position === 0) {
      return this.deleteHead();
    }

    if (position === this.length - 1) {
      return this.deleteTail();
    }

    let current = this.head;
    let index = 0;

    while (index < position - 1) {
      current = current.next;
      index++;
    }

    const deletedNode = current.next;
    current.next = deletedNode.next;

    this.length--;
    return deletedNode.value;
  }

  searchByValue(value) {
    if (!this.head) {
      return -1;
    }

    let current = this.head;
    let index = 0;

    while (current !== null) {
      if (current.value === value) {
        return index;
      }
      current = current.next;
      index++;
    }

    return -1;
  }

  searchByIndex(index) {
    if (index < 0 || index >= this.length) {
      console.log("Invalid index.");
      return null;
    }

    let current = this.head;
    let counter = 0;

    while (counter < index) {
      current = current.next;
      counter++;
    }

    return current.value;
  }

  update(index, newValue) {
    if (index < 0 || index >= this.length) {
      console.log("Invalid index.");
      return null;
    }

    let current = this.head;
    let counter = 0;

    while (counter < index) {
      current = current.next;
      counter++;
    }

    current.value = newValue;
    return current.value;
  }

  reverse() {
    if (!this.head || this.head === this.tail) {
      return;
    }

    let prev = null;
    let current = this.head;
    let next = null;

    this.tail = this.head;

    while (current !== null) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    this.head = prev;
  }
}
```