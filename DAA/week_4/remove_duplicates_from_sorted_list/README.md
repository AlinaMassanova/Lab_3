# 1. Problem
Given the head of a sorted linked list, we need to delete all duplicate nodes so that each element appears only once. The linked list must remain sorted.

# 2. Approach
Since the list is already sorted, duplicates will be adjacent to each other. I used a single pointer `current` to traverse the list. If `current.val` is equal to `current.next.val`, I bypass the next node by setting `current.next = current.next.next`. If they are not equal, I simply move `current` to the next node.

**Challenges / Failed Approaches:**
Initially, I thought about using a hash set to track seen values. However, I realized this is inefficient because the list is already sorted, so we only need to compare adjacent nodes. The hash set approach would waste O(N) space unnecessarily. 

**Tracing with example:**
List: [1, 1, 2, 3, 3]
- Iteration 1: `current` at 1. `current.val` (1) == `current.next.val` (1). 
  Change `current.next` to point to 2. List: [1, 2, 3, 3].
- Iteration 2: `current` at 1. `current.val` (1) != `current.next.val` (2). 
  Move `current` to 2.
- Iteration 3: `current` at 2. `current.val` (2) != `current.next.val` (3). 
  Move `current` to 3.
- Iteration 4: `current` at 3. `current.val` (3) == `current.next.val` (3). 
  Change `current.next` to `None`. List: [1, 2, 3].
- End of list. Return head.

# 3. Time Complexity
**Time Complexity: O(n)**
Where `n` is the number of nodes in the list. We traverse the linked list exactly once. Each comparison and pointer update takes O(1) constant time.

# 4. Space Complexity
**Space Complexity: O(1)**
We only use a single pointer `current` and modify the existing list in place. No extra memory is used.

# 5. Reflection / Improvement
- **Is there a more efficient approach?** No, this is the most optimal approach. We must visit each node at least once, so O(n) time is the theoretical minimum. O(1) space is also optimal.