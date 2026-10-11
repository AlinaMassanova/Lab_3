# 1. Problem
Given the heads of two singly linked lists, find the node at which the two lists intersect. If they do not intersect, return `None`.

# 2. Approach
I used a two-pointer approach. `ptrA` starts at `headA` and `ptrB` starts at `headB`. They traverse their respective lists one step at a time. When a pointer reaches the end of its list, I redirect it to the head of the *other* list. By doing this, both pointers will traverse the exact same total distance (length A + length B). If there is an intersection, they will eventually meet at the intersection node at the exact same time. If there is no intersection, they will both reach `None` at the same time.

**Challenges / Failed Approaches:**
My first idea was a brute-force approach: loop through list A, and for each node, loop through list B to check for a match. This failed testing because it was too slow (Time Limit Exceeded - O(N*M) complexity). I also thought about storing list A nodes in a Hash Set, which works (O(N+M) time), but requires O(N) extra space, violating the O(1) space requirement often expected for this problem. 

**Tracing with example:**
List A: [1, 2, 3], List B: [6, 3] (intersection at 3)
- Step 1: A at 1, B at 6
- Step 2: A at 2, B at 3
- Step 3: A at 3, B at None
- Step 4: A at None, B at 1 (redirected to headA)
- Step 5: A at 6 (redirected to headB), B at 2
- Step 6: A at 3, B at 3. Match found! Return node 3.

# 3. Time Complexity
**Time Complexity: O(n + m)**
Where `n` and `m` are the lengths of the two lists. In the worst case, each pointer traverses both lists exactly once before they meet or reach `None`.

# 4. Space Complexity
**Space Complexity: O(1)**
Only two pointers (`ptrA` and `ptrB`) are used. We do not use any additional data structures.

# 5. Reflection / Improvement
- **Is there a more efficient approach?** The current two-pointer approach is the most optimal. Another O(1) space approach is finding the lengths of both lists, calculating the difference, and giving the longer list a head start, but the two-pointer redirection is more concise and has the exact same complexity.