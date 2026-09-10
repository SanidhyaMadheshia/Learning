# Learn LinkedList — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** (the sub-steps of the topic). Every problem from the sheet appears exactly once, each with intuition, a worked example, and a memorable analogy. Difficulty: 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Learn 1D LinkedList

### Introduction to Singly LinkedList  🟢 Easy
**Links:** [Article](https://takeuforward.org/linked-list/linked-list-introduction) · 🎥 [YouTube](https://youtu.be/Nq7ok-OyEpg?si=9PR1o8OPRWil7fRA)
**Intuition / Approach:** Represent each element as a `Node{data, next}`. Build the chain by pointing each node's `next` to the following node; the last node points to `nullptr`. Traverse by following `next` from `head`.
**Example:** Values `[3, 1, 4]` → `head → 3 → 1 → 4 → null`. Traversal prints `3 1 4`.
**Analogy:** A scavenger hunt — each clue (node) tells you only where the *next* clue is, not the whole route.

### Insertion at the head of Linked List  🟢 Easy
**Links:** [Article](https://takeuforward.org/linked-list/insert-at-the-head-of-a-linked-list) · 🎥 [YouTube](https://youtu.be/VaECK03Dz-g?si=vHSwdf9jhE05adKM&t=1934)
**Intuition / Approach:** Make the new node point to the current head, then move `head` to the new node — O(1), no traversal needed.
**Example:** List `10 → 20`, insert `5` at head → `5 → 10 → 20`.
**Analogy:** Cutting to the front of a queue — you link arms with the current first person and become the new front.

### Deletion of the head of LL  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/delete-node-in-a-linked-list/) · 🎥 [YouTube](https://youtu.be/VaECK03Dz-g?si=CRaBHbOo2bHFbOT5)
**Intuition / Approach:** Save the head in a temp, move `head = head->next`, then free the temp. Guard the empty-list case.
**Example:** List `5 → 10 → 20`, delete head → `10 → 20` (node `5` freed).
**Analogy:** The person at the front of the line leaves; the second person is now the front.

### Find the length of the Linked List  🟢 Easy
**Links:** [Article](https://takeuforward.org/linked-list/find-the-length-of-a-linked-list) · 🎥 [YouTube](https://youtu.be/Nq7ok-OyEpg?si=xqQbukLfo2oZ6C6s&t=2240)
**Intuition / Approach:** Walk from head to `nullptr`, incrementing a counter each step. O(n).
**Example:** `7 → 7 → 9 → null` → count = 3.
**Analogy:** Counting train cars by walking from the engine to the caboose, one car at a time.

### Search in Linked List  🟡 Medium
**Links:** [Article](https://takeuforward.org/linked-list/search-an-element-in-a-linked-list) · 🎥 [YouTube](https://youtu.be/Nq7ok-OyEpg?si=WNXcIaXZ_B6cNq0s&t=2524)
**Intuition / Approach:** Linear scan — compare each node's `data` to the target; return true on a match, false if you hit `nullptr`.
**Example:** Search `9` in `7 → 9 → 2` → found at position 2 → true.
**Analogy:** Looking for a friend by walking down a line of people and checking each face until you find them.

---

## Learn Doubly LinkedList

### Introduction to Doubly LL  🟢 Easy
**Links:** [Article](https://takeuforward.org/linked-list/introduction-to-doubly-linked-list) · 🎥 [YouTube](https://youtu.be/0eKMU10uEDI?si=uDnoj_C5ghEpNLvP)
**Intuition / Approach:** Each node stores `prev` and `next`. This lets you walk backward as well as forward and delete a node in O(1) when you hold its pointer.
**Example:** `null ← 10 ⇄ 20 ⇄ 30 → null`; from `30` you can reach `10` by following `prev` twice.
**Analogy:** A two-way street — you can drive to a house from either direction, unlike a one-way singly list.

### Insert node before head in Doubly Linked List  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/insert-at-end-of-doubly-linked-list/) · 🎥 [YouTube](https://youtu.be/0eKMU10uEDI?si=J5a0pQTosimcO_aA&t=2684)
**Intuition / Approach:** New node's `next` = old head; if head exists, set `head->prev` = new node; then move head to the new node.
**Example:** `10 ⇄ 20`, insert `5` before head → `5 ⇄ 10 ⇄ 20`.
**Analogy:** A new locomotive coupled at the front of a train — it links to the old front car both ways.

### Delete head of Doubly Linked List  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/delete-last-node-of-a-doubly-linked-list/) · 🎥 [YouTube](https://youtu.be/0eKMU10uEDI?si=sE7jqrW46lfRHVLd&t=853)
**Intuition / Approach:** Advance head to `head->next`, set the new head's `prev = nullptr`, and free the old head. Handle single-node and empty cases.
**Example:** `5 ⇄ 10 ⇄ 20`, delete head → `10 ⇄ 20` (10's `prev` becomes null).
**Analogy:** Unhitching the front car of a train; the second car becomes the lead and has nothing ahead of it.

### Reverse a Doubly Linked List  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/reverse-a-doubly-linked-list/) · 🎥 [YouTube](https://youtu.be/u3WUW2qe6ww?si=96Wwlju72IvmzkxE)
**Intuition / Approach:** For each node, swap its `prev` and `next` pointers; the old tail becomes the new head. O(n) time, O(1) space.
**Example:** `10 ⇄ 20 ⇄ 30` → `30 ⇄ 20 ⇄ 10`.
**Analogy:** Flipping a two-way street's signage so "forward" and "backward" swap for every block at once.

---

## Medium Problems of LL

### Middle of a LinkedList [TortoiseHare Method]  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/) · 🎥 [YouTube](https://youtu.be/7LjQ57RqgEc?si=ir_rRDio38rhamU_)
**Intuition / Approach:** Move `slow` one step and `fast` two steps; when `fast` reaches the end, `slow` sits at the middle — one pass, no length count.
**Example:** `1 → 2 → 3 → 4 → 5`: slow ends at `3`. For `1→2→3→4`, slow ends at `3` (second middle).
**Analogy:** Two runners on a track — the fast one laps twice as quick, so when they finish the slow one is exactly halfway.

### Reverse a LinkedList [Iterative]  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/reverse-linked-list/) · 🎥 [YouTube](https://youtu.be/D2vI2DNJGd8?si=RCaLSx01qR21IBdh)
**Intuition / Approach:** Keep `prev, cur, next`. Save `next`, point `cur->next = prev`, then slide all three forward. When `cur` is null, `prev` is the new head.
**Example:** `1 → 2 → 3` → `3 → 2 → 1`.
**Analogy:** Reversing a conga line — each dancer turns to hold the person who was behind them.

### Reverse a LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/reverse-linked-list/) · 🎥 [YouTube](https://youtu.be/D2vI2DNJGd8?si=RCaLSx01qR21IBdh)
**Intuition / Approach:** Same reversal, expressible recursively: reverse the rest, then make the next node point back at the current node and set `head->next = nullptr`.
**Example:** `1 → 2 → 3` → recursion reverses `2 → 3` to `3 → 2`, then hooks `1` on the end → `3 → 2 → 1`.
**Analogy:** Undoing a chain of dominoes by standing each one back up in the opposite order.

### Detect a loop in LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/linked-list-cycle/) · 🎥 [YouTube](https://youtu.be/wiOo4DC5GGA?si=zagt6O6tFXc4_3cx)
**Intuition / Approach:** Floyd's tortoise–hare: if `slow` and `fast` (2×) ever meet, there's a cycle; if `fast` reaches null, there isn't. O(n)/O(1).
**Example:** `1 → 2 → 3 → 4 → 2(back)`: fast catches slow inside the loop → cycle detected.
**Analogy:** On a circular track a fast runner eventually laps and bumps into a slow runner; on a straight road they never meet.

### Find the starting point in LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/) · 🎥 [YouTube](https://youtu.be/2Kd0KKmmHFc?si=7UreDPRjRvapeVB0)
**Intuition / Approach:** After the meet, reset one pointer to head; advance both one step at a time. They meet at the cycle's entry (distance identity head→entry == meet→entry).
**Example:** Loop entering at node `2`: after meeting, walking one from head and one from meet lands both on `2`.
**Analogy:** Two hikers on a lollipop-shaped trail — starting from the trailhead and the meeting spot at equal pace, they reunite exactly at the loop's junction.

### Length of loop in LL  🟡 Medium
**Links:** [Article](https://takeuforward.org/linked-list/length-of-loop-in-linked-list) · 🎥 [YouTube](https://youtu.be/I4g1qbkTPus?si=ONktpqewvx57T8pF)
**Intuition / Approach:** Detect the meeting point with Floyd, then keep one pointer fixed and walk the other around the loop counting steps until it returns.
**Example:** Loop `3 → 4 → 5 → 3`: from the meeting node, counting back to itself gives length 3.
**Analogy:** Standing on a circular track and counting your steps until you return to the exact spot you started.

### Check if LL is palindrome or not  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/palindrome-linked-list/) · 🎥 [YouTube](https://youtu.be/lRY_G-u_8jk?si=BpM8hRYvXSYyjl-G)
**Intuition / Approach:** Find the middle (fast/slow), reverse the second half, then compare the two halves node by node. Optionally restore the list.
**Example:** `1 → 2 → 2 → 1`: reverse second half `2 → 1` to `1 → 2`; compare with first half `1 → 2` → equal → palindrome.
**Analogy:** Folding a strip of paper in half — a palindrome is when the printed letters line up perfectly on top of each other.

### Segregate odd and even nodes in Linked List  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/odd-even-linked-list/) · 🎥 [YouTube](https://youtu.be/qf6qp7GzD5Q?si=JozAyXUdT8EJMSCQ)
**Intuition / Approach:** Group nodes at **odd positions** into one chain and **even positions** into another, then attach the even chain after the odd chain. O(n)/O(1).
**Example:** `1 → 2 → 3 → 4 → 5` → odd-positions `1 → 3 → 5`, even `2 → 4` → `1 → 3 → 5 → 2 → 4`.
**Analogy:** Splitting a line of people into "odd-numbered tickets" and "even-numbered tickets", then having all odds board first.

### Remove Nth node from the back of the LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) · 🎥 [YouTube](https://youtu.be/3kMKYQ2wNIU?si=DtFDnPU7z9HMz_GM)
**Intuition / Approach:** Advance a `fast` pointer N nodes ahead, then move `fast` and `slow` together until `fast` hits the end; `slow` stops just before the target. Use a dummy head to handle removing the first node.
**Example:** `1 → 2 → 3 → 4 → 5`, N=2 → remove `4` → `1 → 2 → 3 → 5`.
**Analogy:** Two people walking a fixed 2-step gap apart; when the leader steps off the curb, the follower is exactly at the node to remove.

### Delete the middle node in LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/) · 🎥 [YouTube](https://youtu.be/ePpV-_pfOeI?si=Au9GsZkVO57j6SiN)
**Intuition / Approach:** Use slow/fast but let slow start one behind (or advance fast first) so slow lands on the node *before* the middle, then splice the middle out.
**Example:** `1 → 2 → 3 → 4`: middle is `3`; delete it → `1 → 2 → 4`.
**Analogy:** Pulling the center bead off a necklace and re-tying the two loose ends together.

### Sort LL  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/sort-list/) · 🎥 [YouTube](https://youtu.be/8ocB7a_c-Cc?si=Gv-Y8q8-WyARoV35)
**Intuition / Approach:** Merge sort on the list: split at the middle (fast/slow), recursively sort each half, then merge two sorted lists. O(n log n) time, O(log n) recursion space.
**Example:** `4 → 2 → 1 → 3` → split → sort halves `2 → 4` and `1 → 3` → merge → `1 → 2 → 3 → 4`.
**Analogy:** Sorting a deck by repeatedly cutting it in half, sorting each pile, then shuffling the two sorted piles together in order.

### Sort a Linked List of 0's 1's and 2's  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/sort-a-linked-list-of-0s-1s-and-2s-by-changing-links) · 🎥 [YouTube](https://youtu.be/gRII7LhdJWc?si=l3qRC7w3NhY7OAqw)
**Intuition / Approach:** One pass distributing nodes into three separate lists (zeros, ones, twos), then concatenate them. O(n)/O(1). (Dutch-flag by relinking, not swapping values.)
**Example:** `1 → 0 → 2 → 1 → 0` → zeros `0 → 0`, ones `1 → 1`, twos `2` → `0 → 0 → 1 → 1 → 2`.
**Analogy:** Sorting mixed laundry into three baskets (whites, colors, darks), then stacking the baskets in order.

### Find the intersection point of Y LL  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists/) · 🎥 [YouTube](https://youtu.be/0DYoPz2Tpt4?si=L-uJs5yXUxj4VJM2)
**Intuition / Approach:** Two pointers start at the two heads; when one hits null, redirect it to the other head. After at most two passes they align at the intersection (or both reach null). O(n+m)/O(1).
**Example:** Lists share tail `8 → 4 → 5`; the switching pointers meet at node `8`.
**Analogy:** Two commuters on different-length routes that merge into one highway; by swapping starting points they synchronize at the merge ramp.

### Add one to a number represented by LL  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/add-1-to-a-number-represented-by-ll) · 🎥 [YouTube](https://youtu.be/aXQWhbvT3w0?si=uRgU9S4r5cVmnUy7)
**Intuition / Approach:** Reverse the list (so units are first), add 1 with carry propagation, then reverse back. Or use recursion returning a carry from the tail.
**Example:** `1 → 2 → 9` (129) + 1 → `1 → 3 → 0` (130).
**Analogy:** Adding 1 to a car odometer — the last wheel rolls over 9 to 0 and nudges the next wheel up.

### Add two numbers in Linked List  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/add-two-numbers/) · 🎥 [YouTube](https://www.youtube.com/watch?v=LBVsXSMOIk4&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=32)
**Intuition / Approach:** Digits are stored least-significant-first. Walk both lists together, sum digit + carry, create a result node with `sum % 10`, carry `sum / 10`. Use a dummy head.
**Example:** `2 → 4 → 3` (342) + `5 → 6 → 4` (465) → `7 → 0 → 8` (807).
**Analogy:** Grade-school column addition, but reading the digits right-to-left because that's the order they arrive.

---

## Medium Problems of DLL

### Delete all occurrences of a key in DLL  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/delete-all-occurrences-of-a-key-in-dll) · 🎥 [YouTube](https://youtu.be/Mh0NH_SD92k?si=tCYshBRi1upMqSVz)
**Intuition / Approach:** Traverse; whenever `cur->data == key`, bridge `cur->prev` and `cur->next` (handle head), free `cur`, and continue. The `prev` pointer makes splicing O(1).
**Example:** `1 ⇄ 2 ⇄ 3 ⇄ 2 ⇄ 4`, key=2 → `1 ⇄ 3 ⇄ 4`.
**Analogy:** Removing every defective bead of one color from a two-sided beaded chain, re-tying neighbors each time.

### Find Pairs with Given Sum in Doubly Linked List  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/find-pairs-with-given-sum-in-doubly-linked-list) · 🎥 [YouTube](https://youtu.be/YitR4dQsddE?si=iZAC259hdngV_OxC)
**Intuition / Approach:** On a **sorted** DLL, use two pointers `left` at head and `right` at tail. If sum < K move `left` forward; if > K move `right` back; if equal record and shrink both. O(n)/O(1).
**Example:** `1 ⇄ 2 ⇄ 3 ⇄ 4 ⇄ 5`, K=6 → pairs (1,5) and (2,4).
**Analogy:** Two people closing in from both ends of a sorted shelf until their picks add up to the target price.

### Remove duplicates from sorted DLL  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/remove-duplicates-from-sorted-dll) · 🎥 [YouTube](https://youtu.be/YJKVTnOJXSY?si=AsZoNUoewetsBjr0)
**Intuition / Approach:** Because it's sorted, duplicates are adjacent. While `cur->next` has the same value, unlink and delete that neighbor, fixing `prev` links. O(n)/O(1).
**Example:** `1 ⇄ 1 ⇄ 2 ⇄ 3 ⇄ 3` → `1 ⇄ 2 ⇄ 3`.
**Analogy:** Skimming duplicate consecutive names off a sorted guest list, keeping just the first of each run.

---

## Hard Problems of LL

### Reverse LL in group of given size K  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/) · 🎥 [YouTube](https://youtu.be/lIar1skcQYI?si=_jFghHKX4eaK36a1)
**Intuition / Approach:** Check that K nodes remain; if so reverse that block and recursively (or iteratively) attach the reversed remainder; if fewer than K remain, leave them untouched. O(n)/O(1).
**Example:** `1 → 2 → 3 → 4 → 5`, K=2 → `2 → 1 → 4 → 3 → 5`.
**Analogy:** Flipping pancakes in fixed-size stacks of K; a leftover stack smaller than K stays as-is.

### Rotate a LL  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/rotate-list/description/) · 🎥 [YouTube](https://youtu.be/uT7YI7XbTY8?si=ZaChW3a68c_v54Is)
**Intuition / Approach:** Connect tail to head to form a ring, compute `k %= len`, walk `len - k` steps to the new tail, break the ring there → new head. O(n)/O(1).
**Example:** `1 → 2 → 3 → 4 → 5`, k=2 → `4 → 5 → 1 → 2 → 3`.
**Analogy:** Rotating a Ferris wheel by k seats — the same cabins, just a shifted starting point.

### Flattening of LL  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/flattening-a-linked-list/) · 🎥 [YouTube](https://youtu.be/ykelywHJWLg?si=InMg9MmTHzY22NSR)
**Intuition / Approach:** Each node has a `next` (right) and a sorted `bottom` (down) list. Merge the bottom lists pairwise from right to left (like merging sorted lists), producing one fully sorted bottom chain.
**Example:** Columns `3→(bottom)6`, `2→(bottom)10`, `1→(bottom)4` → merged sorted bottom: `1 → 2 → 3 → 4 → 6 → 10`.
**Analogy:** Merging several already-sorted card columns into one long sorted column, combining two at a time.

### Clone a LL with random and next pointer  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/copy-list-with-random-pointer/) · 🎥 [YouTube](https://youtu.be/q570bKdrnlw?si=epZtpWvtNwuTf23o)
**Intuition / Approach:** Interleave a copy after each original (`A → A' → B → B' …`). Set each copy's `random = orig->random->next`. Finally detach the copies to restore both lists. O(n)/O(1) extra.
**Example:** `A(rand→C) → B(rand→A) → C(rand→B)`: after interleaving and wiring randoms, split out `A' → B' → C'` as a faithful deep copy.
**Analogy:** Photocopying each page and clipping the copy right behind the original, so you can point each copy's cross-reference at the copy of the page it referenced — then separate the two booklets.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|------------|---------|---------------|
| 1 | Introduction to Singly LinkedList | 🟢 Easy | 1D LinkedList | [Article](https://takeuforward.org/linked-list/linked-list-introduction) |
| 2 | Insertion at the head of Linked List | 🟢 Easy | 1D LinkedList | [Article](https://takeuforward.org/linked-list/insert-at-the-head-of-a-linked-list) |
| 3 | Deletion of the head of LL | 🟢 Easy | 1D LinkedList | [LeetCode](https://leetcode.com/problems/delete-node-in-a-linked-list/) |
| 4 | Find the length of the Linked List | 🟢 Easy | 1D LinkedList | [Article](https://takeuforward.org/linked-list/find-the-length-of-a-linked-list) |
| 5 | Search in Linked List | 🟡 Medium | 1D LinkedList | [Article](https://takeuforward.org/linked-list/search-an-element-in-a-linked-list) |
| 6 | Introduction to Doubly LL | 🟢 Easy | Doubly LinkedList | [Article](https://takeuforward.org/linked-list/introduction-to-doubly-linked-list) |
| 7 | Insert node before head in Doubly Linked List | 🟢 Easy | Doubly LinkedList | [Article](https://takeuforward.org/data-structure/insert-at-end-of-doubly-linked-list/) |
| 8 | Delete head of Doubly Linked List | 🟢 Easy | Doubly LinkedList | [Article](https://takeuforward.org/data-structure/delete-last-node-of-a-doubly-linked-list/) |
| 9 | Reverse a Doubly Linked List | 🟡 Medium | Doubly LinkedList | [Article](https://takeuforward.org/data-structure/reverse-a-doubly-linked-list/) |
| 10 | Middle of a LinkedList [TortoiseHare Method] | 🟢 Easy | Medium LL | [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/) |
| 11 | Reverse a LinkedList [Iterative] | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/reverse-linked-list/) |
| 12 | Reverse a LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/reverse-linked-list/) |
| 13 | Detect a loop in LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/linked-list-cycle/) |
| 14 | Find the starting point in LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/) |
| 15 | Length of loop in LL | 🟡 Medium | Medium LL | [Article](https://takeuforward.org/linked-list/length-of-loop-in-linked-list) |
| 16 | Check if LL is palindrome or not | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/palindrome-linked-list/) |
| 17 | Segregate odd and even nodes in Linked List | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/odd-even-linked-list/) |
| 18 | Remove Nth node from the back of the LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) |
| 19 | Delete the middle node in LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/) |
| 20 | Sort LL | 🔴 Hard | Medium LL | [LeetCode](https://leetcode.com/problems/sort-list/) |
| 21 | Sort a Linked List of 0's 1's and 2's | 🟡 Medium | Medium LL | [Article](https://takeuforward.org/data-structure/sort-a-linked-list-of-0s-1s-and-2s-by-changing-links) |
| 22 | Find the intersection point of Y LL | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists/) |
| 23 | Add one to a number represented by LL | 🟡 Medium | Medium LL | [Article](https://takeuforward.org/data-structure/add-1-to-a-number-represented-by-ll) |
| 24 | Add two numbers in Linked List | 🟡 Medium | Medium LL | [LeetCode](https://leetcode.com/problems/add-two-numbers/) |
| 25 | Delete all occurrences of a key in DLL | 🔴 Hard | Medium DLL | [Article](https://takeuforward.org/data-structure/delete-all-occurrences-of-a-key-in-dll) |
| 26 | Find Pairs with Given Sum in Doubly Linked List | 🟡 Medium | Medium DLL | [Article](https://takeuforward.org/data-structure/find-pairs-with-given-sum-in-doubly-linked-list) |
| 27 | Remove duplicates from sorted DLL | 🔴 Hard | Medium DLL | [Article](https://takeuforward.org/data-structure/remove-duplicates-from-sorted-dll) |
| 28 | Reverse LL in group of given size K | 🔴 Hard | Hard LL | [LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/) |
| 29 | Rotate a LL | 🔴 Hard | Hard LL | [LeetCode](https://leetcode.com/problems/rotate-list/description/) |
| 30 | Flattening of LL | 🔴 Hard | Hard LL | [Article](https://takeuforward.org/data-structure/flattening-a-linked-list/) |
| 31 | Clone a LL with random and next pointer | 🔴 Hard | Hard LL | [LeetCode](https://leetcode.com/problems/copy-list-with-random-pointer/) |
