# Binary Search Trees — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems (by Pattern)](./problems.md) · [Resources & References](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Introduction to BST](https://youtu.be/p7-9UvDQZ3w) — takeUforward's opening lecture on the BST invariant and why operations are O(h).
- [Striver — Search in a BST](https://youtu.be/KcNt6v_56cc) — the downward walk that underlies every BST algorithm.
- [Striver — Floor in a BST](https://youtu.be/xm_W1ub-K-w) — candidate-carrying walk for nearest-value queries.
- [Striver — Insert into a BST](https://youtu.be/FiFiNvM29ps) — attaching a new leaf without disturbing structure.
- [Striver — Delete a node in a BST](https://youtu.be/kouxiP_H5WE) — the inorder-successor splice for two-child deletion.
- [Striver — Kth smallest/largest in BST](https://youtu.be/9TJYWh0adfk) — controlled inorder / reverse inorder.
- [Striver — Validate a BST](https://youtu.be/f-sj7I5oXEI) — the global `(low,high)` bounds technique.
- [Striver — LCA in a BST](https://youtu.be/cX_kPV_foZc) — using ordering to find the split point in O(h).
- [Striver — Construct BST from preorder](https://youtu.be/UmJT3j26t1I) — upper-bound recursion in O(n).
- [Striver — Inorder Successor/Predecessor](https://youtu.be/SXKAD2svfmI) — successor without parent pointers.
- [Striver — BST Iterator](https://youtu.be/D2jMcmxU4bs) — O(h)-memory controlled inorder (basis for merging BSTs).
- [Striver — Two Sum in a BST](https://youtu.be/ssL3sHwPeb4) — two-pointer with ascending + descending iterators.
- [Striver — Recover BST (two swapped nodes)](https://youtu.be/ZWGW7FminDM) — spotting inorder violations.
- [Striver — Largest BST in a Binary Tree](https://youtu.be/X0oXMdtUDwo) — postorder `{min,max,size}` aggregation.
- [takeUforward — A2Z Trees Playlist](https://www.youtube.com/watch?v=xm_W1ub-K-w&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk) — full ordered playlist covering trees and BSTs.

## 📝 Articles & Tutorials

- [takeUforward — Introduction to Binary Search Trees](https://takeuforward.org/binary-search-tree/introduction-to-binary-search-trees/) — Striver's written notes on the invariant.
- [takeUforward — Search in a BST](https://takeuforward.org/data-structure/search-in-a-binary-search-tree-2/) — step-by-step search article.
- [takeUforward — Find Min/Max in a BST](https://takeuforward.org/data-structure/find-minmax-in-a-bst) — leftmost/rightmost walk.
- [takeUforward — Floor in a BST](https://takeuforward.org/binary-search-tree/floor-in-a-binary-search-tree/) — floor/ceil write-up.
- [takeUforward — Kth Largest/Smallest in BST](https://takeuforward.org/data-structure/kth-largest-smallest-element-in-binary-search-tree/) — rank queries.
- [takeUforward — Inorder Successor/Predecessor in BST](https://takeuforward.org/data-structure/inorder-successorpredecessor-in-bst) — successor/predecessor patterns.
- [takeUforward — Two Sum in BST](https://takeuforward.org/data-structure/two-sum-in-bst-check-if-there-exists-a-pair-with-sum-k) — pair-with-sum-K approach.
- [takeUforward — BST Iterator](https://takeuforward.org/data-structure/bst-iterator) — iterator design, used to merge BSTs.
- [GeeksforGeeks — Binary Search Tree (data structure)](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) — canonical overview with complexities.
- [GeeksforGeeks — Introduction to Binary Search Tree](https://www.geeksforgeeks.org/introduction-to-binary-search-tree/) — beginner-friendly intro.
- [GeeksforGeeks — Insertion in a BST](https://www.geeksforgeeks.org/dsa/insertion-in-binary-search-tree/) — insertion walkthrough.
- [GeeksforGeeks — Iterative Delete in a BST](https://www.geeksforgeeks.org/binary-search-tree-set-3-iterative-delete/) — deletion cases including two-child successor.
- [GeeksforGeeks — Handling duplicates in a BST](https://www.geeksforgeeks.org/dsa/how-to-handle-duplicates-in-binary-search-tree/) — conventions for duplicate keys.
- [GeeksforGeeks — Top 50 BST Coding Problems for Interviews](https://www.geeksforgeeks.org/dsa/top-50-binary-search-tree-coding-problems-for-interviews/) — curated practice set.

## 🧮 Visualizers & Tools

- [VisuAlgo — Binary Search Tree / AVL](https://visualgo.net/en/bst) — animated insert/search/delete and traversals; supports AVL balancing.
- [USFCA — BST Visualization](https://www.cs.usfca.edu/~galles/visualization/BST.html) — classic step-by-step operation animator.
- [see-algorithms — BST Visualizer](https://see-algorithms.com/data-structures/BST) — interactive add/remove/search demo.

## ❓ Most-Asked Interview Questions

1. **What defines a BST vs a plain binary tree?** For every node, all left-subtree keys are smaller and all right-subtree keys are larger — recursively. A binary tree has no such ordering.
2. **Why are BST operations O(h) and not O(log n) always?** Each step drops one level, so cost equals height. Height is log n only when balanced; a sorted-insert sequence yields a stick of height n.
3. **How do you validate a BST correctly?** Pass down an allowed `(low, high)` range; each node must satisfy `low < val < high`. Comparing only parent-to-child is wrong because the invariant is global.
4. **How do you delete a node with two children?** Replace its value with the inorder successor (min of the right subtree), then delete that successor from the right subtree.
5. **What is the inorder successor and how do you find it?** The next-larger key. If the node has a right child, it's the min of the right subtree; otherwise it's the lowest ancestor for which the node is in the left subtree.
6. **How do you find the k-th smallest element?** Inorder traversal is sorted; the k-th visited node is the answer. Stop early after k nodes for O(h+k).
7. **Why is inorder traversal so central to BST problems?** It produces keys in sorted order, reducing many problems (k-th, two-sum, recover, validate) to 1-D sorted-array techniques.
8. **How is LCA in a BST cheaper than in a general tree?** Use ordering: if both keys are smaller go left, both larger go right; the split point is the LCA — O(h), no extra storage.
9. **How do you find a pair summing to K in a BST in O(h) space?** Two-pointer with an ascending BST iterator and a descending one; move whichever pointer to approach K. Beats a hash set's O(n) space.
10. **How do you recover a BST with two swapped nodes?** Inorder scan tracking `prev`; the swap causes one or two order violations. Record first/middle/last offenders and swap them back.
11. **How do you build a BST from a preorder traversal in O(n)?** Recurse with an upper bound and a shared index; the first value is the root, values below the bound form the left subtree, the rest the right.
12. **What's the largest-BST-subtree trick?** Postorder aggregation returning `{min, max, size, isBST}`; a node is a BST iff both children are BSTs and `leftMax < val < rightMin`.
13. **How do you get guaranteed O(log n) operations?** Use a self-balancing BST — AVL or Red-Black tree — or a library ordered container like C++ `std::set`/`std::map`.
14. **How do you handle duplicate keys?** Decide a convention: disallow, always go one side, or store a per-node count; state your choice since BSTs are defined on distinct keys.
15. **How does a BST Iterator achieve O(h) memory?** It stores only the current leftmost spine on a stack, pushing the next left-spine after each `next()` — a controlled, lazy inorder traversal.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Ch. 12 "Binary Search Trees"** and Ch. 13 "Red-Black Trees" for balanced variants.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Ch. 3.2/3.3** — BSTs and balanced search trees.
- **Skiena — *The Algorithm Design Manual*, §3.4** — BST operations and trade-offs.
- Local books shelf (if present): [../../../books/](../../../books/)
- Course: [takeUforward A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-sheet-and-most-asked-coding-questions/).

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Sheet (Step 14: BST)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-sheet-and-most-asked-coding-questions/) — the source sheet for this step.
- [LeetCode — Binary Search Tree tag](https://leetcode.com/tag/binary-search-tree/) — all BST-tagged problems.
- [LeetCode — Binary Tree explore card](https://leetcode.com/explore/learn/card/data-structure-tree/) — structured learning path.
- [GeeksforGeeks — Top 50 BST Coding Problems](https://www.geeksforgeeks.org/dsa/top-50-binary-search-tree-coding-problems-for-interviews/) — interview problem index.
