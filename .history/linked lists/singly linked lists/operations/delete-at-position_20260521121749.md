# Singly Linked List: Delete at Position

## Approach

- Deleting at a specific position means removing the node at a given index and connecting the predecessor directly to the node that came after the deleted node, effectively skipping over it.
- This requires traversal to find the predecessor node.
- Core idea is the same as `deleteTail`: We need the predecessor node because:
    - The predecessor needs to bypass the deleted node by pointing to the deleted node’s `next`
    - Without that update, the deleted node would still be reachable and the list would be broken
- Edge cases:
    1. If postion is `0`, delegate to `deleteHead`
    2. If position is `length - 1`, delegate to `deleteTail`
    3. If position is out of bounds, return `null`

## High-level Algorithm

1. If position is out of bounds (less than 0 or ≥ length), return `null`.
2. If position is 0, delegate to `deleteHead` and return.
3. If position is `length - 1`, delegate to `deleteTail` and return.
4. Traverse to the predecessor node (the node at `position - 1`).
5. Store the node to be deleted (predecessor’s `next`).
6. Set predecessor’s `next` to the deleted node’s `next`.
    - Predecessor now skips over the deleted node.
7. Decrement length by 1.
8. Return the deleted node’s value.

## Implementation

```jsx
insertAtPosition(position) {
	// If position is out of bounds, return null.
	if(position < 0 || position >= this.length) return null;
	
	// If position is 0, delegate to deleteHead and return.
	if(position === 0) {
		return this.deleteHead();
	}
	
	// If position is length - 1, delegate to deleteTail and return.
	if(position === this.length - 1) {
		return this.deleteTail();
	}
	
	// Traverse to the predecessor node (position - 1)
	let current = this.head;
	let index = 0;
	
	while(index < position - 1) {
		current = current.next;
		index++;
	}
	// current is now predecessor
	
	// Store the node to be deleted
	const deletedNode = current.next;
	
	// Predecessor skips over the deleted node
	current.next = deletedNode.next;
	
	// Decrement length by 1
	this.length--;
	
	// Return deleted node's value
	return deletedNode.value;
}
```

- Time complexity: `O(n)`
- Space complexity: `O(1)`