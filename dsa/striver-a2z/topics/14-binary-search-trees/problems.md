# Binary Search Trees — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems (by Pattern)](./problems.md) · [Resources & References](./resources.md)

> Problems are **grouped by pattern** (the data's sub-steps). Every problem from the topic appears exactly once, each with intuition, a worked example, and a memorable analogy. Difficulty key: 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Concepts

### Introduction to BST  🟢

**Links:** [Article](https://takeuforward.org/binary-search-tree/introduction-to-binary-search-trees/) · 🎥 [YouTube](https://youtu.be/p7-9UvDQZ3w)

**Intuition / Approach:** A BST is a binary tree with the ordering invariant — left subtree keys < node < right subtree keys — applied recursively. This makes search/insert/delete run in O(h). The defining consequence: an inorder traversal prints keys in sorted order.

**Example:** Insert `8,3,10,1,6` in order → root 8; 3 goes left; 10 goes right; 1 goes left-of-3; 6 goes right-of-3. Inorder → `1 3 6 8 10` (sorted). ✅

**Analogy:** A well-organized library where every shelf's left side holds "earlier" call numbers and the right side "later" ones — you never scan the whole library, you just keep turning left or right.

*Complexity:* operations O(h); O(log n) balanced, O(n) skewed.

### Search in a Binary Search Tree  🟢

**Links:** [LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/KcNt6v_56cc)

**Intuition / Approach:** Compare the target with the current node. Equal → found; smaller → go left; larger → go right. Repeat until match or `null`. No backtracking needed.

**Example:** Find `10` in `[8,3,10,1,6,null,14]`: at 8, 10>8 → right to 10 → equal → return that subtree. ✅

**Analogy:** A phone-book binary search: open the middle, decide "earlier or later", and discard the half you don't need.

*Complexity:* O(h) time, O(1) iterative space.

### Find Min/Max in BST  🟢

**Links:** [Article](https://takeuforward.org/data-structure/find-minmax-in-a-bst)

**Intuition / Approach:** The smallest key is the leftmost node — keep going left until there's no left child. The largest is the rightmost — keep going right. No comparisons needed beyond following pointers.

**Example:** In `[8,3,10,1,6,null,14]`: min = go left 8→3→1 (no left) → **1**; max = go right 8→10→14 (no right) → **14**. ✅

**Analogy:** In a sorted spiral staircase, the bottom-left step is the lowest floor and the top-right step is the highest — just walk to the corner.

*Complexity:* O(h) time, O(1) space.

---

## Practice Problems

### Floor and Ceil in a BST  🟢

**Links:** 🎥 [YouTube](https://www.youtube.com/watch?v=xm_W1ub-K-w&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=43)

**Intuition / Approach:** Floor = largest key ≤ x; Ceil = smallest key ≥ x. Walk down: if `node->val == x` it's both; if `node->val < x`, it's a floor candidate, go right for something bigger; if `node->val > x`, it's a ceil candidate, go left. Carry the best candidate.

**Example:** Tree keys `{2,5,8,10,14}`, find floor & ceil of `7`: at 8→ceil-candidate go left; at 5→floor-candidate go right; end. Floor=**5**, Ceil=**8**. ✅

**Analogy:** Finding the nearest lower and upper floor buttons in an elevator when your exact floor isn't a stop.

*Complexity:* O(h) time.

### Floor in a Binary Search Tree  🟢

**Links:** [Article](https://takeuforward.org/binary-search-tree/floor-in-a-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/xm_W1ub-K-w)

**Intuition / Approach:** Track a `floor` answer while walking. If `node->val == x` return it. If `node->val <= x`, record it as the best-so-far and move right (hunting for a bigger valid value). If `node->val > x`, move left.

**Example:** Keys `{2,5,8,10,14}`, floor of `9`: at 8→record 8, go right; at 10→too big, go left; end → **8**. ✅

**Analogy:** Water level rising toward `x` — the floor is the highest stone still under the surface.

*Complexity:* O(h) time, O(1) space.

### Insert a given node in BST  🟡

**Links:** [LeetCode](https://leetcode.com/problems/insert-into-a-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/FiFiNvM29ps)

**Intuition / Approach:** A new key always ends up as a **leaf**. Walk the BST as if searching for the key; when you fall off the tree (hit a null child), attach a new node there. Existing structure is untouched.

**Example:** Insert `5` into `[4,2,7,1,3]`: 5>4 → right to 7; 5<7 → left of 7 is null → attach 5 there. ✅

**Analogy:** Filing a new document in an alphabetized cabinet — you slide to the exact empty slot where it belongs and drop it in; nothing else moves.

*Complexity:* O(h) time.

### Delete a node in BST  🟡

**Links:** [LeetCode](https://leetcode.com/problems/delete-node-in-a-bst/) · 🎥 [YouTube](https://youtu.be/kouxiP_H5WE)

**Intuition / Approach:** Find the node. Leaf → just remove. One child → replace node with that child. Two children → copy the **inorder successor** (min of right subtree) into the node, then delete that successor from the right subtree. This preserves ordering.

**Example:** Delete `3` (two children) in `[5,3,6,2,4,null,7]`: successor = min(right of 3) = 4; copy 4 up, delete original 4 → tree `[5,4,6,2,null,null,7]`. ✅

**Analogy:** A manager leaves; you promote the *next most senior* junior into the seat so the org chart stays ordered.

*Complexity:* O(h) time.

### Kth Smallest and Largest element in BST  🟡

**Links:** [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) · 🎥 [YouTube](https://youtu.be/9TJYWh0adfk)

**Intuition / Approach:** Inorder traversal yields ascending order — the k-th visited node is the k-th smallest. For k-th largest, do reverse inorder (Right→Node→Left) or use `size - k + 1`. Stop early once you hit the k-th.

**Example:** Tree keys → inorder `[1,3,4,6,7,8,10]`, k=3 → 3rd element = **4**; k-th largest with k=2 → reverse inorder 10,8 → **8**. ✅

**Analogy:** Reading a sorted leaderboard top-down for smallest, bottom-up for largest — count off until you reach rank k.

*Complexity:* O(h + k) with early stop; O(n) worst; O(h) space.

### Check if a tree is a BST or not  🟡

**Links:** [LeetCode](https://leetcode.com/problems/validate-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/f-sj7I5oXEI)

**Intuition / Approach:** The invariant is global. Recurse carrying an allowed open range `(low, high)`; each node must satisfy `low < val < high`, then recurse left with `(low,val)` and right with `(val,high)`. Alternatively verify the inorder sequence is strictly increasing.

**Example:** `[5,1,4,null,null,3,6]`: node 3 lives in the right subtree of 5, so its bound is `(5,∞)`, but 3<5 → invalid. Output **false**. ✅

**Analogy:** Passport control at every border: each traveler must fall inside the range allowed by *all* ancestors above them, not just their immediate parent.

*Complexity:* O(n) time, O(h) space.

### LCA in BST  🟡

**Links:** [LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/cX_kPV_foZc)

**Intuition / Approach:** Use the ordering. If both targets are smaller than the node, LCA is in the left subtree; if both larger, go right; the first node where they **split** (one on each side, or one equals the node) is the LCA.

**Example:** LCA of `2` and `8` in `[6,2,8,0,4,7,9]`: at 6, 2<6 and 8>6 → split → LCA = **6**. ✅

**Analogy:** Two hikers descending a fork-filled trail — the last shared junction before their paths diverge is their common ancestor.

*Complexity:* O(h) time, O(1) space.

### Construct a BST from a preorder traversal  🟡

**Links:** [LeetCode](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/) · 🎥 [YouTube](https://youtu.be/UmJT3j26t1I)

**Intuition / Approach:** Preorder = Node, then left subtree, then right subtree. Rebuild by recursing with an **upper bound**: the first element becomes the node; keep consuming elements smaller than the bound for the left subtree, the rest (until the current node's value bound) for the right. O(n) with a running index.

**Example:** Preorder `[8,5,1,7,10,12]` → 8 root; 5,1,7 (<8) build left; 10,12 build right → BST whose inorder is `1,5,7,8,10,12`. ✅

**Analogy:** Following a treasure-map's ordered list of instructions where each "go here first" plants a marker and its bound tells you when a branch ends.

*Complexity:* O(n) time, O(h) space.

### Inorder Successor/Predecessor in BST  🟡

**Links:** [LeetCode](https://leetcode.com/problems/inorder-successor-in-bst/) · 🎥 [YouTube](https://youtu.be/SXKAD2svfmI)

**Intuition / Approach:** Successor of key = smallest key strictly greater. Walk down: when `node->val > key`, record it as a candidate and go left (seeking a tighter one); else go right. Predecessor is symmetric (largest key < target). No parent pointers needed.

**Example:** Keys inorder `[2,5,8,10,14]`, successor of `8`: at 10→candidate, go left; at 5→go right; end → **10**. Predecessor of `8` → **5**. ✅

**Analogy:** In a sorted queue, your successor is simply the next person's ticket number after yours — you slide right and grab the nearest bigger one.

*Complexity:* O(h) time.

### Merge 2 BST's  🔴

**Links:** [LeetCode](https://leetcode.com/problems/binary-search-tree-iterator/) · 🎥 [YouTube](https://youtu.be/D2jMcmxU4bs)

**Intuition / Approach:** (Striver pairs this with the **BST Iterator** design.) A BST Iterator exposes `next()`/`hasNext()` giving keys in ascending order using O(h) memory via a controlled stack of leftmost nodes. To merge two BSTs, run two iterators, merge their sorted streams (like merge-sort's merge), then build a balanced BST from the combined sorted list.

**Example:** BST A inorder `[1,3,5]`, BST B inorder `[2,4]` → merged sorted `[1,2,3,4,5]` → build balanced BST rooted at 3. ✅

**Analogy:** Merging two already-sorted playlists into one ordered playlist by repeatedly taking the smaller "next song" from either list.

*Complexity:* O(n₁+n₂) time, O(h) iterator space.

### Two Sum In BST | Check if there exists a pair with Sum K  🔴

**Links:** [LeetCode](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/) · 🎥 [YouTube](https://youtu.be/ssL3sHwPeb4)

**Intuition / Approach:** Because inorder is sorted, apply the classic **two-pointer**: one BST iterator gives ascending values (`left`), a reverse iterator gives descending (`right`). If `left+right == K` found; if `<K` advance the ascending one; if `>K` advance the descending one. O(n) time, O(h) space — better than a hash set's O(n) space.

**Example:** BST inorder `[2,3,4,6,7]`, K=9: left=2,right=7 → 9 → **true**. ✅

**Analogy:** Two people walking toward each other along a sorted number line — step the low one up or the high one down until their sum lands on the target.

*Complexity:* O(n) time, O(h) space.

### Correct BST with two nodes swapped  🔴

**Links:** [LeetCode](https://leetcode.com/problems/recover-binary-search-tree/) · 🎥 [YouTube](https://youtu.be/ZWGW7FminDM)

**Intuition / Approach:** In a correct BST inorder is strictly increasing; swapping two nodes creates one or two "descents." Do an inorder scan tracking `prev`. First violation → `first = prev`, `middle = current`. Second violation → `last = current`. Swap `first` with (`last` if it exists, else `middle`).

**Example:** Inorder becomes `1 3 2 4` (adjacent swap): one violation at 3>2 → swap 3 and 2 → `1 2 3 4`. ✅

**Analogy:** A sorted bookshelf where two books got swapped — scan left to right, spot where order breaks, and swap the two offenders back.

*Complexity:* O(n) time, O(h) space (Morris → O(1) space).

### Largest BST in Binary Tree  🔴

**Links:** [LeetCode](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/) · 🎥 [YouTube](https://youtu.be/X0oXMdtUDwo)

**Intuition / Approach:** Postorder bottom-up: each node returns `{min, max, size, isBST}` (and sum for the max-sum variant). A node forms a BST iff both children are BSTs and `leftMax < val < rightMin`; then size = left+right+1. Track the global best size (or max sum). O(n) single pass.

**Example:** In a mostly-invalid tree, a subtree `[3,1,4]` is valid (size 3) while its parent `[10,3,4...]` breaks the rule → answer = **3** (largest valid BST subtree). ✅

**Analogy:** Scanning a family tree for the biggest branch where everyone still follows the "left-younger, right-older" rule — you certify each branch from the leaves up.

*Complexity:* O(n) time, O(h) space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Introduction to BST | 🟢 Easy | Concepts | [Article](https://takeuforward.org/binary-search-tree/introduction-to-binary-search-trees/) |
| 2 | Search in a Binary Search Tree | 🟢 Easy | Concepts | [LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/) |
| 3 | Find Min/Max in BST | 🟢 Easy | Concepts | [Article](https://takeuforward.org/data-structure/find-minmax-in-a-bst) |
| 4 | Floor and Ceil in a BST | 🟢 Easy | Practice Problems | [YouTube](https://www.youtube.com/watch?v=xm_W1ub-K-w&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=43) |
| 5 | Floor in a Binary Search Tree | 🟢 Easy | Practice Problems | [Article](https://takeuforward.org/binary-search-tree/floor-in-a-binary-search-tree/) |
| 6 | Insert a given node in BST | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/insert-into-a-binary-search-tree/) |
| 7 | Delete a node in BST | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/delete-node-in-a-bst/) |
| 8 | Kth Smallest and Largest element in BST | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) |
| 9 | Check if a tree is a BST or not | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/validate-binary-search-tree/) |
| 10 | LCA in BST | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) |
| 11 | Construct a BST from a preorder traversal | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/) |
| 12 | Inorder Successor/Predecessor in BST | 🟡 Medium | Practice Problems | [LeetCode](https://leetcode.com/problems/inorder-successor-in-bst/) |
| 13 | Merge 2 BST's | 🔴 Hard | Practice Problems | [LeetCode](https://leetcode.com/problems/binary-search-tree-iterator/) |
| 14 | Two Sum In BST | 🔴 Hard | Practice Problems | [LeetCode](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/) |
| 15 | Correct BST with two nodes swapped | 🔴 Hard | Practice Problems | [LeetCode](https://leetcode.com/problems/recover-binary-search-tree/) |
| 16 | Largest BST in Binary Tree | 🔴 Hard | Practice Problems | [LeetCode](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/) |
