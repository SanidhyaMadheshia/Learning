# Strings [Advanced] — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

All links below are real, drawn from the data file and web research. Use them to go deeper on KMP/LPS, the Z-function, Rabin–Karp, and prefix-function applications.

---

## 📺 Videos & Playlists

- [takeUforward — KMP Algorithm / LPS array (article + video)](https://takeuforward.org/data-structure/kmp-algorithm-or-lps-array) — Striver's canonical KMP explanation, LPS build and search, interview-aligned.
- [takeUforward — Longest Happy Prefix](https://takeuforward.org/data-structure/longest-happy-prefix) — direct LPS application walkthrough.
- [takeUforward — Hashing in Strings](https://takeuforward.org/data-structure/hashing-in-strings) — string hashing foundation for Rabin–Karp.
- [takeUforward — Count and Say](https://takeuforward.org/data-structure/count-and-say) — run-length simulation, step by step.
- [takeUforward — Minimum Bracket Reversals](https://takeuforward.org/data-structure/minimum-number-of-bracket-reversals-needed-to-make-an-expression-balanced) — counting/stack technique.

---

## 📝 Articles & Tutorials

- [cp-algorithms — Prefix function (KMP)](https://cp-algorithms.com/string/prefix-function.html) — the definitive linear-time prefix-function reference with applications.
- [cp-algorithms — Z-function](https://cp-algorithms.com/string/z-function.html) — rigorous Z-array derivation and `[l,r]` window proof.
- [cp-algorithms — Rabin–Karp](https://cp-algorithms.com/string/rabin-karp.html) — rolling hash matching.
- [cp-algorithms — String hashing](https://cp-algorithms.com/string/string-hashing.html) — modulus/base choices and collision probability.
- [GfG — Prefix Function and KMP for Competitive Programming](https://www.geeksforgeeks.org/competitive-programming/prefix-function-and-kmp-algorithm-for-competitive-programming/) — concise LPS + KMP with code.
- [GfG — Z algorithm (linear pattern search)](https://www.geeksforgeeks.org/dsa/z-algorithm-linear-time-pattern-searching-algorithm/) — Z-based matching walkthrough.
- [GfG — Rabin-Karp Algorithm for Pattern Searching](https://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/) — rolling hash with examples.
- [GfG — Lexicographically minimum string rotation](https://www.geeksforgeeks.org/dsa/lexicographically-minimum-string-rotation/) — Booth-style minimal rotation.
- [AlgoMaster — KMP Algorithm](https://algomaster.io/learn/dsa/kmp-algorithm) — clean intuition for the failure-shift.
- [LeetCode Discuss — Z Function of a String](https://leetcode.com/discuss/study-guide/4677228/LC-Blogs-3-or-Z-Function-of-a-String/) — study-guide blog with LC applications.
- [9oelm — Shortest Palindrome via KMP](https://9oelm.github.io/2022-01-06--find-the-shortest-palindrome-an-intensive-review-of-kmp(knuth-morris-pratt)-algorithm/) — deep dive tying KMP to shortest palindrome.
- [OpenGenus — Z Algorithm function](https://iq.opengenus.org/z-algorithm-function/) — compact Z-function reference.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — String Matching (KMP, Z, Rabin–Karp)](https://visualgo.net/en/stringmatching) — animated step-through of all three matchers.
- [USFCA — Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — classic algorithm animations.
- [Wikipedia — Lexicographically minimal string rotation](https://en.wikipedia.org/wiki/Lexicographically_minimal_string_rotation) — Booth's algorithm description and pseudocode.

---

## ❓ Most-Asked Interview Questions

1. **What does LPS[i] mean?** The length of the longest proper prefix of `s[0..i]` that is also a suffix of `s[0..i]`.
2. **Why is KMP `O(n+m)`?** The `len` pointer increases at most `m` times over the build and `n` times over the search; total decreases (fallbacks) are bounded by total increases, giving amortized linear time.
3. **Difference between LPS and Z arrays?** LPS[i] measures the longest border *ending* at `i`; Z[i] measures the longest prefix-match *starting* at `i`. Both are computable in `O(n)`.
4. **How do you find a string's period with KMP?** `period = n − lps[n-1]`; the string is fully periodic iff `n % period == 0` and `lps[n-1] > 0`.
5. **How does Rabin–Karp update a window hash in O(1)?** Subtract the leading character's weighted value, multiply by the base, add the new trailing character — all modulo a large prime.
6. **How do you handle hash collisions?** Verify the substring character-by-character on a hash match, or use double hashing (two moduli) to make collisions negligibly likely.
7. **Why add `+M` in rolling-hash subtraction in C++?** Subtracting can produce a negative intermediate; adding the modulus before `%` keeps the result in `[0, M)`.
8. **How to solve Shortest Palindrome in linear time?** Build `s + '#' + reverse(s)`, compute LPS; `lps.back()` is the longest palindromic prefix length; prepend the reversed remaining suffix.
9. **What is a "happy prefix"?** A non-empty proper prefix that is also a suffix — exactly `lps[n-1]`.
10. **How to detect if a string is a repetition of a substring?** With KMP: `len = lps[n-1]`; it repeats iff `n % (n − len) == 0` and `len != 0`.
11. **How to find the lexicographically smallest rotation efficiently?** Booth's algorithm — run a modified failure function over `s + s` in `O(n)`.
12. **When choose Z over KMP (or vice versa)?** Z is simpler to code for "match length from a position" and distinct-substring problems; KMP is natural for streaming search and periodicity/border problems.
13. **What's the worst case of Rabin–Karp and when does it happen?** `O(n·m)` when many windows hash-collide with the pattern (e.g., adversarial input against a known modulus); good/random moduli avoid it.
14. **Why does the separator in `pat + '#' + txt` matter?** It prevents a match from spanning the boundary; it must be a character absent from both strings.
15. **How to count palindromic subsequences?** Interval DP `dp[i][j]` using inclusion–exclusion (`dp[i+1][j] + dp[i][j-1] − dp[i+1][j-1]`), adding inner counts when `s[i]==s[j]`, all under a modulus.

---

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Chapter 32 "String Matching"** — naïve, Rabin–Karp, finite-automaton, and KMP with correctness proofs.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Section 5.3 "Substring Search"** — Knuth–Morris–Pratt, Boyer–Moore, Rabin–Karp.
- **Competitive Programmer's Handbook (Antti Laaksonen), "String algorithms" chapter** — Z-array, string hashing, and applications.
- Cross-link: see [`../../../books/`](../../../books/) for any local algorithm-book PDFs/notes in this repo.

---

## 🔗 Official Problem Sources

- [takeUforward — Striver A2Z DSA Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the parent sheet; Step 18 "Strings" lives here.
- [LeetCode — Implement strStr()](https://leetcode.com/problems/implement-strstr/) — canonical KMP practice.
- [LeetCode — Longest Happy Prefix](https://leetcode.com/problems/longest-happy-prefix/) — LPS application.
- [LeetCode — Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/) — KMP application.
- [LeetCode — Count and Say](https://leetcode.com/problems/count-and-say/)
- [LeetCode — Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)
- [LeetCode — Count Palindromic Subsequences](https://leetcode.com/problems/count-palindromic-subsequences/)
- [LeetCode — String Matching tag](https://leetcode.com/tag/string-matching/) — full tagged problem list for drilling this topic.
