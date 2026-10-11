# 1. Problem
We need to remove all nodes from a linked list that have a specific value `val` and return the new head of the list.

# 2. Approach
I used a `dummy` node that points to the `head` of the list. This is extremely helpful because the node to be removed might be the very first node (head). The dummy node ensures that we always have a previous node to work with. I iterate through the list using a `current` pointer (starting at dummy). If `current.next.val == val`, I skip `current.next` by rewiring `current.next` to `current.next.next`. If the value doesn't match, I just move `current` forward.

**Challenges / Failed Approaches:**
Initially, I tried solving it without a dummy node. My code broke when the target value was at the head of the list, or when all elements in the list needed to be removed (e.g., list: [7, 7, 7], target: 7). I had to write messy `if` statements to handle head deletions. Using a dummy node completely eliminated these edge cases and made the logic clean.

**Tracing with example:**
List: [1, 2, 6, 3], val: 6
- Setup: dummy(-1) -> 1 -> 2 -> 6 -> 3. `current` is at dummy.
- Iter 1: `current.next` is 1 ( != 6). Move `current` to 1.
- Iter 2: `current.next` is 2 ( != 6). Move `current` to 2.
- Iter 3: `current.next` is 6 ( == 6). Skip it: `current.next` = 3. `current` stays at 2.
- Iter 4: `current.next` is 3 ( != 6). Move `current` to 3.
- End of list. Return `dummy.next` (which is 1).

# 3. Time Complexity
**Time Complexity: O(n)**
We traverse the linked list exactly once. Each node comparison takes O(1) time.

# 4. Space Complexity
**Space Complexity: O(1)**
We modify the linked list in place using a single dummy node and one pointer. No arrays or new data structures are created.

# 5. Reflection / Improvement
- **Is there a more efficient approach?** The solution is already optimal in terms of time and space.
- **What could be changed?** It could be implemented recursively. A recursive approach would have O(n) time, but the space complexity would drop to O(n) due to the recursive call stack. Thus, the iterative approach is superior.