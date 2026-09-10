# Solve Problems on Arrays [Easy → Medium → Hard] — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Arrays Part 1 (Easy) full walkthrough](https://youtu.be/37E9ckMDdTk) — takeUforward's marathon on largest/second-largest, sorted check, remove duplicates.
- [Striver — Arrays Part 2 (rotation, move zeros, union, search)](https://youtu.be/wvcQg43_V8U) — left rotate by one/K, move zeros, union, linear search.
- [Striver — Max consecutive ones & Single number](https://youtu.be/bYWLJb3vCWY) — running counters and XOR trick.
- [Striver — Kadane's Algorithm (Max Subarray Sum)](https://youtu.be/AHZpyENo7k4) — intuition, code, and printing the subarray.
- [Striver — Sort 0s,1s,2s (Dutch National Flag)](https://youtu.be/tp8JIuCXBaU) — three-pointer one-pass partition.
- [Striver — Majority Element (Boyer–Moore)](https://youtu.be/nP_ns3uSh80) — voting algorithm derivation.
- [Striver — Majority Element II (> n/3)](https://youtu.be/vwZj1K0e9U8) — two-candidate extended voting.
- [Striver — Next Permutation](https://youtu.be/JDOXKqF60RQ) — pivot/swap/reverse technique.
- [Striver — Longest Consecutive Sequence](https://youtu.be/oO5uLE7EUlM) — hashset expansion approach.
- [Striver — Set Matrix Zeroes](https://youtu.be/N0MgLvceX7M) · [Rotate Image 90°](https://youtu.be/Z0R2u6gd3GU) · [Spiral Matrix](https://youtu.be/3Zv-s9UUrFM) — matrix trio.
- [Striver — 3 Sum](https://youtu.be/DhFh8Kw7ymk) · [4 Sum](https://youtu.be/eD95WRfh81c) — sorted two-pointer k-sum.
- [Striver — Count subarrays with XOR K](https://youtu.be/eZr-6p0B7ME) · [Count Inversions](https://youtu.be/AseUmwVNaoY) · [Reverse Pairs](https://youtu.be/0e4bZaP3MDI) — prefix-XOR & merge-sort counting.
- [Striver — Merge Overlapping Intervals](https://youtu.be/IexN60k62jo) · [Merge sorted arrays w/o extra space](https://youtu.be/n7uwj04E0I4) · [Repeating & Missing](https://youtu.be/2D0D8HE6uak).

## 📝 Articles & Tutorials

- [takeUforward — Kadane's Algorithm](https://takeuforward.org/data-structure/kadanes-algorithm-maximum-subarray-sum-in-an-array/) — canonical Striver write-up with code.
- [takeUforward — Sort an array of 0s,1s,2s](https://takeuforward.org/data-structure/sort-an-array-of-0s-1s-and-2s/) — Dutch flag article.
- [takeUforward — Majority Element (n/2)](https://takeuforward.org/data-structure/find-the-majority-element-that-occurs-more-than-n-2-times/) — Moore voting.
- [takeUforward — Count subarrays with XOR K](https://takeuforward.org/data-structure/count-the-number-of-subarrays-with-given-xor-k/) — prefix-XOR hashmap.
- [takeUforward — Merge overlapping subintervals](https://takeuforward.org/data-structure/merge-overlapping-sub-intervals/) — sort + sweep.
- [GeeksforGeeks — Maximum Subarray Sum (Kadane)](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/) — brute → optimal progression.
- [GeeksforGeeks — Dutch National Flag Problem](https://www.geeksforgeeks.org/dsa/dutch-national-flag-problem-in-python/) — Dijkstra's three-way partition.
- [GeeksforGeeks — Sort an array of 0s,1s,2s](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-and-2s/) — multiple approaches.
- [GeeksforGeeks — Find the missing number](https://www.geeksforgeeks.org/find-the-missing-number/) — sum & XOR methods.
- [algo.monster — Subarray Sum Equals K (560) deep dive](https://algo.monster/liteproblems/560) — prefix-sum + hashmap intuition.
- [LeetCode Discuss — "Solve any array problem: Prefix sum, Kadane's, Intervals, Hashing, 2D"](https://leetcode.com/discuss/post/8356889/how-to-solve-any-array-problem-prefix-su-dji5/) — pattern cheat sheet.
- [LeetCode Discuss — Subarray Sum Patterns](https://leetcode.com/discuss/post/5284478/subarray-sum-patterns-by-nobleknight-h4ly/) — sum/xor/divisible variants with templates.
- [LeetCode Study Guide — Prefix Sum Problems](https://leetcode.com/discuss/study-guide/5119937/prefix-sum-problems) — curated prefix-sum problem set.

## 🧮 Visualizers & Tools

- [VisuAlgo — Sorting (incl. 3-way / partition intuition)](https://visualgo.net/en/sorting) — animate partition-based sorting relevant to Dutch flag.
- [USFCA — Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — classic algorithm animations.
- [Wikipedia — Maximum subarray problem (with Kadane figure)](https://en.wikipedia.org/wiki/Maximum_subarray_problem) — formal treatment and diagram.
- [Wikipedia — Dutch national flag problem](https://en.wikipedia.org/wiki/Dutch_national_flag_problem) — Dijkstra's original formulation.

## ❓ Most-Asked Interview Questions

1. **How does Kadane's handle all-negative arrays?** Track the global best *before* resetting `cur` to 0 (or seed `best = -∞`); the answer is the largest single element.
2. **Why does Boyer–Moore voting work?** Non-majority votes cancel majority votes at most 1-for-1; since the majority exceeds n/2, at least one vote survives, so the final candidate is correct (verify for the >n/3 case).
3. **Explain the Dutch National Flag invariant.** `[0..low-1]=0`, `[low..mid-1]=1`, `[mid..high]=unknown`, `[high+1..]=2`; on a `2` swap and *don't* advance `mid`.
4. **Why seed the prefix-sum hashmap with `{0:1}`?** So a subarray starting at index 0 whose sum equals `k` is counted (prefix itself equals `k`).
5. **Count subarrays with sum K when negatives exist — why not sliding window?** Sliding window needs monotonic sums; negatives break monotonicity, so use prefix-sum + hashmap.
6. **How to rotate a matrix 90° in place?** Transpose then reverse each row (clockwise); reverse columns/reverse-then-transpose for counter-clockwise.
7. **How to find both the repeating and missing number in O(n)/O(1)?** Solve `x - y = S - Sn` and `x² - y² = S2 - S2n`; use `long long`. XOR bucketing is an alternative.
8. **Why does merge sort count inversions?** During a merge, when `left[i] > right[j]`, every remaining left element is also greater, contributing `(mid - i + 1)` inversions in O(1).
9. **Difference between subarray and subsequence?** Subarray is contiguous; subsequence preserves order but may skip elements.
10. **How to find the longest consecutive sequence in O(n)?** Put values in a hashset and only start counting a run from a number whose predecessor is absent.
11. **How does Two Sum reach O(n)?** A hashmap of seen values lets you look up the complement `target - x` in O(1).
12. **How to merge overlapping intervals?** Sort by start; if the next start ≤ current end, extend; otherwise push a new interval.
13. **Why track both max and min in Max Product Subarray?** A negative number swaps the roles — the current minimum (very negative) can become the maximum after multiplying by another negative.
14. **What's the reversal trick for array rotation?** Reverse first `k`, reverse remaining `n-k`, reverse whole → left-rotated by `k` in O(n)/O(1).
15. **How does Next Permutation work?** Find rightmost `a[i] < a[i+1]`, swap `a[i]` with the smallest element to its right that's larger, then reverse the suffix.

## 📚 Books & Courses

- **CLRS — Introduction to Algorithms:** Ch. 2 (Insertion/Merge sort & inversions), Ch. 4 (Maximum subarray / divide & conquer), Ch. 8 (linear-time sorting ideas behind partitioning).
- **Sedgewick & Wayne — Algorithms (4th ed.):** sorting and partitioning chapters (three-way quicksort ↔ Dutch flag).
- **takeUforward A2Z DSA Course/Sheet** — the source curriculum for this topic.
- Cross-link: see [`../../../books/`](../../../books/) for any locally stored reference texts.

## 🔗 Official Problem Sources

- [takeUforward — Striver A2Z DSA Sheet (Step 3: Arrays)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official step page.
- [LeetCode — Array tag](https://leetcode.com/tag/array/) — all array-tagged problems.
- [LeetCode — Prefix Sum tag](https://leetcode.com/tag/prefix-sum/) · [Two Pointers tag](https://leetcode.com/tag/two-pointers/) · [Matrix tag](https://leetcode.com/tag/matrix/) — pattern-filtered practice.
- [LeetCode — Top Interview 150 study plan](https://leetcode.com/studyplan/top-interview-150/) — includes the core array problems above.
