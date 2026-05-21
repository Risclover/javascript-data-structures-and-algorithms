# SLL Interview Problems: Remove Nth Node from End

Given a singly linked list, remove the nth node from the end of the list and return the head of the modified list.

## Approaches

- We need to remove the node that sits `n` positions from the end.
- The challenge is that we’re measuring from the end, not the beginning, and in a linked list, we don’t know where the end is until we get there.

### Naive Approach

- Two passes - traverse once to find the length, compute the position from the front as `length - n`, and traverse again to that position and delete.
- Although this works, it’s not the most efficient.

### The Gap Technique

- If we place two pointers exactly `n` steps apart, then when the front pointer reaches the end of the list, the back pointer will be sitting exactly at the node we want to delete.
- We want the **predecessor** of the node to delete - we need the node just before it so we can rewire the pointer. So we place the back pointer one step before the target, meaning we maintain a gap of `n + 1` between the two pointers.
- Setup:
    - Advance `fast` pointer `n + 1` steps ahead of `slow`
    - Move both pointers forward together until `fast` reaches `null`
    - `slow` is now the predecessor of the node to delete
    - Rewire `slow.next` to skip over the target node
- We also use a **dummy node** here to elegantly handle the edge case where we need to delete the head node.

#### Why `n+1` and not `n`?

This is worth being precise about. We want `slow` to stop at the predecessor of the target, not the target itself. If we only advanced `fast` by `n` steps, `slow` would land on the target node directly - and we’d have no way to remove it without a reference to what came before it. Advancing `fast` by `n + 1` pushes `slow` one position earlier, landing it exactly on the predecessor.

## High-level Algorithm

1. Create a dummy node pointing to `head`.
2. Set `slow` and `fast` pointers to the dummy node.
3. Advance `fast` `n + 1` steps forward.
    - This creates a gap of `n + 1` between `fast` and `slow`.
4. Move both `slow` and `fast` forward together until `fast` is `null`.
5. `slow` is now the predecessor of the node to delete.
6. Rewire `slow.next` to skip over the target node.
7. Return `dummy.next` as the head.

## Implementation

```jsx
function removeNthFromEnd(head, n) {
	// Dummy node handles the edge case of deleting the head
	const dummy = new Node(0);
	dummy.next = head;
	
	let slow = dummy;
	let fast = dummy;
	
	// Advance fast n + 1 steps ahead of slow
	let steps = 0;
	
	while(steps <= n) {
		fast = fast.next;
		steps++;
	}
	
	// Move both pointers until fast reaches null
	while (fast !== null) {
		slow = slow.next;
		fast = fast.next;
	}
	// slow is now the predecessor of the node to delete.
	
	// skip over the target node
	slow.next = slow.next.next;
	
	// return the real head
	return dummy.next;
}
```
- Time complexity: `O(n)`
- Space complexity: `O(1)`

---

⬅️ [Back to Singly Linked Lists](../singly-linked-lists.md)