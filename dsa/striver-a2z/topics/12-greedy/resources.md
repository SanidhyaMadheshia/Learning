# Greedy Algorithms — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Assign Cookies (takeUforward)](https://youtu.be/DIX2p7vb9co?si=GofAIDimue-Av0Fi) — the greedy two-pointer match, the A2Z starting problem.
- [Striver — Fractional Knapsack](https://youtu.be/1ibsQrnuEEg?si=8R2By3wpHo0zZVHE) — ratio-based greedy and why it beats 0/1 knapsack.
- [Striver — N Meetings in One Room](https://youtu.be/mKfhTotEguk?si=2RELeq18mpmIIN3Q) — canonical activity-selection / sort-by-end intuition.
- [Striver — Jump Game I](https://youtu.be/tZAa_jJ3SwQ?si=voKd7n9VTLDRRNzJ) & [Jump Game II](https://youtu.be/7SBVnw7GSTk?si=9uUouBELh9K3m2jZ) — reachability and min-jumps window.
- [Striver — Minimum Platforms](https://youtu.be/AsGzwR_FWok?si=165acXU_dtqOHuo9) — two-pointer sweep over arrivals/departures.
- [Striver — Job Sequencing](https://youtu.be/QbwltemZbRg?si=wvcemJ5BLPlTRmkG) — profit-desc sort + latest-slot assignment.
- [Striver — Candy](https://youtu.be/IIqVFvKE6RY?si=EjmuXZJNLQLUkEd7) — two-pass neighbor-constraint greedy.
- [Striver — Shortest Job First (SJF)](https://youtu.be/3-QbX1iDbXs?si=IH8QZUblr01F7UoQ) — CPU scheduling as greedy.
- [Striver — Insert Interval](https://youtu.be/xxRE-46OCC8?si=a7aPuIw16zDx2lAa) & [Non-overlapping Intervals](https://youtu.be/HDHQ8lAWakY?si=JVtLqboGdpUTOVjf) — interval merging/removal.
- [Striver — Merge Intervals (A2Z playlist)](https://www.youtube.com/watch?v=2JzRBPFYbKE&list=PLgUwDviBIf0rPG3Ictpu74YWBQ1CaBkm2&index=6) — sort-by-start merge sweep.
- [Striver — Valid Parenthesis String](https://youtu.be/cHT6sG_hUZI?si=XRHeyh7jOaLaTy3g) — the `[low, high]` range trick.

---

## 📝 Articles & Tutorials

- [GeeksforGeeks — Greedy Algorithms Tutorial](https://www.geeksforgeeks.org/greedy-algorithms/) — broad overview with worked examples and pitfalls.
- [GeeksforGeeks — Greedy Algorithms: General Structure](https://www.geeksforgeeks.org/greedy-algorithms-general-structure-and-applications/) — the standard greedy template and where it applies.
- [GeeksforGeeks — Activity Selection Problem](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/) — the interval-scheduling archetype.
- [GeeksforGeeks — Scheduling in Greedy Algorithms](https://www.geeksforgeeks.org/dsa/scheduling-in-greedy-algorithms/) — correctness argument for earliest-finish scheduling.
- [GeeksforGeeks — Greedy vs Dynamic Programming](https://www.geeksforgeeks.org/greedy-approach-vs-dynamic-programming/) — when each wins and why.
- [Cornell CS482 — Greedy Exchange Argument (PDF)](https://www.cs.cornell.edu/courses/cs482/2004su/handouts/greedy_exchange.pdf) — the definitive 3-step exchange-argument proof method.
- [Stanford CS161 — Greedy Algorithms Lecture Notes (PDF)](https://web.stanford.edu/class/archive/cs/cs161/cs161.1166/lectures/lecture14.pdf) — greedy as a refinement of DP, formal treatment.
- [The Exchange Argument Explained (Jeremy Quinto)](https://blog.jeremyquinto.com/proving-optimization-problems-the-exchange-argument) — approachable walkthrough of proving greedy optimality.
- [CLRS Chapter 16 solutions (GitHub)](https://github.com/gzc/CLRS/blob/master/C16-Greedy-Algorithms/16.1.md) — activity-selection variants and proofs.
- [OpenGenus — Activity Selection using Greedy](https://iq.opengenus.org/activity-selection-problem-greedy-algorithm/) — `O(n log n)` derivation and variants.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — Sorting](https://visualgo.net/en/sorting) — visualize the sort step that precedes most greedy algorithms.
- [USFCA — Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — heaps/priority queues used in deadline-greedy problems.
- [Algorithm Visualizer (interval/greedy)](https://algorithm-visualizer.org/) — step through greedy and scheduling algorithms interactively.

---

## ❓ Most-Asked Interview Questions

1. **What is a greedy algorithm?** An algorithm that makes the locally optimal choice at each step and commits to it, aiming for a global optimum without backtracking.
2. **When is greedy guaranteed correct?** When the problem has the **greedy-choice property** (a local optimum leads to a global optimum) *and* **optimal substructure**.
3. **How do you prove a greedy algorithm optimal?** With an **exchange argument** (swap any optimal solution's element for greedy's choice without worsening it) or a **"greedy stays ahead"** inductive proof.
4. **Greedy vs Dynamic Programming?** Greedy makes one irrevocable choice per step (fast, `O(n log n)` typical); DP explores overlapping subproblems and memoizes. Use DP when the greedy choice depends on future subproblems.
5. **Why is Fractional Knapsack greedy but 0/1 Knapsack DP?** Fractions let you take value/weight ratio optimally; with whole items only, a locally best ratio can block a better combination, breaking the greedy-choice property.
6. **In activity selection, why sort by finish time (not start or duration)?** Earliest finish frees the resource soonest, leaving maximum room for remaining activities; the exchange argument shows no other choice does better.
7. **How do you find the minimum number of platforms?** Sort arrivals and departures separately and sweep with two pointers, tracking peak concurrent trains — that peak is the answer.
8. **How does Jump Game II achieve O(n)?** Treat it as BFS levels: expand a reachable window, take the farthest reach as the next window, and count each boundary as one jump.
9. **Why does Candy need two passes?** A single direction only satisfies one neighbor; the second reverse pass with `max` enforces the other side's constraint simultaneously.
10. **How is Job Sequencing greedy?** Sort by profit descending and place each job in the latest free slot before its deadline, maximizing total profit while leaving early slots free.
11. **Give an example where greedy fails.** General Coin Change with denominations like {1,3,4} for amount 6 — greedy picks 4+1+1 (3 coins) but 3+3 (2 coins) is optimal; needs DP.
12. **What is the greedy strategy in Lemonade Change?** Prefer giving `$10+$5` over three `$5` for a `$20`, hoarding flexible `$5` bills.
13. **How do you insert an interval into a sorted list?** Append all intervals before it, merge all overlapping ones by expanding bounds, then append the merged interval and the rest — `O(n)`.
14. **What sort key merges intervals?** Sort by **start**; extend the current interval's end while the next start ≤ current end.
15. **What's the greedy insight for Non-overlapping Intervals?** Maximize kept compatible intervals by sorting on end time; minimum removals = `n − kept`.

---

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Chapter 16 "Greedy Algorithms"** — activity selection, greedy-choice property, matroid theory, Huffman codes. See [../../../books/](../../../books/) if a local copy exists.
- **Kleinberg & Tardos — *Algorithm Design*, Chapter 4 "Greedy Algorithms"** — interval scheduling and the exchange-argument proof style in depth.
- **Skiena — *The Algorithm Design Manual*** — practical heuristics and when greedy is a reasonable approximation.
- **[Stanford CS161 course archive](https://web.stanford.edu/class/archive/cs/cs161/cs161.1166/)** — lecture notes and problem sets on greedy correctness.

---

## 🔗 Official Problem Sources

- [takeUforward — Striver A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — Step 12 "Greedy Algorithms" is the source of these problems.
- [LeetCode — Greedy Tag](https://leetcode.com/tag/greedy/) — all greedy-tagged problems for extra practice.
- [LeetCode — Intervals Tag](https://leetcode.com/tag/interval/) — interval scheduling/merging problems from this step.
- [GeeksforGeeks — Greedy Algorithms Practice](https://www.geeksforgeeks.org/greedy-algorithms/) — company-tagged greedy problem set.
