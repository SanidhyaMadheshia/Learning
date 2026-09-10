# Dynamic Programming — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver DP Series — Dynamic Programming Problems (takeUforward)](https://takeuforward.org/dynamic-programming/striver-dp-series-dynamic-programming-problems) — The canonical, structured 56-video DP playlist this study package is built around (memo → tab → space-opt for every pattern).
- [Introduction to DP (Striver, YouTube)](https://youtu.be/tyB0ztf0DNY) — The mindset video: overlapping subproblems, optimal substructure, and the three-step framework.
- [Climbing Stairs / 1D DP (Striver)](https://youtu.be/mLfjzJsN8us) — Kicks off 1D DP with the Fibonacci-shaped recurrence.
- [Longest Common Subsequence (Striver)](https://youtu.be/-zI4mrF2Pb4) — The template for all two-string DP.
- [Edit Distance (Striver)](https://youtu.be/fJaKO8FbDdo) — Insert/delete/replace recurrence, the interview classic.
- [Buy & Sell Stock DP intro (Striver)](https://youtu.be/excAOvwF_Wk) — State machine for the entire stocks sub-pattern.
- [Longest Increasing Subsequence, Binary Search (Striver)](https://youtu.be/on2hvxBXJH4) — O(n²) DP and the O(n log n) tails/patience approach.
- [Matrix Chain Multiplication / Partition DP (Striver)](https://youtu.be/vRVfmbCFW7Y) — Interval DP framework used by MCM, cut-the-stick, and burst balloons.
- [Burst Balloons — Partition DP (Striver)](https://youtu.be/Yz4LlDSlkns) — The "which element bursts last" reframing.

## 📝 Articles & Tutorials

- [takeUforward — Dynamic Programming Introduction](https://takeuforward.org/data-structure/dynamic-programming-introduction/) — Text companion to the intro video.
- [GeeksforGeeks — Dynamic Programming (DP) main tutorial](https://www.geeksforgeeks.org/dsa/dynamic-programming/) — Broad reference hub with dozens of worked DP problems.
- [GeeksforGeeks — DP Introduction / GATE notes](https://www.geeksforgeeks.org/dsa/introduction-to-dynamic-programming-data-structures-and-algorithm-tutorials/) — Clean explanation of overlapping subproblems & optimal substructure.
- [cp-algorithms — Knapsack DP](https://cp-algorithms.com/dynamic_programming/knapsack.html) — Rigorous treatment of 0/1 vs unbounded knapsack (competitive-programming grade).
- [GeeksforGeeks — 0/1 Knapsack Problem](https://www.geeksforgeeks.org/dsa/0-1-knapsack-problem-dp-10/) — The subsequence/knapsack backbone with take/not-take.
- [GeeksforGeeks — Unbounded Knapsack](https://www.geeksforgeeks.org/dsa/unbounded-knapsack-repetition-items-allowed/) — Coin change / rod cutting foundation.
- [GeeksforGeeks — Longest Common Subsequence (LCS)](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/) — LCS table and reconstruction, the string-DP root.
- [LeetCode Discuss — Dynamic Programming Patterns (study guide)](https://leetcode.com/discuss/study-guide/4988261/Dynamic-Programming-Patterns/) — Popular pattern catalog mapping problem types to recurrences.
- [LeetCode Discuss — Mastering Dynamic Programming: A Comprehensive Guide](https://leetcode.com/discuss/study-guide/4677772/Mastering-Dynamic-Programming:-A-Comprehensive-Guide/) — End-to-end DP methodology with curated problem lists.
- [LeetCode Discuss — Art of Intuition for Solving DP Problems](https://leetcode.com/discuss/post/5583619/Learning-the-Art-of-Intuition-for-Solving-Dynamic-Programming-Problems/) — How to *derive* the recurrence rather than memorize.

## 🧮 Visualizers & Tools

- [VisuAlgo — Dynamic Programming visualizations](https://visualgo.net/en) — Animates classic DP (LCS, edit distance, coin change, knapsack tables).
- [USFCA Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — Includes DP-related structures and dynamic algorithm animations.
- [LeetCode DP Grandmaster study plan](https://leetcode.com/studyplan/dynamic-programming-grandmaster/) — Interactive, progressively harder DP set with built-in test harness.

## ❓ Most-Asked Interview Questions

1. **What are the two conditions that make a problem solvable by DP?**
   *Optimal substructure* (optimal answer built from optimal sub-answers) and *overlapping subproblems* (same sub-problem recomputed).

2. **Memoization vs Tabulation — difference and trade-offs?**
   Memoization is top-down recursion + cache (easy to write, uses call stack, computes only needed states). Tabulation is bottom-up iteration filling a table (no stack, may compute unused states, easier to space-optimize).

3. **How do you decide the DP state?**
   Ask "what minimal set of parameters uniquely identifies a sub-problem?" Those parameters become the table dimensions; the recurrence is how a state depends on smaller states.

4. **Difference between 0/1 and unbounded knapsack in the recurrence?**
   In 0/1, after taking an item you move to `i-1`. In unbounded you stay on `i` (item reusable). This one line separates Coin Change, Rod Cutting, and Subset Sum.

5. **How is Longest Palindromic Subsequence solved with LCS?**
   `LPS(s) = LCS(s, reverse(s))` — the longest subsequence matching the string against its reverse is palindromic.

6. **Minimum insertions/deletions to convert A→B?**
   Keep the LCS; delete `len(A)-LCS` from A and insert `len(B)-LCS` into A. Total = `n + m - 2·LCS`.

7. **Why does Burst Balloons use "last balloon burst" instead of "first"?**
   If you fix which balloon bursts *last* in an interval, its neighbours are the fixed interval boundaries, making the subproblems independent. Fixing "first" leaves neighbours ambiguous.

8. **Explain the LIS O(n log n) approach.**
   Maintain `tails[k]` = smallest possible tail of an increasing subsequence of length `k+1`. For each element, binary-search its position; replace or append. The array length is the LIS length (patience sorting).

9. **How do stock problems generalize?**
   State `(day, holdingOrNot, transactionsLeft)`. Each day you skip or act (buy flips to holding and subtracts price; sell flips back, adds price, decrements transactions). Cooldown skips a day after selling; fee subtracts on the transaction.

10. **When is a problem a Partition/Interval DP?**
    When you must choose an order of operations or a split point on a contiguous range, and cost depends on the boundaries (MCM, cut-the-stick, burst balloons, palindrome partitioning). State is an interval `(i,j)`; try every split `k`.

11. **How do you handle counting DPs that overflow?**
    Use `long long` or apply the required modulus at each addition (common in Count Subsets, Target Sum, Coin Change 2, #LIS).

12. **Subsequence vs Substring in DP — what changes?**
    Substring/subarray requires contiguity, so on a mismatch the recurrence *resets to 0* (Longest Common Substring). Subsequence allows skipping, so it carries the best of neighbours forward.

13. **What's the space-optimization trick and when can't you use it?**
    If `dp[i]` depends only on `dp[i-1]` (and maybe `dp[i-2]`) or the previous row, keep just those. You can't fully compress when you need to *reconstruct* the actual answer (you need the whole table to backtrack).

14. **How does Count Square Submatrices work in one pass?**
    `dp[i][j] = 1 + min(top, left, top-left)` gives the largest square ending at `(i,j)`; that value also equals the number of squares ending there, so summing all `dp[i][j]` counts every square.

15. **Greedy vs DP — how to tell them apart (e.g. Assign Cookies vs Coin Change)?**
    If a locally optimal choice provably leads to a global optimum (exchange argument), greedy works (Assign Cookies). If choices interact and you must explore combinations, use DP (Minimum Coins with arbitrary denominations).

## 📚 Books & Courses

- **Introduction to Algorithms (CLRS), 3rd/4th ed.** — Chapter 15 "Dynamic Programming" (rod cutting, matrix-chain multiplication, LCS, optimal BST). The rigorous foundation for MCM and LCS here.
- **Algorithm Design (Kleinberg & Tardos)** — Chapter 6 "Dynamic Programming" (weighted interval scheduling, knapsack, sequence alignment / edit distance, RNA secondary structure).
- **Competitive Programming (Halim & Halim, "CP4")** — DP chapter covering classic and non-classical DP with contest problems.
- **Grokking Dynamic Programming Patterns (Educative)** — Pattern-based course (0/1 knapsack, unbounded knapsack, subsequences, palindromic) mirroring this file's grouping.
- **takeUforward A2Z DSA Course** — the full free structured course this topic is a part of (see below).
- *(Local cross-link:* if a `../../../books/` folder is added to this repo, link relevant CLRS/Kleinberg-Tardos chapter notes here.)*

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2) — The parent sheet; Step 16 is this Dynamic Programming step.
- [takeUforward — Striver DP Series (Step 16 hub)](https://takeuforward.org/dynamic-programming/striver-dp-series-dynamic-programming-problems) — Ordered problem+video index for exactly these patterns.
- [LeetCode — Dynamic Programming tag](https://leetcode.com/tag/dynamic-programming/) — All DP-tagged problems for extra practice.
- [LeetCode — Dynamic Programming Grandmaster study plan](https://leetcode.com/studyplan/dynamic-programming-grandmaster/) — Curated advanced DP study plan.
- [LeetCode — Dynamic Programming Patterns discuss guide](https://leetcode.com/discuss/study-guide/4988261/Dynamic-Programming-Patterns/) — Community-maintained pattern → problem map.
- [GeeksforGeeks — Dynamic Programming practice hub](https://www.geeksforgeeks.org/dsa/dynamic-programming/) — Article + practice links per DP problem.
