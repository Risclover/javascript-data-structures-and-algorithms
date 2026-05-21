# Singly Linked List: Insert at Position

## Approach

- Inserting at a specific position means placing a new node at a given position within the list, shifting everything after it forward by one position.
- Requires traversal - we need to walk the list to find the node just *before* the target position, then rewire the pointers.
- The node just before the insertion point is called the **predecessor node**.
- We also need to handle two edge cases clearly:
    1. If position is `0`, it’s just an `insertHead`.
    2. If position equals the list’s `length`, it’s just an `insertTail`.

## High-level Algorithm

1. If position is out of bounds (less than 0 or greater than `length`), return null.
2. If position is 0, delegate to `insertHead` and return.
3. If position equals `length`, delegate to `insertTail` and return.
4. Create a new node with the given value.
5. Traverse the list to the node at `position - 1` (the predecessor).
    - Track `index` to mark our current position as we traverse.
6. Set new node’s `next` to predecessor’s `next`
    - New node now points to what comes after it
7. Set predecessor’s `next` to the new node
    - Predecessor now points to the new node
8. Increment length by 1

## Implementation

```jsx
insertAtPosition(value, position) {
	// If position is out of bounds, return null.
	if(position < 0 || position > this.length) {
		return null;
	}
	
	// If position is 0, delegate to insertHead.
	if(position === 0) {
		this.insertHead(value);
		return;
	}
	
	// If position equals length, delegate to insertTail.
	if(position === this.length) {
		this.insertTail(value);
		return;
	}
	
	// Create the new node
	const newNode = new Node(value);
	
	// Traverse to the predecessor node (the node at position - 1)
	let current = this.head;
	let index = 0;
	
	while(index < position - 1) {
		current = current.next;
		index++;
	}
	
	// New node points to what the predecessor was pointing to
	newNode.next = current.next;
	
	// Predecessor now points to the new node
	current.next = newNode;
	
	// Increment length
	this.length++;
}
		
```

- Time complexity: `O(n)`
- Space complexity: `O(1)`