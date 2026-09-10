# Binary Search [1D, 2D Arrays, Search Space] — Resources & References

**Navigation:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Binary Search Full Playlist (takeUforward A2Z)](https://www.youtube.com/watch?v=v57lNF2mb_s&list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF) — the complete Striver binary search series covering 1D, answers, and 2D.
- [Striver — Binary Search intro / template](https://youtu.be/MHf6awe89xw) — the foundational binary search video used for "Search X in sorted array".
- [Striver — Lower & Upper Bound / Insert Position / Floor-Ceil](https://youtu.be/6zhGS79oQ4k) — one video that grounds all the boundary problems.
- [Striver — First & Last Occurrence / Count](https://youtu.be/hjR1IYVx9lY) — occurrence and count problems.
- [Striver — Search in Rotated Sorted Array I](https://www.youtube.com/watch?v=r3pMQ8-Ad5s) — the sorted-half detection technique.
- [Striver — Koko Eating Bananas (BS on answer)](https://youtu.be/qyfekrNni90) — canonical intro to binary search on the answer.
- [Striver — Aggressive Cows](https://youtu.be/R_Mfw4ew-Vo) — the maximize-minimum-distance pattern.
- [Striver — Median of Two Sorted Arrays](https://www.youtube.com/watch?v=NTop3VTjmxk) — the partition method in detail.
- [Striver — Search in a 2D Matrix](https://youtu.be/ZYpYur0znng) and [2D Matrix II](https://youtu.be/9ZbB397jU4k) — flattened search vs staircase search.
- [Striver — Find Peak Element II (2D)](https://youtu.be/nGGp5XBzC4g) — binary search on columns.

## 📝 Articles & Tutorials

- [takeUforward — Binary Search Explained](https://takeuforward.org/data-structure/binary-search-explained/) — Striver's written companion to the playlist.
- [CP-Algorithms — Binary Search](https://github.com/dhruvksuri/cp-algorithms-bible/blob/master/src/num_methods/binary_search.md) — rigorous treatment of the splitting idea and search on answer.
- [GeeksforGeeks — Binary Search on Answer Tutorial with Problems](https://www.geeksforgeeks.org/binary-search-on-answer-tutorial-with-problems/) — predicate-based framing with practice problems.
- [GeeksforGeeks — binary_search, lower_bound, upper_bound in C++ STL](https://www.geeksforgeeks.org/cpp/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/) — STL usage reference.
- [GeeksforGeeks — Median of two sorted arrays (different sizes) via BS](https://www.geeksforgeeks.org/median-two-sorted-arrays-different-sizes-ologminn-m/) — the partition derivation.
- [LeetCode Discuss — An opinionated guide to binary search (bulletproof template)](https://leetcode.com/discuss/study-guide/2371234/An-opinionated-guide-to-binary-search-) — a single robust template for every variant.
- [LeetCode Discuss — Powerful Ultimate Binary Search Template](https://leetcode.com/discuss/post/786126/python-powerful-ultimate-binary-search-t-rwv8/) — the "minimize k s.t. condition(k)" framework.
- [LeetCode Discuss — Binary Search: A Comprehensive Guide (monotonic functions)](https://leetcode.com/discuss/post/3726061/binary-search-a-comprehensive-guide/) — when a problem reduces to searching a monotone function.
- [Medium — The Ultimate Binary Search Guide: Different Templates](https://ahmedhemaz.medium.com/the-ultimate-binary-search-guide-exploring-different-templates-for-success-ae501637a478) — the three-template taxonomy.
- [Medium — Binary Search: Find Upper and Lower Bound](https://medium.com/swlh/binary-search-find-upper-and-lower-bound-3f07867d81fb) — clear lower/upper bound walkthrough.

## 🧮 Visualizers & Tools

- [VisuAlgo — Binary Search Tree / search operations](https://visualgo.net/en/bst) — interactive visualization of ordered search structures.
- [USFCA — Comparison / Search visualizations](https://www.cs.usfca.edu/~galles/visualization/Search.html) — step-through of binary search on an array.
- [LeetCode Discuss — Binary Search Visualization (see it move)](https://leetcode.com/discuss/post/8375313/binary-search-visualization-binary-searc-o6z8/) — animated intuition for pointer movement.

## ❓ Most-Asked Interview Questions

1. **Why does `mid = (low + high) / 2` fail and how do you fix it?** For large indices `low + high` overflows `int`. Use `mid = low + (high - low) / 2`.
2. **What's the difference between lower_bound and upper_bound?** `lower_bound` returns the first index with `a[i] >= x`; `upper_bound` returns the first index with `a[i] > x`. Their difference is the count of `x`.
3. **How do you find first and last occurrence in `O(log n)`?** First = `lower_bound(x)`; last = `upper_bound(x) - 1` (after confirming `x` exists).
4. **When can binary search be applied without a sorted array?** Whenever the answer space has a **monotone predicate** `F...F T...T` — this is "binary search on the answer".
5. **How do you search a rotated sorted array?** At each step one half is sorted; check whether the target lies in the sorted half and recurse there. `O(log n)` for unique elements.
6. **Why does rotated array with duplicates degrade to `O(n)`?** When `a[low]==a[mid]==a[high]` you can't tell which half is sorted, so you shrink both ends by one — adversarial input (all equal) forces linear time.
7. **How do you find a peak element in `O(log n)`?** Move toward the higher neighbor (`a[mid] < a[mid+1]` → go right). You always converge to some peak because you climb uphill.
8. **Explain the Koko / ship-capacity / book-allocation family.** All are "minimize the maximum" (or "maximize the minimum") — bound the answer range, write a feasibility predicate, binary search the boundary.
9. **How do you choose the search bounds for a BS-on-answer problem?** `lo` is the smallest feasible individual constraint (e.g., `max(weights)` so a single item fits) and `hi` is the loosest (e.g., `sum(weights)`).
10. **How do you find the median of two sorted arrays in `O(log(min(m,n)))`?** Binary search a partition of the smaller array so left halves total `(m+n+1)/2` and `l1<=r2 && l2<=r1`; the median is derived from the boundary elements.
11. **How do you search a fully sorted 2D matrix?** Treat it as a 1D array of size `m*n` and map `mid → (mid/n, mid/%n)`; `O(log(m*n))`.
12. **How does staircase search work for a row/column-sorted matrix?** Start top-right: go left if the cell is too big, down if too small; `O(m+n)`.
13. **How do you find a 2D peak efficiently?** Binary search on columns; within the middle column take the row-max and move toward the larger horizontal neighbor; `O(m log n)`.
14. **How do you find the median of a row-wise sorted matrix?** Binary search on the value range; count elements `<= x` per row with `upper_bound`; median is the smallest `x` with count `>= (m*n+1)/2`.
15. **What causes infinite loops in binary search?** Using `low = mid` without biasing `mid` upward, or mixing closed `[low,high]` and half-open `[low,high)` conventions in one loop.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*** — searching, divide-and-conquer analysis (Ch. 2 & problem sets on binary search / master theorem). See [../../../books/](../../../books/) if present in this repo.
- **Sedgewick & Wayne — *Algorithms* (4th ed.)** — binary search and ordered symbol tables.
- **Competitive Programmer's Handbook (Antti Laaksonen)** — free PDF; chapter on binary search including "binary search on the answer".
- **takeUforward A2Z DSA Course** — the structured course this package follows.

## 🔗 Official Problem Sources

- [takeUforward — Striver A2Z DSA Sheet (Step 4: Binary Search)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official step page.
- [LeetCode — Binary Search tag](https://leetcode.com/tag/binary-search/) — all binary-search-tagged problems.
- [LeetCode — Binary Search Explore Card](https://leetcode.com/explore/learn/card/binary-search/) — official interactive study track.
- [LeetCode Discuss — Ultimate Binary Search Master List (Amazon SDE prep)](https://leetcode.com/discuss/post/7483322/ultimate-binary-search-master-list-for-a-yes1/) — curated interview problem list overlapping this step.
