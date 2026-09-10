# Binary Trees — Problems (by Pattern)

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)
>
> Problems are **grouped by pattern** (the sub-steps of the Striver A2Z sheet). Every problem has an intuition, a worked example, and a memory analogy. 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Traversals

### Introduction to Trees  🟢
**Links:** [Article](https://takeuforward.org/binary-tree/introduction-to-trees/) · 🎥 [YouTube](https://youtu.be/_ANrF3FJm7I)

**Intuition / Approach:** Learn the vocabulary — node, root, leaf, height, depth, level — and the family of trees (full, complete, perfect, balanced, skewed). A binary tree limits each node to ≤ 2 children.
**Example:** Tree `1 -> (2,3)`; node `1` is root (depth 0), `2` and `3` are leaves at depth 1; height of tree = 1.
**Analogy:** A family tree where every parent may have at most two kids — grandparents at the top, cousins branching out below.

### Binary Tree Representation in Java  🟢
**Links:** [Article](https://takeuforward.org/binary-tree/binary-tree-representation-in-java/) · 🎥 [YouTube](https://youtu.be/hyLyW7rP24I)

**Intuition / Approach:** Represent a node with a value and two child pointers/references. Build the tree by wiring `root.left` and `root.right`. In C++ it's a `struct TreeNode{int val; TreeNode *left,*right;}`.
**Example:** `Node root = new Node(1); root.left = new Node(2); root.right = new Node(3);` builds a 3-node tree.
**Analogy:** Each node is a box with a label and two strings tied to two smaller boxes beneath it.

### Pre, Post, Inorder in one traversal  🟢
**Links:** [Article](https://takeuforward.org/data-structure/preorder-inorder-postorder-traversals-in-one-traversal/) · 🎥 [YouTube](https://youtu.be/ySp2epYvgTE)

**Intuition / Approach:** Push `(node, state)` onto a stack where `state` counts how many times we've touched the node (1→pre, 2→in, 3→post). Emit into the right list at each state, incrementing the state each visit.
**Example:** For `1->(2,3)`: node 1 seen at state1 (pre), state2 (in after left), state3 (post after right) — one stack pass fills all three lists.
**Analogy:** A tour guide who stamps your passport three times as you enter, pass the desk, and exit — one walk, three records.

### Preorder Traversal  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/) · 🎥 [YouTube](https://youtu.be/RlUu72JrOCQ)

**Intuition / Approach:** Visit **Root → Left → Right**. Recursively record the node before descending. Preorder captures the "top-down" copy of the tree.
**Example:** `1->(2,3)` with `2->(4,5)` → `[1,2,4,5,3]`.
**Analogy:** Reading a table of contents top-first: chapter title before its sub-sections.

### Inorder Traversal of Binary Tree  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) · 🎥 [YouTube](https://youtu.be/Z_NEgBgbRVI)

**Intuition / Approach:** Visit **Left → Root → Right**. For a BST, inorder yields sorted order. Recurse left fully, record root, recurse right.
**Example:** `2->(4,5)`, root `1`, `3` → `[4,2,5,1,3]`.
**Analogy:** Reading a book left-to-right across a two-column page — finish the left column, note the header, then the right.

### Postorder Traversal  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) · 🎥 [YouTube](https://youtu.be/2YBhNLodD8Q)

**Intuition / Approach:** Visit **Left → Right → Root**. The root is recorded last, which is ideal for "process children before parent" tasks (deleting a tree, evaluating expressions).
**Example:** `1->(2,3)`, `2->(4,5)` → `[4,5,2,3,1]`.
**Analogy:** Demolishing a building floor-by-floor — you clear all sub-structures before removing the foundation you stand on.

### Level Order Traversal  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/) · 🎥 [YouTube](https://youtu.be/EoAsWbO7sqg)

**Intuition / Approach:** BFS with a queue. Process `q.size()` nodes per iteration to bucket a whole level, enqueuing children as you go.
**Example:** `1->(2,3)`, `2->(4,5)` → `[[1],[2,3],[4,5]]`.
**Analogy:** Boarding an airplane by row groups — everyone in the same row boards together before the next row.

### Iterative Preorder Traversal of Binary Tree  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/) · 🎥 [YouTube](https://youtu.be/Bfqd8BsPVuw)

**Intuition / Approach:** Use an explicit stack. Pop a node, record it, then push **right first, left second** so left is processed next (LIFO).
**Example:** Push 1 → pop/record 1, push 3 then 2 → pop 2… → `[1,2,4,5,3]`.
**Analogy:** A to-do stack of sticky notes: you handle the top note first, and you place the "must-do-next" note on top last.

### Iterative Inorder Traversal of Binary Tree  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) · 🎥 [YouTube](https://youtu.be/lxTGsVXjwvM)

**Intuition / Approach:** Push all left nodes; when you can't go left, pop → record → move right; repeat until stack empty and curr null.
**Example:** Push 1,2,4 → pop 4,2 (record), go to 5 → pop 5,1,3 → `[4,2,5,1,3]`.
**Analogy:** Walking down a spiral staircase to the bottom-left, then unwinding one step at a time, peeking right at each landing.

### Post-order Traversal of Binary Tree using 2 stack  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) · 🎥 [YouTube](https://youtu.be/2YBhNLodD8Q)

**Intuition / Approach:** Do a modified preorder (Root→Left→Right pushing order) into stack2, which yields **Root→Right→Left**; popping stack2 reverses it into postorder.
**Example:** stack2 fills `[1,3,2,5,4]`; pop reversed → `[4,5,2,3,1]`.
**Analogy:** Writing your itinerary in reverse on scratch paper, then reading the scratch bottom-up to get the true order.

### Post-order Traversal of Binary Tree using 1 stack  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) · 🎥 [YouTube](https://youtu.be/NzIGLLwZBS8)

**Intuition / Approach:** Track a `prev` pointer. Push lefts; peek the top — if its right is unvisited go right, else record it and set `prev`. This visits a node only after both children.
**Example:** For `1->(2,3)` you record 2, then 3, then 1 → `[2,3,1]` (with children first).
**Analogy:** A cautious hiker who only marks a summit "done" after checking both trails branching from it.

### Preorder, Inorder, and Postorder Traversal in one Traversal  🟢
**Links:** [Article](https://takeuforward.org/data-structure/preorder-inorder-postorder-traversals-in-one-traversal/) · 🎥 [YouTube](https://youtu.be/ySp2epYvgTE)

**Intuition / Approach:** Same "state counter" stack trick — each node cycles states 1→2→3, emitting to pre/in/post lists respectively. Produces all three in a single O(n) pass with O(n) space.
**Example:** `1->(2,3)` → pre `[1,2,3]`, in `[2,1,3]`, post `[2,3,1]` from one loop.
**Analogy:** A multi-tracked recorder capturing three commentary channels in one live take of the same walk.

---

## Medium Problems

### Maximum Depth in BT  🟡
**Links:** [LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/) · 🎥 [YouTube](https://youtu.be/eD3tmO66aBA)

**Intuition / Approach:** Bottom-up: `depth = 1 + max(depth(left), depth(right))`, null returns 0. Or BFS counting levels.
**Example:** `1->(2,3)`, `2->4` → depths: leaf 4 gives left path length 3, right 2 → max depth **3**.
**Analogy:** Measuring the tallest root-to-tip branch of a real tree with a tape measure.

### Check for balanced binary tree  🟡
**Links:** [LeetCode](https://leetcode.com/problems/balanced-binary-tree/) · 🎥 [YouTube](https://youtu.be/Yt50Jfbd8Po)

**Intuition / Approach:** Return height but short-circuit with `-1` the moment any node's subtree heights differ by more than 1 — turns the naive O(n²) into O(n).
**Example:** A tree where left height 3, right height 1 at some node → `|3-1|=2 > 1` → **not balanced**.
**Analogy:** A weighing scale under each node — if either pan tips too far, the whole structure is flagged wobbly.

### Diameter of Binary Tree  🟢
**Links:** [LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/) · 🎥 [YouTube](https://youtu.be/Rezetez59Nk)

**Intuition / Approach:** While computing height bottom-up, update a global max with `leftHeight + rightHeight` (path in edges through the node). Answer = largest such sum.
**Example:** `1->(2,3)`, `2->(4,5)` → at node 2, L=1,R=1 → path 2; at node 1, L=2,R=1 → diameter **3**.
**Analogy:** The longest possible walk between two leaves in a park, which may or may not pass through the central fountain (root).

### Maximum path sum  🟡
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum/) · 🎥 [YouTube](https://youtu.be/WszrfSwMz58)

**Intuition / Approach:** Bottom-up: each node returns the best *downward* gain `val + max(0, max(leftGain, rightGain))`; a global max tracks `val + leftGain + rightGain` (a path bending through the node). Clamp negatives to 0.
**Example:** `-10->(9, 20->(15,7))` → best through 20 is `15+20+7=42`, overall **42**.
**Analogy:** Choosing the most profitable route in a road network where some roads charge tolls (negative) you'd rather skip.

### Check if two trees are identical or not  🟡
**Links:** [LeetCode](https://leetcode.com/problems/same-tree/) · 🎥 [YouTube](https://youtu.be/BhuvF_-PWS0)

**Intuition / Approach:** Paired recursion: both null → equal; one null → unequal; else values match AND left subtrees identical AND right subtrees identical.
**Example:** `[1,2,3]` vs `[1,2,3]` → identical; `[1,2]` vs `[1,null,2]` → not identical (structure differs).
**Analogy:** Comparing two org charts position-by-position — same boss, same reports, all the way down.

### Zig Zag or Spiral Traversal  🟡
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) · 🎥 [YouTube](https://youtu.be/3OXWEdlIGl4)

**Intuition / Approach:** Level-order BFS, but reverse the direction of insertion into each level based on a `leftToRight` boolean that flips each level.
**Example:** `1->(2,3)`, `2->(4,5)` → `[[1],[3,2],[4,5]]`.
**Analogy:** A boustrophedon plow — plough one row left-to-right, the next right-to-left, alternating.

### Boundary Traversal  🟡
**Links:** [LeetCode](https://leetcode.com/problems/boundary-of-binary-tree/) · 🎥 [YouTube](https://youtu.be/0ca1nvR0be4)

**Intuition / Approach:** Concatenate three parts anti-clockwise: left boundary (top→down, excluding leaves), all leaves (left→right), right boundary (bottom→up, excluding leaves). Avoid double-counting the root/leaves.
**Example:** A full tree returns root → left edge → leaves → right edge reversed, each node once.
**Analogy:** Tracing the outline of a leaf silhouette with your finger — you follow only the outer edge, not the veins inside.

### Vertical Order Traversal  🟡
**Links:** [LeetCode](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/q_a6lpbKJdw)

**Intuition / Approach:** BFS/DFS tracking `(column, row)`; group nodes by column (root=0, left −1, right +1). Within a column sort by row, then by value for LeetCode ties. Use a `map<col, map<row, multiset<val>>>`.
**Example:** `3->(9, 20->(15,7))` → columns: −1:[9], 0:[3,15], +1:[20], +2:[7] → `[[9],[3,15],[20],[7]]`.
**Analogy:** Sorting mail into vertical pigeonholes by the sender's column position, top to bottom within each slot.

### Top View of BT  🟡
**Links:** [Article](https://takeuforward.org/data-structure/top-view-of-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/Et9OCDNvJ78)

**Intuition / Approach:** BFS with horizontal distance (HD). For each HD, keep the **first** node seen — that's what's visible from directly above. Output columns left→right.
**Example:** `1->(2,3)`, `2->(4,5)`, `3->(6,7)` → HDs give top view `[4,2,1,3,7]`.
**Analogy:** A drone photo looking straight down — you only see the highest node in each vertical strip.

### Bottom view of BT  🟡
**Links:** [Article](https://takeuforward.org/data-structure/bottom-view-of-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/0FtVY6I4pB8)

**Intuition / Approach:** Same HD-BFS, but keep the **last** node seen at each HD (later nodes overwrite earlier) — that's what's visible from below.
**Example:** Same tree → bottom view `[4,2,6,3,7]` (node 6 at HD 0 overwrites 1 and 5 depending on BFS order/level).
**Analogy:** Looking up at the tree from underground — only the lowest node in each vertical strip is visible.

### Right/Left View of Binary Tree  🟡
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-right-side-view/) · 🎥 [YouTube](https://youtu.be/KV4mRzTjlAk)

**Intuition / Approach:** BFS: take the **last** node of each level (right view) or **first** (left view). Or DFS visiting right-first and recording the first node seen per depth.
**Example:** `1->(2,3)`, `2->5` → right view `[1,3,5]`.
**Analogy:** Standing to the right of the tree — you see only the rightmost person in each row.

### Symmetric Binary Tree  🟡
**Links:** [LeetCode](https://leetcode.com/problems/symmetric-tree/) · 🎥 [YouTube](https://www.youtube.com/watch?v=nKggNAiEpBE)

**Intuition / Approach:** Mirror check: compare left subtree with right subtree in *opposite* order — `isMirror(a.left,b.right) && isMirror(a.right,b.left)` with equal values.
**Example:** `[1,2,2,3,4,4,3]` → symmetric; `[1,2,2,null,3,null,3]` → not symmetric.
**Analogy:** Holding a mirror down the middle of a butterfly — both wings must match reflectively.

---

## Hard Problems

### Print root to leaf path in BT  🟡
**Links:** [Article](https://takeuforward.org/data-structure/print-root-to-node-path-in-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/fmflMqVOC7k)

**Intuition / Approach:** DFS carrying the path vector; on reaching the target node (or a leaf) capture the path. Backtrack by popping after recursion so siblings start clean.
**Example:** Find path to `5` in `1->(2->(4,5),3)` → `[1,2,5]`.
**Analogy:** Dropping breadcrumbs as you explore a maze, picking them up when you backtrack a dead end.

### LCA in BT  🔴
**Links:** [LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/_-QHfMDde90)

**Intuition / Approach:** Recurse; return the node if it equals p or q. If both children return non-null, the current node is the LCA; else bubble up the non-null side.
**Example:** In `3->(5,1)` find LCA(5,1) → **3** (both found in different subtrees).
**Analogy:** Two relatives tracing their family trees upward — the first shared ancestor they both hit is the LCA.

### Maximum Width of BT  🟡
**Links:** [LeetCode](https://leetcode.com/problems/maximum-width-of-binary-tree/) · 🎥 [YouTube](https://youtu.be/ZbybYvcVLks)

**Intuition / Approach:** BFS assigning each node an index as if in a complete tree (`left=2i`, `right=2i+1`); width of a level = `last − first + 1`. Normalize indices per level to avoid overflow.
**Example:** `1->(3,2)`, `3->(5,3),` `2->(null,9)` → widest level width = **4** (positions of 5 and 9).
**Analogy:** Measuring the widest shelf in a bookcase by the leftmost and rightmost occupied slots, counting the empty gaps between them.

### Children Sum Property in Binary Tree  🟡
**Links:** [Article](https://takeuforward.org/data-structure/check-for-children-sum-property-in-a-binary-tree/) · 🎥 [YouTube](https://youtu.be/fnmisPM6cVo)

**Intuition / Approach:** For every node, its value must equal the sum of its children's values (leaves/null treated as satisfying). Check recursively; the *convert* variant pushes/pulls values top-down then fixes bottom-up.
**Example:** Node `10->(4,6)` satisfies (4+6=10); `10->(4,5)` violates.
**Analogy:** A household budget where each manager's total must exactly equal the sum of their two team leads' budgets.

### Print all nodes at a distance of K in BT  🔴
**Links:** [LeetCode](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) · 🎥 [YouTube](https://youtu.be/i9ORlEy6EsI)

**Intuition / Approach:** Build a `child→parent` map, then BFS outward from the target (up via parent, down via children), tracking a visited set; nodes reached at distance K are the answer.
**Example:** Target `5`, K=2 in a tree → returns all nodes exactly 2 edges from 5.
**Analogy:** Ripples from a stone dropped in a pond — the ring exactly K units from the splash point.

### Minimum time taken to burn the BT from a given Node  🔴
**Links:** [Article](https://takeuforward.org/data-structure/minimum-time-taken-to-burn-the-binary-tree-from-a-node) · 🎥 [YouTube](https://youtu.be/2r5wLmQfD6g)

**Intuition / Approach:** Same parent-map trick; BFS the fire outward one level per minute; the answer is the number of BFS levels needed to reach the farthest node.
**Example:** Fire starts at a leaf; each minute spreads to adjacent nodes; total minutes = max distance from start.
**Analogy:** A wildfire spreading from an ignition point through connected trees — how many minutes until the last tree catches.

### Count total nodes in a complete BT  🟢
**Links:** [LeetCode](https://leetcode.com/problems/count-complete-tree-nodes/) · 🎥 [YouTube](https://youtu.be/u-yWemKGWO0)

**Intuition / Approach:** For a complete tree, if left-height == right-height the subtree is perfect → `2^h − 1` in O(h). Otherwise recurse on both children. Total O(log²n).
**Example:** A perfect subtree of height 3 → `2^3 − 1 = 7` nodes without visiting each.
**Analogy:** Counting seats in a stadium section that's known-full by multiplying rows × seats instead of counting one by one.

### Requirements needed to construct a unique BT  🟡
**Links:** [Article](https://youtu.be/9GMECGQgWrQ) · 🎥 [YouTube](https://youtu.be/9GMECGQgWrQ)

**Intuition / Approach:** A unique binary tree needs **inorder + (preorder or postorder)**. Preorder+postorder alone is *not* enough (ambiguous for trees with single children). Inorder disambiguates left/right splits.
**Example:** pre `[1,2,3]` + post `[2,3,1]` cannot decide if 2 is left or right of 1; adding inorder fixes it.
**Analogy:** You need both a floor plan (inorder ordering) and a build sequence (pre/post) to reconstruct a house exactly.

### Construct a BT from Preorder and Inorder  🔴
**Links:** [LeetCode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) · 🎥 [YouTube](https://youtu.be/aZNaLrVebKQ)

**Intuition / Approach:** First preorder element is the root; locate it in inorder (via hashmap) to size the left subtree, then recurse on the corresponding pre/in sub-ranges.
**Example:** pre `[3,9,20,15,7]`, in `[9,3,15,20,7]` → root 3, left=[9], right subtree from 20 → rebuilds `3->(9,20->(15,7))`.
**Analogy:** Assembling flat-pack furniture: the manual's first step (preorder root) plus the layout diagram (inorder) tells you which parts go left vs right.

### Construct the Binary Tree from Postorder and Inorder Traversal  🔴
**Links:** [LeetCode](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) · 🎥 [YouTube](https://youtu.be/LgLRTaEMRVc)

**Intuition / Approach:** **Last** postorder element is the root; split inorder around it. Recurse right subtree before left (since postorder ends with root, right precedes it).
**Example:** post `[9,15,7,20,3]`, in `[9,3,15,20,7]` → root 3 (last of post), rebuild same tree as above.
**Analogy:** Reading a project's completion log bottom-up — the last thing finished (root) was built after its sub-parts.

### Serialize and De-serialize BT  🔴
**Links:** [LeetCode](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) · 🎥 [YouTube](https://youtu.be/-YbXySKJsX8)

**Intuition / Approach:** Serialize via BFS/preorder writing values and `#` for nulls into a delimited string. Deserialize by reading tokens in the same order, rebuilding nodes (queue for BFS, or recursion for preorder).
**Example:** `1->(2,3)` → `"1,2,#,#,3,#,#"`; parsing it reconstructs the exact tree.
**Analogy:** Flat-packing a sculpture into a labeled parts list, then rebuilding it identically from the list.

### Morris Preorder Traversal of a Binary Tree  🔴
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) · 🎥 [YouTube](https://youtu.be/80Zug6D1_r4)

**Intuition / Approach:** Thread each node to its inorder predecessor. **Record the value when creating the thread** (before going left) to get preorder. Un-thread on the second visit. O(1) extra space.
**Example:** `1->(2,3)`, `2->(4,5)` → emits `[1,2,4,5,3]` with no stack.
**Analogy:** Tying temporary string shortcuts between rooms so you can wander the whole house without a map, then untying them as you leave.

### Morris Inorder Traversal of a Binary Tree  🔴
**Links:** [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) · 🎥 [YouTube](https://youtu.be/80Zug6D1_r4)

**Intuition / Approach:** Same threading, but **record the value when removing the thread** (second visit, after left subtree done) to get inorder. O(1) space, O(n) time.
**Example:** Same tree → emits `[4,2,5,1,3]`.
**Analogy:** Same string-shortcut house tour, but you jot down each room's name only as you *untie* its string on the way back.

### Flatten Binary Tree to Linked List  🟡
**Links:** [LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/) · 🎥 [YouTube](https://youtu.be/sWf7k1x9XR4)

**Intuition / Approach:** Rearrange the tree into a right-skewed "linked list" in preorder. Morris-style: for each node with a left child, find its left subtree's rightmost node, attach the current right subtree there, move left subtree to the right, and null the left. O(1) space.
**Example:** `1->(2->(3,4),5->(_,6))` → `1→2→3→4→5→6` all as right children.
**Analogy:** Unrolling a branching scroll into a single long ribbon, keeping the reading (preorder) sequence intact.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Introduction to Trees | 🟢 Easy | Traversals | [Article](https://takeuforward.org/binary-tree/introduction-to-trees/) |
| 2 | Binary Tree Representation in Java | 🟢 Easy | Traversals | [Article](https://takeuforward.org/binary-tree/binary-tree-representation-in-java/) |
| 3 | Pre, Post, Inorder in one traversal | 🟢 Easy | Traversals | [Article](https://takeuforward.org/data-structure/preorder-inorder-postorder-traversals-in-one-traversal/) |
| 4 | Preorder Traversal | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/) |
| 5 | Inorder Traversal of Binary Tree | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) |
| 6 | Postorder Traversal | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) |
| 7 | Level Order Traversal | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/) |
| 8 | Iterative Preorder Traversal | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/) |
| 9 | Iterative Inorder Traversal | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) |
| 10 | Postorder Traversal using 2 stack | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) |
| 11 | Postorder Traversal using 1 stack | 🟢 Easy | Traversals | [LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/) |
| 12 | Pre, In, Post in one traversal | 🟢 Easy | Traversals | [Article](https://takeuforward.org/data-structure/preorder-inorder-postorder-traversals-in-one-traversal/) |
| 13 | Maximum Depth in BT | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/) |
| 14 | Check for balanced binary tree | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/balanced-binary-tree/) |
| 15 | Diameter of Binary Tree | 🟢 Easy | Medium Problems | [LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/) |
| 16 | Maximum path sum | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum/) |
| 17 | Check if two trees are identical | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/same-tree/) |
| 18 | Zig Zag or Spiral Traversal | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) |
| 19 | Boundary Traversal | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/boundary-of-binary-tree/) |
| 20 | Vertical Order Traversal | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) |
| 21 | Top View of BT | 🟡 Medium | Medium Problems | [Article](https://takeuforward.org/data-structure/top-view-of-a-binary-tree/) |
| 22 | Bottom view of BT | 🟡 Medium | Medium Problems | [Article](https://takeuforward.org/data-structure/bottom-view-of-a-binary-tree/) |
| 23 | Right/Left View of Binary Tree | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/binary-tree-right-side-view/) |
| 24 | Symmetric Binary Tree | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/symmetric-tree/) |
| 25 | Print root to leaf path in BT | 🟡 Medium | Hard Problems | [Article](https://takeuforward.org/data-structure/print-root-to-node-path-in-a-binary-tree/) |
| 26 | LCA in BT | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) |
| 27 | Maximum Width of BT | 🟡 Medium | Hard Problems | [LeetCode](https://leetcode.com/problems/maximum-width-of-binary-tree/) |
| 28 | Children Sum Property | 🟡 Medium | Hard Problems | [Article](https://takeuforward.org/data-structure/check-for-children-sum-property-in-a-binary-tree/) |
| 29 | Nodes at distance K in BT | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) |
| 30 | Minimum time to burn the BT | 🔴 Hard | Hard Problems | [Article](https://takeuforward.org/data-structure/minimum-time-taken-to-burn-the-binary-tree-from-a-node) |
| 31 | Count nodes in complete BT | 🟢 Easy | Hard Problems | [LeetCode](https://leetcode.com/problems/count-complete-tree-nodes/) |
| 32 | Requirements for unique BT | 🟡 Medium | Hard Problems | [YouTube](https://youtu.be/9GMECGQgWrQ) |
| 33 | Construct BT from Preorder & Inorder | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) |
| 34 | Construct BT from Postorder & Inorder | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) |
| 35 | Serialize and De-serialize BT | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) |
| 36 | Morris Preorder Traversal | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) |
| 37 | Morris Inorder Traversal | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/) |
| 38 | Flatten Binary Tree to Linked List | 🟡 Medium | Hard Problems | [LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/) |
