# SLL Interview Problems: Palindrome Check

Given a singly linked list, determine whether its values form a palindrome. A palindrome reads the same forwards and backwards.

## Approaches

- The challenge is that a singly linked list can only be traversed forward.
- To check if something is a palindrome, you need to compare it forwards and backwards simultaneously.

### Use an array (simple, `O(n)` space)

Convert the list to an array and use two pointers from both ends moving inward. This is the simplest approach and worth knowing as a baseline.

### Reverse second half in-place (optimal, `O(1)` space)

This is the optimal solution. The idea:

1. Find the middle of the list using fast/slow pointers.
2. Reverse the second half of the list in place.
3. Compare the first and reversed second half node by node.
4. Restore the list to its original state (optional, but good practice).

### Use a stack (`O(n)` space)

Push all values onto a stack as you traverse the list. Because a stack is LIFO (Last In First Out), popping from it gives you the values in reverse order. Then, traverse the list again from the head, comparing each node’s value against what you pop off the stack.

### Comparing all approaches

| Approach             | Time   | Space  | Notes                            |
|----------------------|--------|--------|----------------------------------|
| Array + two pointers | `O(n)` | `O(n)` | Simplest to implement            |
| Stack                | `O(n)` | `O(n)` | Intuitive use of LIFO            |
| Reverse second half  | `O(n)` | `O(1)` | Optimal - what interviewers want |

## High-level algorithms

### Using an array

1. If the list is empty, return `true`.
2. Traverse the list and collect every node’s value into an array.
3. Set a left pointer to index 0 and a right pointer to the last index.
4. While `left` is less than `right`:
    1. If `values[left] !== values[right]`, return `false`
    2. Increment `left`
    3. Decrement `right`
5. Return `true`

### Reverse second half in-place

1. If the list is empty or has one node, return `true`
2. Find the middle node using fast/slow pointers
3. Reverse the second half of the list starting from `middle.next`
4. Compare the first half (starting at `head`) with the reversed second half node by node
    1. If any values differ, return `false`
5. Restore the second half by reversing it again
6. Return `true`

### Using a stack

1. If the list is empty, return `true`
2. Traverse the list and push every node’s value onto a stack
3. Traverse the list again from the head:
    1. For each node, pop the top value off the stack
    2. If the node’s value `!==` the popped value, return `false`
4. Return `true`

## Implementations

### Using an array

```jsx
function isPalindromeArray(head) {
	// If empty, return true
	if(!head) return true;
	
	// Collect all values into an array
	const values = [];
	let current = head;
	
	while (current !== null) {
		values.push(current.value);
		current = current.next;
	}
	
	// Two pointer check from both ends
	let left = 0;
	let right = values.length - 1;
	
	while (left < right) {
		if (values[left] !== values[right]) {
			return false;
		}
		left++;
		right--;
	}
	return true;
}	

```
- Time complexity: `O(n)`
- Space complexity: `O(n)`

### Reverse second half in-place

```jsx
function isPalindrome(head) {
	// Empty list or single node is always a palindrome
	if (!head || !head.next) {
		return true;
	}
	
	// Find the middle node using fast/slow pointers
	let slow = head;
	let fast = head;
	
	while (fast !== null && fast.next !== null) {
		slow = slow.next;
		fast = fast.next.next;
	}
	// slow is now at the middle node
	
	// Reverse the second half of the list
	let secondHalfHead = reverseList(slow.next);
	
	// Compare first half and reversed second half
	let left = head;
	let right = secondHalfHead;
	let isPal = true;
	
	while (right !== null) {
		if (left.value !== right.value) {
			isPal = false;
			break;
		}
		left = left.next;
		right = right.next;
	}
	
	// Restore the second half (good interview practice)
	slow.next = reverseList(secondHalfHead);
	
	// Return result
	return isPal;
}

// Helper - reverses a linked list and returns the new head
function reverseList(head) {
	let prev = null;
	let current = head;
	let next = null;
	
	while (current !== null) {
		next = current.next;
		current.next = prev;
		prev = current;
		current = next;
	}
	
	return prev;
}
```
- Time complexity: `O(n)`
- Space complexity: `O(1)`

### Using a stack

```jsx
function isPalindromeStack(head) {
	if(!head) return true;
	
	const stack = [];
	let current = head;
	
	// Push all values onto the stack
	while (current !== null) {
		stack.push(current.value);
		current = current.next;
	}
	
	// Compare each node from the front against the stack (reverse order)
	current = head;
	
	while (current !== null) {
		if (current.value !== stack.pop()) {
			return false;
		}
		current = current.next;
	}
	
	return true;
}
```
- Time complexity: `O(n)`
- Space complexity: `O(n)`

---

⬅️ [Back to Singly Linked Lists](../singly-linked-lists.md)