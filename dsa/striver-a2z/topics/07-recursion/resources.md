# Recursion [PatternWise] — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver's Recursion Playlist (takeUforward)](https://www.youtube.com/watch?v=eQCS_v3bw0Q&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9) — full recursion basics → subsequences → advanced, the canonical A2Z sequence.
- [Striver's Recursion & Backtracking (Placement) Playlist](https://www.youtube.com/playlist?list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma) — the SDE-sheet playlist that hosts N-Queens, Sudoku, M-Coloring, Rat-in-a-Maze videos linked in the problems file.
- [Pow(x, n) — Striver](https://youtu.be/l0YC3876qxg) — binary exponentiation walkthrough (from the data file).
- [Power Set — Striver](https://www.youtube.com/watch?v=b7AYbpM5YrE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=67) — pick/not-pick + bitmask subset generation.
- [Combination Sum I — Striver](https://www.youtube.com/watch?v=OyZFFqQtu98&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=49) & [Combination Sum II — Striver](https://www.youtube.com/watch?v=G1fRTGRxXU8&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=50) — the two must-watch combination videos.
- [Subsets I — Striver](https://www.youtube.com/watch?v=rYkfBRtMJr8&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=52) & [Subsets II — Striver](https://www.youtube.com/watch?v=RIn3gOkbhQE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=53) — subset generation with duplicate handling.
- [N-Queens — Striver](https://www.youtube.com/watch?v=i05Ju7AftcM&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=57), [Sudoku Solver — Striver](https://www.youtube.com/watch?v=FWAIf_EVUKE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=58), [M-Coloring — Striver](https://www.youtube.com/watch?v=wuVwUK25Rfc&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=59), [Rat in a Maze — Striver](https://www.youtube.com/watch?v=bLGZhJlt4y0&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=60) — the hard backtracking set.
- [Palindrome Partitioning — Striver](https://youtu.be/_H8V5hJUGd0) — string partition backtracking (from the data file).

---

## 📝 Articles & Tutorials

- [Striver A2Z DSA Sheet (master index)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the sheet this topic belongs to.
- [Learn All Patterns of Subsequences — takeUforward](https://takeuforward.org/data-structure/learn-all-patterns-of-subsequences-theory) — print/count/exists on one recursion tree.
- [Generating all Subsequences using Recursion — GeeksforGeeks](https://www.geeksforgeeks.org/dsa/generating-all-possible-subsequences-using-recursion/) — the include/exclude decision spelled out.
- [Backtracking: template + subsets/permutations/combination sum — Paul Epps (Substack)](https://paulepps.substack.com/p/backtracking-template-subsets-permutations) — shows LC 78/46/39 as one template.
- [Practical Guide to Recursion with Backtracking — Medium](https://medium.com/@kalyaninturi/practical-guide-to-recursion-with-backtracking-a1b9c4b6cc74) — the choose/explore/unchoose pattern with LeetCode examples.
- [Backtracking to Solve All Permutation/Combination/Subset Problems — labuladong](https://labuladong.online/en/algo/essential-technique/permutation-combination-subset-all-in-one/) — a unifying framework across all three families.
- [How to dry-run recursive backtracking — leetcopilot (Hashnode)](https://leetcopilot.hashnode.dev/how-to-dry-run-recursive-backtracking-problems-for-beginners-step-by-step) — a visual tracing method for beginners.
- [Backtracking: Pattern, Template & 105 LeetCode Problems — Stealth Interview](https://www.stealthinterview.ai/leetcode/patterns/backtracking) — pattern write-up plus a large curated problem list.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — Recursion Tree & DAG](https://visualgo.net/en/recursion/) — animates the recursion tree with active/base-case node coloring.
- [Recursion Visualization — Coddy](https://coddy.tech/visualize/concepts/recursion) — shows the call stack growing and unwinding.
- [Python Tutor](https://pythontutor.com/) — step through recursive calls frame-by-frame (C++, Python, Java) to *see* the stack.
- [Recursion Tree Visualizer — GitHub (Adarshkodes)](https://github.com/Adarshkodes/recursion-tree-visualizer) — interactive branching/depth visualizer for JS/Python/Go.

---

## ❓ Most-Asked Interview Questions

1. **What are the three parts of a recursive function?** Base case (stop), recursive case (reduce toward base), and the state passed down.
2. **What is a recursion tree and how does it relate to complexity?** A tree where each node is a call; number of nodes ≈ time, height ≈ auxiliary stack space.
3. **Explain pick / not-pick.** At each index branch into "include this element" and "exclude it"; a depth-`n` binary tree yields the `2ⁿ` subsequences.
4. **What is backtracking, and how does it differ from plain recursion?** DFS over partial solutions where every choice made going down is undone coming back up (`choose → recurse → un-choose`), letting one mutable path represent the whole tree.
5. **How do you handle duplicates in Subsets II / Combination Sum II?** Sort the input, then skip equal siblings at the same recursion level (`if (i>start && a[i]==a[i-1]) continue;`).
6. **Difference between Combination Sum I and II?** I allows unlimited reuse (recurse on same index); II uses each element once (recurse on `i+1`) and must skip duplicates.
7. **How do you optimize Pow(x, n)?** Binary exponentiation `x^n=(x^{n/2})²` in O(log n); handle negative `n` with `long long` to avoid `INT_MIN` overflow.
8. **How do you avoid recomputation in Word Break?** Memoize on the start index, converting exponential recursion into O(n²).
9. **How do you make the N-Queens safety check O(1)?** Maintain boolean flags for occupied rows and the two diagonals (`row+col`, `n-1+col-row`).
10. **When does recursion cause a stack overflow, and how to fix it?** Very deep recursion (large `n` / missing base case). Fix by adding/correcting base cases, memoizing, or converting to an explicit-stack iterative form.
11. **How do print, count, and exists variants of subsequence problems differ?** Same tree; print collects paths at leaves, count returns `f(pick)+f(skip)`, exists returns `f(pick) || f(skip)` with short-circuit.
12. **Why sort a stack using recursion instead of another stack?** The constraint is "recursion only" — the call stack stores popped elements, and each is re-inserted in sorted order while unwinding (O(n²)).
13. **What is pruning and why does it matter?** Cutting branches that cannot lead to a solution (e.g., `curSum > target`, unsafe placement) — often the difference between TLE and AC.
14. **How do you generate valid parentheses without producing invalid ones?** Maintain the invariant `open ≤ n` and `close < open`; only add a bracket when it keeps the string valid.
15. **How is Sudoku's complexity bounded?** Roughly `O(9^(empty cells))`, drastically reduced by row/column/box constraint pruning.

---

## 📚 Books & Courses

- **Introduction to Algorithms (CLRS)** — Chapter on Divide-and-Conquer and the substitution/recursion-tree method for solving recurrences.
- **The Algorithm Design Manual (Skiena)** — the Backtracking section (combinatorial search, pruning) maps directly to Pattern 3 here.
- **Competitive Programmer's Handbook (Antti Laaksonen)** — "Complete search" chapter covers generating subsets/permutations and backtracking (N-Queens).
- Cross-link: see the repo's [`../../../books/`](../../../books/) folder for local copies/notes if present.
- **Striver's A2Z DSA Course** (free) — [takeuforward.org](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — structured video + article course.

---

## 🔗 Official Problem Sources

- [Striver A2Z Sheet — Step 7 (takeUforward)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official step page listing these recursion problems.
- [LeetCode — Recursion tag](https://leetcode.com/tag/recursion/) — all recursion-tagged problems.
- [LeetCode — Backtracking tag](https://leetcode.com/tag/backtracking/) — subsets, permutations, N-Queens, Sudoku, etc.
- [LeetCode Discuss — Backtracking algorithm + problems to practice](https://leetcode.com/discuss/post/1405817/backtracking-algorithm-problems-to-practice/) — a widely-shared curated backtracking list.
- [GeeksforGeeks — Recursion](https://www.geeksforgeeks.org/dsa/introduction-to-recursion-2/) & [GeeksforGeeks — Backtracking](https://www.geeksforgeeks.org/dsa/backtracking-algorithms/) — reference articles with more practice.
