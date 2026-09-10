# Learn Important Sorting Techniques — Resources & References

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

All links below are real and verified from research and the topic data file.

---

## 📺 Videos & Playlists

- [Striver — Selection / Bubble / Insertion Sort (timestamped)](https://youtu.be/HGk_ypEuS24?t=167) — takeUforward's single video walking through all three quadratic sorts with dry runs.
- [Striver — Merge Sort](https://youtu.be/ogjf7ORKfd8) — divide-and-conquer explained with recursion tree and merge step.
- [Striver — Quick Sort](https://youtu.be/WIrA4YexLRQ) — pivot, partition, and recursion, Striver-style.
- [Strivers A2Z DSA Course/Sheet (official)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the full ordered sheet this topic belongs to.

## 📝 Articles & Tutorials

- [takeUforward — Selection Sort](https://takeuforward.org/sorting/selection-sort-algorithm/) — canonical write-up + code.
- [takeUforward — Bubble Sort](https://takeuforward.org/data-structure/bubble-sort-algorithm/) — with adaptive early-exit.
- [takeUforward — Insertion Sort](https://takeuforward.org/data-structure/insertion-sort-algorithm/) — shift-and-insert intuition.
- [takeUforward — Merge Sort](https://takeuforward.org/data-structure/merge-sort-algorithm/) — recursion + merge.
- [takeUforward — Quick Sort](https://takeuforward.org/data-structure/quick-sort-algorithm/) — partition schemes.
- [GeeksforGeeks — Introduction to Sorting Techniques](https://www.geeksforgeeks.org/dsa/introduction-to-sorting-algorithm/) — in-place, stable, adaptive definitions.
- [GeeksforGeeks — Analysis of Different Sorting Techniques](https://www.geeksforgeeks.org/analysis-of-different-sorting-techniques/) — complexity comparison table.
- [GeeksforGeeks — Stable and Unstable Sorting Algorithms](http://www.geeksforgeeks.org/stability-in-sorting-algorithms/) — precise stability definition with examples.
- [GeeksforGeeks — Sorting Algorithms (index)](https://www.geeksforgeeks.org/sorting-algorithms/) — hub for every sort.
- [Princeton algs4 — Mergesort and Quicksort (PDF)](https://algs4.cs.princeton.edu/lectures/keynote/22Mergesort.pdf) — Sedgewick's authoritative lecture slides.
- [Stanford CS106B — Sorting](https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1262/lectures/19-sorting/) — clean academic treatment.
- [Sorting Algorithms Quick Reference: QuickSort/MergeSort/TimSort](https://sesamedisk.com/quick-reference-sorting-algorithms/) — practical cheat sheet.

## 🧮 Visualizers & Tools

- [VisuAlgo — Sorting (Bubble/Selection/Insertion/Merge/Quick)](https://visualgo.net/en/sorting?slide=6-1) — the gold-standard interactive sorting visualizer.
- [GeeksforGeeks — Bubble Sort Visualization](https://www.geeksforgeeks.org/dsa/sorting-algorithms-visualization-bubble-sort/) — animated bubble sort.
- [GeeksforGeeks — Insertion Sort Visualization](https://www.geeksforgeeks.org/sorting-algorithm-visualization-insertion-sort/) — animated insertion sort.

## ❓ Most-Asked Interview Questions

1. **Which sorts are stable?** Merge, Bubble, and Insertion are stable; Selection and Quick are not (heap sort also unstable).
2. **What does "in-place" mean and which sorts qualify?** Uses O(1) extra memory (plus recursion stack). Selection, Bubble, Insertion, and Quick are in-place; Merge is not (needs O(n) buffer).
3. **Why is merge sort O(n log n) in all cases?** `T(n)=2T(n/2)+O(n)` — log n levels of splitting, O(n) merge work per level.
4. **When does quicksort hit O(n²)?** When partitions are maximally unbalanced — e.g. already-sorted input with first/last-element pivot. Fix with randomised or median-of-three pivot.
5. **Best sort for nearly-sorted data?** Insertion sort — adaptive, runs in ~O(n).
6. **Merge sort vs quick sort — when to pick which?** Merge for guaranteed O(n log n), stability, linked lists, and external sorting; quick for in-place, cache-friendly, fast average performance.
7. **Why is selection sort unstable?** Its long-distance swap can move an equal-valued element past its identical twin, changing relative order.
8. **What is the lower bound for comparison sorts?** Ω(n log n) — proven via the decision-tree argument.
9. **How do counting/radix sort beat n log n?** They are non-comparison sorts exploiting a bounded key range, giving O(n + k) — but need extra assumptions/space.
10. **What sort does the C++ STL `std::sort` use?** Introsort — quicksort that switches to heapsort on bad recursion depth and insertion sort on small ranges.
11. **Minimum number of swaps: selection vs bubble?** Selection does at most n−1 swaps; bubble may do O(n²) swaps — selection wins when writes are expensive.
12. **How to make quicksort's recursion stack O(log n)?** Recurse on the smaller partition first and tail-call/loop on the larger.
13. **Why does `<=` (not `<`) keep merge sort stable?** When keys are equal, taking from the left half first preserves original order.
14. **Which sort is used by Python `sorted()` / Java `Arrays.sort` for objects?** TimSort — a hybrid of merge and insertion sort that exploits existing runs.
15. **Can bubble sort ever be O(n)?** Yes — best case on already-sorted input with the swap-flag optimization.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, 3rd/4th ed.** — Ch. 2 (Insertion/Merge Sort), Ch. 7 (Quicksort), Ch. 8 (lower bounds & non-comparison sorts). See [../../../books/](../../../books/) if a local copy exists.
- **Sedgewick & Wayne — *Algorithms*, 4th ed.** — Ch. 2 Sorting; companion site [algs4.cs.princeton.edu](https://algs4.cs.princeton.edu/lectures/keynote/22Mergesort.pdf).
- **Stanford CS106B** — [Sorting lecture](https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1262/lectures/19-sorting/) for a course-style walkthrough.

## 🔗 Official Problem Sources

- [Strivers A2Z DSA Course/Sheet — Step 2](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the source sheet for this topic.
- [LeetCode — Sorting tag](https://leetcode.com/tag/sorting/) — all sorting-tagged problems.
- [LeetCode — Sort an Array (912)](https://leetcode.com/problems/sort-an-array/) — practice implementing merge/quick sort from scratch.
- [GeeksforGeeks — Sorting Interview Questions](https://www.geeksforgeeks.org/dsa/commonly-asked-data-structure-interview-questions-on-sorting/) — curated interview set.
