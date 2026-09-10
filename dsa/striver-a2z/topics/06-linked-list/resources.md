# Learn LinkedList — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Introduction to LinkedList (takeUforward)](https://youtu.be/Nq7ok-OyEpg?si=9PR1o8OPRWil7fRA) — build, traverse, length, and search on a singly LL.
- [Striver — Insert & Delete operations on a Singly LL](https://youtu.be/VaECK03Dz-g?si=vHSwdf9jhE05adKM) — head/tail/position insertion and deletion.
- [Striver — Doubly Linked List (introduction + operations)](https://youtu.be/0eKMU10uEDI?si=uDnoj_C5ghEpNLvP) — DLL structure, insert-before-head, delete-head.
- [Striver — Reverse a Doubly Linked List](https://youtu.be/u3WUW2qe6ww?si=96Wwlju72IvmzkxE) — pointer-swap reversal in O(1) space.
- [Striver — Middle of a LinkedList (Tortoise–Hare)](https://youtu.be/7LjQ57RqgEc?si=ir_rRDio38rhamU_) — the fast/slow one-pass trick.
- [Striver — Reverse a LinkedList (iterative + recursive)](https://youtu.be/D2vI2DNJGd8?si=RCaLSx01qR21IBdh) — the canonical `prev/cur/next` reversal.
- [Striver — Detect a loop in LL](https://youtu.be/wiOo4DC5GGA?si=zagt6O6tFXc4_3cx) — Floyd's cycle detection.
- [Striver — Starting point of the loop](https://youtu.be/2Kd0KKmmHFc?si=7UreDPRjRvapeVB0) — cycle-II with the distance-identity proof.
- [Striver — Reverse Nodes in K-Group](https://youtu.be/lIar1skcQYI?si=_jFghHKX4eaK36a1) — hard reversal pattern.
- [Striver — Clone a LL with random pointer](https://youtu.be/q570bKdrnlw?si=epZtpWvtNwuTf23o) — the O(1)-space interleave technique.
- [Striver A2Z DSA Course/Sheet (full course hub)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the parent playlist/sheet for every step.

---

## 📝 Articles & Tutorials

- [takeUforward — Linked List: Introduction](https://takeuforward.org/linked-list/linked-list-introduction) — first-principles explanation with code.
- [takeUforward — Reverse a Linked List](https://takeuforward.org/data-structure/reverse-a-linked-list/) — iterative and recursive write-ups.
- [takeUforward — Detect a cycle in a Linked List](https://takeuforward.org/data-structure/detect-a-cycle-in-a-linked-list/) — hashing vs Floyd comparison.
- [takeUforward — Starting point of loop in a Linked List](https://takeuforward.org/data-structure/starting-point-of-loop-in-a-linked-list/) — cycle-entry derivation.
- [takeUforward — Flattening a Linked List](https://takeuforward.org/data-structure/flattening-a-linked-list/) — multi-level merge approach.
- [GeeksforGeeks — Floyd's Cycle Finding Algorithm](https://www.geeksforgeeks.org/floyds-cycle-finding-algorithm/) — full explanation with variants.
- [GeeksforGeeks — Detect Loop or Cycle in Linked List](https://ui.geeksforgeeks.org/videos/detect-loop-or-cycle-in-linked-list) — hash-set vs tortoise–hare.
- [cp-algorithms — Tortoise and Hare (cycle detection)](https://cp-algorithms.com/others/tortoise_and_hare.html) — rigorous algorithm + proof.
- [Wikipedia — Cycle detection (Floyd & Brent)](https://en.wikipedia.org/wiki/Cycle_detection) — theory, alternatives, complexity.
- [Medium — A Complete Mathematical Proof of Floyd's Cycle-Finding Algorithm](https://medium.com/@ekelman3/a-complete-mathematical-proof-of-floyds-cycle-finding-algorithm-f1ab765dc99a) — the modular-arithmetic proof.
- [Math StackExchange — Proof of Floyd Cycle Chasing](https://math.stackexchange.com/q/913529) — community-vetted proof discussion.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — Linked List / Stack / Queue / Deque](https://visualgo.net/en/list) — animate insert/delete/search on singly & doubly lists.
- [USFCA — Data Structure Visualizations (Galles)](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — step-through list operations and more.
- [VisuAlgo — main portal](https://visualgo.net/en) — index of all data-structure animations.

---

## ❓ Most-Asked Interview Questions

1. **How do you find the middle of a linked list in one pass?** Use fast/slow: slow moves 1, fast moves 2; when fast reaches the end, slow is at the middle.
2. **How do you detect a cycle?** Floyd's tortoise–hare; if the 1× and 2× pointers ever meet, a cycle exists (O(n)/O(1)).
3. **How do you find where the cycle begins?** After they meet, reset one pointer to head and advance both by one; they meet at the entry (head→entry == meet→entry).
4. **Reverse a linked list — iterative vs recursive?** Iterative uses `prev/cur/next` (O(1) space); recursion uses O(n) stack; both O(n) time.
5. **Why use a dummy/sentinel node?** It removes special-casing for operations that can modify the head (remove-nth, merge, sort, K-group).
6. **Difference between singly and doubly linked lists?** DLL has a `prev` pointer enabling backward traversal and O(1) deletion given a node, at the cost of extra memory.
7. **How do you find the intersection of two lists?** Two pointers that switch to the other head on reaching null align at the intersection after ≤ 2 passes; O(n+m)/O(1).
8. **How do you remove the Nth node from the end?** Advance a lead pointer N steps, then move both until the lead hits the end; the trailing pointer is just before the target (use a dummy head).
9. **How do you check if a list is a palindrome in O(1) space?** Find the middle, reverse the second half, compare halves, then optionally restore.
10. **How do you sort a linked list in O(n log n)?** Merge sort: split at the middle, recursively sort halves, merge — arrays' quicksort is awkward here due to no random access.
11. **How do you reverse nodes in groups of K?** Verify K nodes remain, reverse that block, recurse/iterate on the rest, and reattach; leftover < K stays as-is.
12. **How do you clone a list with random pointers in O(1) extra space?** Interleave copies after originals, wire `copy->random = orig->random->next`, then detach the two lists.
13. **How do you rotate a list by k?** Form a ring by joining tail to head, take `k %= len`, walk `len - k` steps, and break the ring for the new head.
14. **Why are linked lists poor for cache performance?** Nodes are scattered in memory, so traversal causes frequent cache misses versus a contiguous array.
15. **How do you delete a node given only a pointer to it (not the head)?** Copy the next node's data into it and delete the next node (works only if it isn't the tail).

---

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Ch. 10 (Elementary Data Structures):** linked-list representations and operations. See [`../../../books/`](../../../books/) if a local copy is tracked in this repo.
- **Cormen et al. — pointer/sentinel discussion in the same chapter:** the theory behind dummy-node techniques.
- [Striver's A2Z DSA Course/Sheet](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — structured free course covering this entire LinkedList step.

---

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Sheet (Step 6 hub)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the official step containing all these problems.
- [LeetCode — Linked List tag](https://leetcode.com/tag/linked-list/) — every linked-list problem on the platform.
- [LeetCode — Linked List Explore Card](https://leetcode.com/explore/learn/card/linked-list/) — guided study plan for the topic.
- [GeeksforGeeks — Data Structures: Linked List](https://www.geeksforgeeks.org/data-structures/linked-list/) — comprehensive problem/article index.
