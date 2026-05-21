# Singly Linked List: Update

## Approach

- Updating means finding the node at a given index and replacing its value with a new one.
- Essentially a search by index followed by a value assignment.
- Requires traversal.

## High-level Algorithm


1. If index is out of bounds (less than 0 or ≥ length), return `null`.
2. Traverse to the node at the given index.
3. Replace that node’s value with the new value.
4. Return the updated node’s value.

## Implementation


```jsx
update(index, newValue) {
    // Index is out of bounds
	if(index < 0 || index >= this.length) return null;
	
	let current = this.head;
	let counter = 0;
	
    // Traverse to the node at the given index
	while(counter < index) {
		current = current.next;
		counter++;
	}
	
    // Replace node's value with the new value
	current.value = newValue;
	// Return updated node's value
	return current.value;
}
		
```
- Time complexity: `O(n)`
- Space complexity: `O(1)`

---

⬅️ [Back to Singly Linked Lists](../singly-linked-lists.md)