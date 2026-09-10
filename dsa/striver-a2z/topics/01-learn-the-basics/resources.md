# Learn the Basics — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

All links below are real (verified from the dataset or from research). No fabrication.

---

## 📺 Videos & Playlists

- [Striver — C++ / Language Basics (full video)](https://youtu.be/EAR7De6Goz4) — one-shot covering I/O, if/else, switch, loops, functions, arrays/strings (timestamps in the problems file).
- [Striver — Time & Space Complexity](https://youtu.be/FPu9Uld7W-E) — the canonical A2Z complexity lecture.
- [Striver — Must-Do Pattern Problems playlist](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3) — all 22 star/number/character patterns worked out.
- [Striver — Basic Maths (one-shot)](https://youtu.be/1xNbjMdbjug) — count digits, reverse, palindrome, Armstrong, divisors, prime, GCD in one video.
- [Striver — Recursion playlist](https://www.youtube.com/watch?v=yVdKa8dnKiE&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9) — introduction through Fibonacci, the exact recursion topics here.
- [Striver — C++ STL tutorial](https://www.youtube.com/watch?v=RRVYpIET_RU) — most-used STL containers and algorithms.
- [Striver — Basic Hashing](https://www.youtube.com/watch?v=KEs5UyBJ39g) — hashing, maps, collisions, division rule.

## 📝 Articles & Tutorials

- [takeUforward — Time and Space Complexity](https://takeuforward.org/time-complexity/time-and-space-complexity-strivers-a2z-dsa-course/) — the A2Z complexity write-up.
- [takeUforward — Must-do Pattern Problems](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) — all 22 patterns with code.
- [takeUforward — C++ STL tutorial](https://takeuforward.org/c/c-stl-tutorial-most-frequent-used-stl-containers/) — containers reference.
- [takeUforward — GCD of two numbers](https://takeuforward.org/data-structure/find-gcd-of-two-numbers/) — Euclid explained.
- [cp-algorithms — Euclidean algorithm for GCD](https://cp-algorithms.com/algebra/euclid-algorithm.html) — rigorous treatment + complexity proof.
- [cp-algorithms — Extended Euclidean algorithm](https://cp-algorithms.com/algebra/extended-euclid-algorithm.html) — for `ax + by = gcd(a,b)` (next step up).
- [GeeksforGeeks — Euclidean algorithms (Basic and Extended)](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) — code + walkthrough.
- [GeeksforGeeks — Introduction to Recursion](https://www.geeksforgeeks.org/dsa/introduction-to-recursion-2/) — base case, recursive case, stack.
- [GeeksforGeeks — Recursion Tree Method for Recurrences](https://www.geeksforgeeks.org/dsa/how-to-solve-time-complexity-recurrence-relations-using-recursion-tree-method/) — analyze recursive time complexity.
- [GeeksforGeeks — unordered_map in C++ STL](https://www.geeksforgeeks.org/cpp/unordered_map-in-cpp-stl/) — the hash-map workhorse.
- [GeeksforGeeks — map vs unordered_map in C++](https://www.geeksforgeeks.org/map-vs-unordered_map-c/) — O(log n) vs avg O(1) trade-off.
- [GeeksforGeeks — STL containers complexity table](https://www.geeksforgeeks.org/internal-data-structures-and-time-complexity-table-of-all-the-cpp-stl-containers/) — a handy cheat sheet.
- [Wikipedia — Euclidean algorithm](https://en.wikipedia.org/wiki/Euclidean_algorithm) — history and proofs.

## 🧮 Visualizers & Tools

- [VisuAlgo — algorithm visualizations](https://visualgo.net/en) — interactive visualizations (hashing, recursion-driven structures).
- [USFCA — Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — classic animated hashing / open addressing / chaining.
- [Coddy — Recursion Visualization](https://coddy.tech/visualize/concepts/recursion) — watch the call stack grow and unwind.
- [Recursion Tree Visualizer (Bruno Papa)](https://github.com/brpapa/recursion-tree-visualizer) — paste a function, see its recursion tree (great for Fibonacci).
- [Extended Euclidean Algorithm calculator](https://extendedeuclideanalgorithm.com/euclidean.php) — step-by-step GCD table.

## ❓ Most-Asked Interview Questions

1. **What is time complexity vs space complexity?** Time = how operation count grows with input `n`; space = how extra memory grows with `n`. Both use Big-O, dropping constants and lower-order terms.
2. **What's the difference between O, Θ, and Ω?** O = upper bound (worst case), Ω = lower bound (best case), Θ = tight bound (both). Interviews usually mean the worst-case tight bound by "O".
3. **How do you estimate if a solution is fast enough?** ~10⁸ simple ops ≈ 1s. For `n=10⁵`, O(n²)=10¹⁰ is too slow; aim for O(n log n) or better.
4. **Difference between pass-by-value and pass-by-reference?** Value copies the argument (local changes only); reference (`&`) shares the original (mutations persist, no copy cost). Use `const &` for read-only large objects.
5. **How do you reverse an integer, and what's the pitfall?** Loop `rev = rev*10 + n%10; n/=10`. Pitfall: 32-bit overflow — use `long long` or return 0 when the result leaves `[-2³¹, 2³¹-1]`.
6. **How do you check primality efficiently?** Test divisibility only up to √n; if no divisor found, it's prime. O(√n). For many queries, use the Sieve of Eratosthenes (O(n log log n)).
7. **Explain Euclid's GCD and its complexity.** `gcd(a,b)=gcd(b, a mod b)` until `b=0`. It runs in O(log min(a,b)) because the remainder shrinks at least by half every two steps.
8. **Why are all divisors found in O(√n)?** Divisors pair up as `(i, n/i)`; once past √n you'd only re-encounter the pair partners, so iterating to √n and adding both is sufficient.
9. **What is an Armstrong number?** A `k`-digit number equal to the sum of its digits each raised to power `k` (e.g., 153 = 1³+5³+3³).
10. **What are the two required parts of a recursive function?** A base case (stops recursion) and a recursive case (calls itself on a smaller subproblem). Missing/incorrect base case → stack overflow.
11. **Why is naive Fibonacci O(2ⁿ)?** Overlapping subproblems are recomputed; the call tree roughly doubles per level. Memoization or bottom-up iteration reduces it to O(n).
12. **How much space does recursion use?** O(depth) for the call stack — each active call holds a frame (parameters, locals, return address).
13. **What is hashing and its average complexity?** Mapping keys to buckets for average O(1) insert/find/erase. Worst case O(n) with many collisions or adversarial input.
14. **map vs unordered_map — when to use which?** `map` (balanced BST) gives sorted keys and guaranteed O(log n); `unordered_map` (hash table) gives average O(1) but no ordering and O(n) worst case. Use `unordered_map` for pure lookups, `map` when you need order.
15. **When prefer a frequency array over a hash map?** When keys are small, non-negative, bounded integers — a plain array is a collision-free perfect hash with lower constant factors.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*** — Ch. 3 (Growth of Functions / asymptotic notation), Ch. 4 (Recurrences & the recursion-tree method), Ch. 11 (Hash Tables), Ch. 31 §31.2 (Euclid's GCD).
- **Sedgewick & Wayne — *Algorithms*** — analysis of algorithms and symbol tables (hashing) chapters.
- **Striver's A2Z DSA Course/Sheet** — the parent course for this topic: [strivers-a2z-sheet](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z).
- Local library (if present): cross-reference `../../../books/` for CLRS / algorithms PDFs in this repo.

## 🔗 Official Problem Sources

- [Striver's A2Z DSA Sheet (Step 1: Learn the Basics)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official step page.
- [Strivers A2Z DSA Course/Sheet (root)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — full sheet index.
- [LeetCode — Reverse Integer](https://leetcode.com/problems/reverse-integer/) · [Palindrome Number](https://leetcode.com/problems/palindrome-number/) · [Armstrong Number](https://leetcode.com/problems/armstrong-number/) · [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) · [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) · [Frequency of the Most Frequent Element](https://leetcode.com/problems/frequency-of-the-most-frequent-element/).
- [LeetCode — Recursion tag](https://leetcode.com/tag/recursion/) · [Hash Table tag](https://leetcode.com/tag/hash-table/) · [Math tag](https://leetcode.com/tag/math/) — filter more practice by topic.
