# Strings [Basic and Medium] — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Strivers A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the canonical Striver playlist; Step 5 covers all string problems here.
- [takeUforward — YouTube channel](https://www.youtube.com/@takeUforward) — Raj Vikramaditya's video solutions for each Striver problem.
- [Longest Palindromic Substring — LeetCode #5 (NeetCode)](https://www.youtube.com/watch?v=XYQecbcd6_c) — clear expand-around-center walkthrough.
- [String to Integer (atoi) — LeetCode #8 (NeetCode)](https://www.youtube.com/watch?v=YA0LYrKI1CQ) — state-machine parsing with overflow handling.
- [Valid Anagram — LeetCode #242 (NeetCode)](https://www.youtube.com/watch?v=9UtInBqnCgA) — frequency-count technique.

## 📝 Articles & Tutorials

- [takeUforward — Remove Outermost Parentheses](https://takeuforward.org/data-structure/remove-outermost-parentheses)
- [takeUforward — Reverse Words in a String](https://takeuforward.org/data-structure/reverse-words-in-a-string/)
- [takeUforward — Largest Odd Number in a String](https://takeuforward.org/data-structure/largest-odd-number-in-a-string)
- [takeUforward — Longest Common Prefix](https://takeuforward.org/data-structure/longest-common-prefix)
- [takeUforward — Isomorphic Strings](https://takeuforward.org/data-structure/isomorphic-string)
- [takeUforward — Sort Characters by Frequency](https://takeuforward.org/data-structure/sort-characters-by-frequency)
- [takeUforward — Roman Numerals to Integer](https://takeuforward.org/data-structure/roman-numerals-to-integer)
- [takeUforward — Recursive atoi](https://takeuforward.org/data-structure/recursive-implementation-of-atoi)
- [takeUforward — Longest Palindromic Substring](https://takeuforward.org/data-structure/longest-palindromic-substring)
- [takeUforward — String Blogs Hub](https://takeuforward.org/blogs/string)
- [GeeksforGeeks — Top 50 String Coding Problems for Interviews](https://www.geeksforgeeks.org/top-50-string-coding-problems-for-interviews/)
- [GeeksforGeeks — Longest Palindromic Substring](https://www.geeksforgeeks.org/longest-palindromic-substring/)
- [GeeksforGeeks — Palindrome String Coding Problems](https://www.geeksforgeeks.org/dsa/string-palindrome/)
- [GeeksforGeeks — Manacher's Algorithm (linear-time LPS)](https://www.geeksforgeeks.org/dsa/manachers-algorithm-linear-time-longest-palindromic-substring-part-1/)
- [cp-algorithms — Prefix function / KMP](https://cp-algorithms.com/string/prefix-function.html) — foundation for the `a+a` rotation trick in linear time.
- [Medium — Expand From Center Algorithm (Palindrome DP pattern)](https://rajuhemanth456.medium.com/expand-from-center-algorithm-dp-pattern-palindrome-306b542ae916)

## 🧮 Visualizers & Tools

- [VisuAlgo — String matching visualizer](https://visualgo.net/en/stringmatching) — animated KMP/naive search useful for the rotation trick.
- [USFCA — Algorithm Visualizations (KMP, Boyer-Moore)](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — step-through string-matching automata.
- [LeetCode Playground](https://leetcode.com/playground/) — quickly test C++ string templates from the theory file.

## ❓ Most-Asked Interview Questions

1. **How do you check if two strings are anagrams?** Compare lengths; use a `freq[26]` array, `++` for one string and `--` for the other; anagram iff no count goes negative and lengths match. `O(n)` time, `O(1)` space.
2. **Why do two maps for isomorphic strings?** A single `s→t` map allows two distinct source chars to collide onto one target (e.g., `"ab"→"aa"`). The reverse map enforces a bijection.
3. **How do you find the longest palindromic substring efficiently?** Expand around all `2n-1` centers in `O(n²)`/`O(1)`; Manacher's algorithm does it in `O(n)`.
4. **What are the edge cases in `atoi`?** Leading spaces, optional single sign, no digits (return 0), trailing garbage (stop), and overflow — clamp to `[INT_MIN, INT_MAX]` accumulating in a wider type.
5. **How does the rotation trick work?** `b` is a rotation of `a` iff `|a|==|b|` and `b` is a substring of `a+a`; concatenation exposes every rotation as a window.
6. **How do you reverse words while handling extra spaces?** Tokenize on whitespace, discard empty tokens, join in reverse with single spaces; or reverse the whole string then reverse each word in place.
7. **Convert Roman numerals to integer?** Map symbols to values; add unless the current value is strictly less than the next (subtractive pairs like IV, IX, CM), in which case subtract.
8. **Find the maximum nesting depth of parentheses?** Track a running balance (`+1`/`-1`) and return the maximum value it reaches.
9. **How do you remove the outermost parentheses of each primitive?** Use a depth counter; append `(` only when depth>0 before incrementing, append `)` only when depth>0 after decrementing.
10. **How do you sort characters by frequency?** Count frequencies, sort characters by count descending (or bucket sort by frequency), rebuild the string.
11. **What's the difference between substring and subsequence?** A substring is contiguous; a subsequence preserves order but may skip characters. There are `n(n+1)/2` substrings.
12. **How do you count substrings with exactly `k` distinct characters?** `exactly(k) = atMost(k) − atMost(k−1)` using a sliding window.
13. **Largest odd number formable as a prefix?** Scan from the right to the first odd digit at index `i`; answer is `s[0..i]`, else `""`.
14. **When to use `freq[26]` vs `freq[256]` vs a hash map?** `26` for lowercase-only, `256` for full ASCII, a hash map for arbitrary/large or Unicode key sets.
15. **How does the "sum of beauty of all substrings" work?** For each substring, beauty = max frequency − min non-zero frequency; enumerate substrings incrementally with a `freq[26]` in `O(n²)`.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Ch. 32 "String Matching"** — theoretical grounding for KMP/automata used in rotation and pattern search. See also [../../../books/](../../../books/) if local copies are present.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Ch. 5 "Strings"** — tries, substring search, and regular expressions.
- [GeeksforGeeks — String Data Structure hub](https://www.geeksforgeeks.org/dsa/string-data-structure/) — free tutorial series and practice.
- [NeetCode 150 — Strings section](https://neetcode.io/practice) — curated interview-frequency ordering.

## 🔗 Official Problem Sources

- [Striver A2Z Sheet — Step 5: Strings (Basic & Medium)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official step listing these problems.
- [LeetCode — String tag](https://leetcode.com/tag/string/) — all string problems, filterable by difficulty.
- [LeetCode — Two Pointers tag](https://leetcode.com/tag/two-pointers/) — for palindrome/reverse-style problems.
- [LeetCode — Hash Table tag](https://leetcode.com/tag/hash-table/) — for anagram/isomorphic/frequency problems.
- [GeeksforGeeks — Top 50 String Problems](https://www.geeksforgeeks.org/top-50-string-coding-problems-for-interviews/) — companion practice set.
