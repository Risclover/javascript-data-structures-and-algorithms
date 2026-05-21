# SLL Interview Problems: Merge Two Sorted Lists

Given two sorted singly linked lists, merge them into a single sorted linked list and return the head of the merged list. Do not create new nodes - reuse the existing nodes.

## Approaches

- We have two linked lists where each is already sorted in ascending order. We need to weave them together into one sorted list by rewiring their `next` pointers - not by creating new nodes or copying values.
- At every step, we just need to compare the current front nodes of both lists and pick the smaller one. Whichever we pick becomes the next node in the merged list, and we advance that list’s pointer forward (a classic two pointer approach).

### Naive Approach

- Store every visited node in a hash set, then check each new node against the set. If we encounter a node we’ve already seen, there’s a cycle.
- Although this works, it costs `O(n)` space for the hash set, and we can do it in `O(1)` space.

### The Dummy Node Technique

This problem introduces an important implementation pattern, the **dummy node** (also called a **sentinel node**). The problem with building a new list from scratch is that the first node is a special case - before we add the first node, there’s nothing to attach it to. We’d need a separate `if` block just to handle the head. The dummy node eliminates this special case entirely.

- We create a dummy node with an arbitrary value at the start to act as a placeholder head.
- We always append to `dummy.next` rather than worrying about which node comes first.
- At the end, we simply return `dummy.next` as our real head and discard the dummy.

## High-level Algorithm

1. Create a dummy node to act as a placeholder head.
2. Set a `current` pointer to the dummy node.
3. While both lists have remaining nodes:
    1. Compare the values at the fronts of both lists.
    2. Attach the smaller node to `current.next`.
    3. Advance the pointer of whichever list we took from.
    4. Advance `current` forward.
4. When one list is exhausted, attach the remainder of the other list.
5. Return `dummy.next` as the head of the merged list.

## Implementation

```jsx
function mergeSortedLists(headA, headB) {
	// If either list is empty, return the other.
	if(!headA) return headB;
	if(!headB) return headA;
	
	// Create a dummy node to simplify head management
	const dummy = new Node(0);
	let current = dummy; // current builds the merged list
	
	let pointerA = headA; // traversal pointer for list A
	let pointerB = headB; // traversal pointer for list B
	
	// While both lists have nodes remaining...
	while(pointerA !== null && pointerB !== null) {
		if(pointerA.value <= pointerB.value) {
			current.next = pointerA; // Take from list A
			pointerA = pointerA.next; // Advance list A pointer
		} else {
			current.next = pointerB; // Take from list B
			pointerB = pointerB.next; // Advance list B pointer
		}
		current = current.next; // Advance the merged list pointer
	}
	
	// Attach whichever list still has remaining nodes
	if(pointerA !== null) {
		current.next = pointerA;
	} else {
		current.next = pointerB;
	}
	
	// Return the real head (skip the dummy node)
	return dummy.next;
}
```
- Time complexity: `O(n + m)`
    - where `n` is the length of list A and `m` is the length of list B.
- Space complexity: `O(1)`

---

⬅️ [Back to Singly Linked Lists](../singly-linked-lists.md)