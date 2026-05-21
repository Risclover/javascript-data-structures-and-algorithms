# SLL Interview Problems: Linked List Length

Given the head of a singly linked list, return the number of nodes in the list.

## Approach

Although more of a simple problem, it’s worth covering, because it appears as a sub-problem inside more complex problems constantly. Knowing how to get the length of a list cleanly is a baseline skill.

### Using the Length Property (`O(1)`)

If you’re working with a `LinkedList` class that tracks `this.length`, the answer is trivially `O(1)` - just return the property directly.

```jsx
function getLength(linkedList) {
	return linkedList.length;
}
```

<aside>
💡

This is worth mentioning in an interview to show awareness that good implementations track this. However, many interview problems give you only a **head node** with no wrapper class — so you need to know the traversal approach too.

</aside>

### Traversal (`O(n)`)

When given only a head node, traverse the list and count every node you visit.

## High-level algorithm

1. If head is `null`, return 0.
2. Initialize a counter to 0 and `current` to `head`.
3. While `current` is not `null`:
    1. Increment `counter`.
    2. Advance `current` forward.
4. Return `counter`.

## Implementation

```jsx
function getLength(head) {
	// Empty list has length 0
	if(!head) return 0;
	
	let current = head;
	let counter = 0;
	
	while (current !== null) {
		counter++;
		current = current.next;
	}
	
	return counter;
}
```

- Time complexity: `O(n)`
- Space complexity: `O(1)`