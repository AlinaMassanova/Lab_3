# 1. Problem
Given the head of a singly linked list, determine if it is a palindrome (reads the same forwards and backwards).

# 2. Approach
To achieve O(1) space, I used the following algorithm:
1. **Find the middle:** Use the fast and slow pointer technique. `fast` moves 2 steps, `slow` moves 1 step. When `fast` reaches the end, `slow` is in the middle.
2. **Reverse the second half:** Starting from `slow`, reverse the pointers of the second half of the list.
3. **Compare:** Use two pointers, one at the `head` and one at the head of the reversed second half (`prev`). Compare them node by node. If they all match, it's a palindrome.

**Challenges / Failed Approaches:**
My first solution was to convert the linked list into a Python array (`list`) and just check if `arr == arr[::-1]`. This was very easy to write and worked perfectly, but it used O(N) space. I realized that to meet the true challenge of the problem (O(1) space constraint), I had to manipulate the linked list in place. Reversing a linked list is tricky, and I initially messed up the variables for reversing, causing infinite loops before I got the `prev`, `curr`, `next_temp` logic right.

**Tracing with example:**
List: [1, 2, 2, 1]
- Step 1 (Find middle): `slow` ends up at the second '2'.
- Step 2 (Reverse): Reverse from '2' onwards. The second half becomes [1, 2].
- Step 3 (Compare): `left` starts at head (1), `right` starts at reversed head (1).
  - Iter 1: left (1) == right (1).
  - Iter 2: left (2) == right (2).
  - `right` becomes `None`. Loop ends. Return `True`.

# 3. Time Complexity
**Time Complexity: O(n)**
Finding the middle takes O(n/2) steps. Reversing the second half takes O(n/2) steps. Comparing the two halves takes O(n/2) steps. Total time is roughly O(1.5n), which simplifies to O(n).

# 4. Space Complexity
**Space Complexity: O(1)**
We only use a few pointers (`slow`, `fast`, `prev`, `curr`, `left`, `right`) and reverse the list in place without allocating any new nodes or data structures.

# 5. Reflection / Improvement
- **Is there a more efficient approach?** No, in terms of Big-O, O(N) time and O(1) space is the most efficient possible solution. 
- **What could be changed?** In a production environment, mutating the input data structure (reversing it) is sometimes frowned upon unless you restore it before returning. I could add a step 4 to reverse the second half back to its original state before returning the boolean result. The complexity would remain the same.