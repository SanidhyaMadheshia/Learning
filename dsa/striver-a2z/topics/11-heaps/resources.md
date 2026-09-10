# Heaps — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver's A2Z DSA Course/Sheet (takeUforward)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the parent course; the Heaps step links each problem's article + video.
- [Introduction to Priority Queues using Binary Heaps — takeUforward](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps) — Striver's canonical heap/priority-queue lesson with the embedded theory video.
- [Blind 75 Solved & Explained — Part 8: Heaps (Medium)](https://medium.com/@ulucozdenvar/ace-your-coding-interview-blind-75-solved-and-explained-part-8-heaps-560ab652094f) — walkthrough of interview heap problems including two-heaps median.
- [Running Median with Heaps — Medium](https://medium.com/@eranda/running-median-with-heaps-829522330e8a) — focused explanation of the two-heaps median technique with worked balancing.

## 📝 Articles & Tutorials

- [GfG — Binary Heap](https://www.geeksforgeeks.org/dsa/binary-heap/) — full reference on min/max heaps, operations, and array representation.
- [GfG — Priority Queue using Binary Heap](https://www.geeksforgeeks.org/dsa/priority-queue-using-binary-heap/) — insert/extractMax/changePriority mechanics with diagrams.
- [GfG — Building Heap from Array](https://www.geeksforgeeks.org/building-heap-from-array/) — why build-heap is `O(n)` and the bottom-up heapify order.
- [GfG — Heap Sort](https://www.geeksforgeeks.org/heap-sort/) — heapsort built on repeated extract-max.
- [GfG — Heap Data Structure for Competitive Programming](https://www.geeksforgeeks.org/competitive-programming/heap-data-structure-for-competitive-programming/) — heap idioms and tricks for contests.
- [Tech Interview Handbook — Heap Cheatsheet](https://www.techinterviewhandbook.org/algorithms/heap/) — concise heap/PQ cheat sheet with time complexities and gotchas.
- [emre.me — Coding Patterns: K-way Merge](https://emre.me/coding-patterns/k-way-merge/) — clean pattern write-up for merging K sorted sequences.
- [Codinginterview.com — K-Way Merge pattern](https://www.codinginterview.com/coding-patterns/k-way-merge/) — the min-heap "waiting room" model for k-way merge.
- [Two Heaps: Min & Max — Mastering the Two-Heaps Pattern (Medium)](https://medium.com/@stephen.joel/two-heaps-median-f28ebc1569d7) — the two-heaps median pattern step by step.
- [LeetCode Discuss — Master HEAP: 4 patterns where the heap is used](https://leetcode.com/discuss/post/1127238/master-heap-understanding-4-patterns-whe-fb8z/) — pattern taxonomy for heap problems.
- [LeetCode Discuss — How to solve ANY heap problem (5 patterns, templates)](https://leetcode.com/discuss/post/8362310/how-to-solve-any-heap-problem-5-patterns-efd2/) — templates including the "max-heap to maintain the minimum" trick.
- [LeetCode Discuss — Important concepts & problems in Priority Queue/Heaps](https://leetcode.com/discuss/post/1113631/important-concepts-problems-in-priority-xu551/) — curated heap problem list with concepts.

## 🧮 Visualizers & Tools

- [VisuAlgo — Binary Heap (Priority Queue)](https://visualgo.net/en/heap) — animated insert/extract/heapify with a built-in quiz.
- [USF (Galles) — Heap operations lecture (PDF)](https://www.cs.usfca.edu/~galles/cs673/lecture/lecture3.pdf) — heap operations and analysis reference from the USFCA visualizations author.

## ❓ Most-Asked Interview Questions

1. **What is a heap and how is it stored?** A complete binary tree obeying the heap property, stored in an array; for index `i`: parent `(i-1)/2`, children `2i+1`/`2i+2`.
2. **Min-heap vs max-heap?** Min-heap: parent ≤ children (min at root). Max-heap: parent ≥ children (max at root). Only a partial order — siblings are unordered.
3. **Time complexity of insert, extract, and peek?** insert/extract `O(log n)` (sift-up/down along height), peek `O(1)`.
4. **Is building a heap `O(n)` or `O(n log n)`?** Bottom-up build-heap is `O(n)` — the height-weighted sum `Σ n/2^h · h` converges to `O(n)`. Inserting n elements one-by-one is `O(n log n)`.
5. **For K-th largest, which heap do you use and why?** A **min-heap of size K** — you keep the K largest and evict the smallest, so the root is the K-th largest. Cost `O(n log K)`.
6. **How do you find a running median from a stream?** Two heaps — max-heap for the lower half, min-heap for the upper half — kept balanced within one element; median is a top or the average of tops. `O(log n)` add, `O(1)` query.
7. **How does K-way merge with a heap work?** Push one head per sorted list into a min-heap; repeatedly pop the global min and push the next element from that same list. `O(N log K)`.
8. **Why is a heap not a sorted array?** It only guarantees the root is extreme; there's no total order, so you can't binary-search or index the K-th element directly.
9. **How do you convert a min-heap to a max-heap?** Rebuild with build-heap under the opposite comparator — `O(n)`, not `O(n log n)`.
10. **Heap vs BST for priority operations?** Both give `O(log n)` insert/delete, but a heap has `O(1)` find-min/max and better constants/locality; a BST gives ordered traversal and predecessor/successor, which a heap can't.
11. **When is quickselect better than a heap for K-th largest?** Quickselect averages `O(n)` (worst `O(n²)`) and is in-place; the heap is `O(n log K)` but streaming-friendly and worst-case bounded.
12. **How do you implement decrease-key with `std::priority_queue`?** It's not native — use lazy deletion (push updated entry, skip stale entries on pop) or an indexed heap.
13. **How does Task Scheduler use a heap?** A max-heap of remaining task counts always runs the most frequent available task, with cooling tasks held aside until their cooldown expires (idle otherwise).
14. **What is the greedy behind "connect ropes/sticks minimum cost"?** Repeatedly combine the two smallest via a min-heap (Huffman) — small lengths get re-added fewest times → `O(n log n)`.
15. **How would you get Top-K frequent elements efficiently?** Count frequencies, then a size-K min-heap keyed by frequency (`O(n log K)`), or bucket sort by frequency for `O(n)`.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Chapter 6 "Heapsort"** — heaps, `MAX-HEAPIFY`, `BUILD-MAX-HEAP` (the `O(n)` proof), and heapsort; **Chapter 6.5** covers priority queues.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Section 2.4** — binary heaps, heapsort, and index priority queues.
- **Grokking the Coding Interview** — the *Top-K Elements*, *Two Heaps*, and *K-way Merge* patterns map directly to this step: [Educative — Common Heaps Patterns](https://educative.io/courses/data-structures-for-coding-interviews/common-heaps-pattern) and [Introduction to K-way Merge](https://www.educative.io/courses/grokking-coding-interview-patterns-cpp/introduction-to-k-way-merge).
- If a local `books/` folder exists in this repo, see [../../../books/](../../../books/) for CLRS/Sedgewick copies.

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Sheet (Step 11: Heaps)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the official step this package covers.
- LeetCode problems from this step:
  - [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
  - [Task Scheduler](https://leetcode.com/problems/task-scheduler/)
  - [Hand of Straights](https://leetcode.com/problems/hand-of-straights/)
  - [Design Twitter](https://leetcode.com/problems/design-twitter/)
  - [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
  - [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
  - [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- [LeetCode Tag — Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/) — full problem list filtered by the heap tag for extra practice.
