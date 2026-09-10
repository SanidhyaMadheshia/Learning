# Binary Trees — Resources & References

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver's Tree Series — Tree Data Structure (takeUforward)](https://takeuforward.org/data-structure/strivers-tree-series-tree-data-structure) — the canonical A2Z tree series landing page with every video/article in order.
- [Introduction to Trees (takeUforward)](https://youtu.be/_ANrF3FJm7I) — vocabulary, node types, and tree families.
- [Preorder / Inorder / Postorder in one traversal (Striver)](https://youtu.be/ySp2epYvgTE) — the state-counter stack trick.
- [Iterative Preorder Traversal (Striver)](https://youtu.be/Bfqd8BsPVuw) — stack-based DFS without recursion.
- [Level Order Traversal (Striver)](https://youtu.be/EoAsWbO7sqg) — BFS level-by-level template.
- [Diameter of Binary Tree (Striver)](https://youtu.be/Rezetez59Nk) — the bottom-up height+global-max pattern.
- [Maximum Path Sum (Striver)](https://youtu.be/WszrfSwMz58) — clamping negative gains, global answer.
- [LCA in Binary Tree (Striver)](https://youtu.be/_-QHfMDde90) — the single-pass bubbling approach.
- [Nodes at distance K (Striver)](https://youtu.be/i9ORlEy6EsI) — parent map + BFS.
- [Construct BT from Preorder & Inorder (Striver)](https://youtu.be/aZNaLrVebKQ) — index-splitting with a hashmap.
- [Serialize & Deserialize (Striver)](https://youtu.be/-YbXySKJsX8) — BFS encoding with null markers.
- [Morris Traversal — Inorder & Preorder (Striver)](https://youtu.be/80Zug6D1_r4) — O(1) space threaded traversal.

---

## 📝 Articles & Tutorials

- [Strivers A2Z DSA Course/Sheet](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the full ordered sheet this topic belongs to.
- [Introduction to Trees (takeUforward article)](https://takeuforward.org/binary-tree/introduction-to-trees) — foundational concepts in text form.
- [Preorder, Inorder, Postorder in one traversal (takeUforward)](https://takeuforward.org/data-structure/preorder-inorder-postorder-traversals-in-one-traversal/) — deep dive on the combined traversal.
- [Boundary Traversal of a Binary Tree (takeUforward)](https://takeuforward.org/data-structure/boundary-traversal-of-a-binary-tree/) — the three-part anti-clockwise boundary.
- [Vertical Order Traversal (takeUforward)](https://takeuforward.org/data-structure/vertical-order-traversal-of-binary-tree/) — column/row bookkeeping with maps.
- [Morris Traversal for Inorder (GeeksforGeeks)](https://www.geeksforgeeks.org/dsa/level-order-traversal-of-binary-tree-using-morris-traversal/) — threaded-tree explanation and code.
- [Morris Traversal for Preorder (GeeksforGeeks)](https://www.geeksforgeeks.org/dsa/morris-traversal-for-preorder/) — when to emit during threading.
- [Serialize and De-serialize a Binary Tree (takeUforward)](https://takeuforward.org/data-structure/serialize-and-deserialize-a-binary-tree/) — encoding/decoding strategy.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — DFS & BFS traversal](https://visualgo.net/en/dfsbfs) — animated depth-first and breadth-first traversal on trees/graphs.
- [DSA Visualizer — Morris (O(1) Space) Tree Traversal](https://dsavisualizer.in/visualizer/trees/traversal/morris) — step-by-step animation of threading and un-threading.
- [USFCA Binary Search Tree Visualization](https://www.cs.usfca.edu/~galles/visualization/BST.html) — interactive tree operations and traversals (David Galles).

---

## ❓ Most-Asked Interview Questions

1. **What are the three DFS traversals and how do they differ?**
   Preorder = Root→Left→Right, Inorder = Left→Root→Right, Postorder = Left→Right→Root. They differ only in *when* the root is recorded relative to its subtrees.

2. **How do you traverse a tree in O(1) extra space?**
   Morris traversal: thread each node to its inorder predecessor's right pointer, walk without a stack, and restore threads on the second visit.

3. **What is the difference between height and depth?**
   Depth is measured from the root down to a node; height is measured from a node down to its deepest leaf. Tree height = height of the root.

4. **How do you find the diameter of a binary tree?**
   Compute height bottom-up; at each node track `leftHeight + rightHeight` (edges) in a global max. O(n).

5. **Explain the O(n) balanced-tree check.**
   Return height but propagate a `-1` sentinel the moment any node's subtree heights differ by more than 1, short-circuiting the recursion.

6. **How does the single-pass LCA algorithm work in a binary tree (no parent pointers)?**
   Recurse; return a node if it matches p or q. If both left and right calls return non-null, the current node is the LCA; otherwise return the non-null side.

7. **Why can't you uniquely rebuild a tree from preorder + postorder?**
   They can't distinguish a single left child from a single right child. You need **inorder + (pre or post)** to fix left/right splits.

8. **How do you construct a tree from inorder + preorder efficiently?**
   The first preorder value is the root; use a hashmap to find it in inorder in O(1) and split the ranges, recursing on each side. O(n).

9. **How do you find all nodes at distance K from a target?**
   Build a child→parent map, then BFS outward from the target (up + down) with a visited set; nodes reached at level K are the answer.

10. **How do the "views" (top/bottom/left/right) relate to traversals?**
    Top/bottom use BFS with horizontal distance keeping first/last per column; left/right views use BFS keeping first/last node per level.

11. **How do you serialize and deserialize a binary tree?**
    Serialize with BFS or preorder writing values and null markers into a delimited string; deserialize by consuming tokens in the same order to rebuild nodes.

12. **What is the time complexity to count nodes in a *complete* binary tree, and how?**
    O(log²n): if left-height == right-height a subtree is perfect (`2^h − 1`); otherwise recurse both children.

13. **How is level-order traversal implemented, and how do you separate levels?**
    BFS with a queue; capture `queue.size()` at the start of each iteration to process exactly one level before moving on.

14. **When would you choose iterative over recursive traversal?**
    For very deep/skewed trees to avoid stack overflow, or when interviewers explicitly forbid recursion; Morris when O(1) space is required.

15. **What does maximum path sum ask, and what's the trick?**
    The maximum sum along *any* node-to-node path. Each recursion returns the best single downward branch (clamping negatives to 0) while a global max tracks paths bending through each node.

---

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Ch. 10 (Elementary Data Structures) & Ch. 12 (Binary Search Trees)** — formal treatment of tree representations and traversals.
- **Skiena — *The Algorithm Design Manual*, Ch. 3 (Data Structures)** — practical tree usage and trade-offs.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Ch. 3 (Searching)** — tree-based symbol tables and traversal.
- Cross-link: see the repo's [`../../../books/`](../../../books/) directory for local copies/notes if available.
- [Strivers A2Z DSA Course (free)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — structured video + article course covering this step.

---

## 🔗 Official Problem Sources

- [takeUforward — Striver's Tree Series (Step 13)](https://takeuforward.org/data-structure/strivers-tree-series-tree-data-structure) — the official step landing page.
- [LeetCode — Binary Tree tag](https://leetcode.com/tag/binary-tree/) — all binary-tree tagged problems.
- [LeetCode — Tree Explore Card](https://leetcode.com/explore/learn/card/data-structure-tree/) — guided study path for trees.
- Individual problems (exact links used in [problems.md](./problems.md)):
  - [Preorder](https://leetcode.com/problems/binary-tree-preorder-traversal/) · [Inorder](https://leetcode.com/problems/binary-tree-inorder-traversal/) · [Postorder](https://leetcode.com/problems/binary-tree-postorder-traversal/) · [Level Order](https://leetcode.com/problems/binary-tree-level-order-traversal/)
  - [Max Depth](https://leetcode.com/problems/maximum-depth-of-binary-tree/) · [Balanced](https://leetcode.com/problems/balanced-binary-tree/) · [Diameter](https://leetcode.com/problems/diameter-of-binary-tree/) · [Max Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
  - [Same Tree](https://leetcode.com/problems/same-tree/) · [Zigzag](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) · [Boundary](https://leetcode.com/problems/boundary-of-binary-tree/) · [Vertical Order](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)
  - [Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) · [Symmetric](https://leetcode.com/problems/symmetric-tree/) · [LCA](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) · [Max Width](https://leetcode.com/problems/maximum-width-of-binary-tree/)
  - [Distance K](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) · [Count Complete Nodes](https://leetcode.com/problems/count-complete-tree-nodes/) · [Construct Pre+In](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) · [Construct Post+In](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
  - [Serialize/Deserialize](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) · [Flatten](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)
