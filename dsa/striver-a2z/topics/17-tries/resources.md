# Tries — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Trie Playlist (takeUforward)](https://www.youtube.com/watch?v=dBGUmUQhjaM&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp) — the full A2Z trie series: implementation, advanced ops, XOR problems.
- [Striver — Longest Word with All Prefixes](https://www.youtube.com/watch?v=AWnBa91lThI&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=3) — building & scanning a trie for prefix chains.
- [Striver — Number of Distinct Substrings using Trie](https://www.youtube.com/watch?v=RV0QeTyHZxo&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=4) — suffix-insertion node counting.
- [Striver — Bit Prerequisites for Trie](https://youtu.be/5iyuU4hQFrw) — the bit-manipulation warm-up for XOR tries.
- [Striver — Maximum XOR of Two Numbers in an Array](https://www.youtube.com/watch?v=EIhAwfHubE8&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=6) — greedy opposite-bit walk on a bit-trie.
- [Striver — Maximum XOR with an Element (offline queries)](https://www.youtube.com/watch?v=Q8LhG9Pi5KM&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=7) — sorting queries + incremental insertion.

---

## 📝 Articles & Tutorials

- [takeUforward — Implement Trie (Part 1)](https://takeuforward.org/data-structure/implement-trie-1/) — canonical Striver walkthrough of insert/search/startsWith.
- [takeUforward — Implement Trie II (advanced ops)](https://takeuforward.org/data-structure/implement-trie-ii/) — counts, erase, and the longest-prefix-word problem.
- [takeUforward — Distinct Substrings using Trie](https://takeuforward.org/data-structure/number-of-distinct-substrings-in-a-string-using-trie/) — suffix trie node counting.
- [takeUforward — Maximum XOR of Two Numbers](https://takeuforward.org/data-structure/maximum-xor-of-two-numbers-in-an-array/) — bit-trie XOR maximization.
- [takeUforward — Maximum XOR Queries with Trie](https://takeuforward.org/trie/maximum-xor-queries-trie/) — offline constrained XOR queries.
- [GeeksforGeeks — Trie: Insert and Search](https://www.geeksforgeeks.org/dsa/trie-insert-and-search/) — clear intro with diagrams.
- [GeeksforGeeks — Trie Data Structure in C++](https://www.geeksforgeeks.org/cpp/trie-data-structure-in-cpp/) — C++-specific implementation.
- [GeeksforGeeks — Maximum XOR of Two Numbers in an Array (Set 2)](https://www.geeksforgeeks.org/maximum-xor-of-two-numbers-in-an-array-set-2/) — bit-trie approach.
- [GeeksforGeeks — Auto-complete feature using Trie](https://www.geeksforgeeks.org/auto-complete-feature-using-trie/) — a classic applied use case.
- [LeetCode Discuss — Beginner-friendly guide to Trie](https://leetcode.com/discuss/post/931977/beginner-friendly-guide-to-trie-tutorial-practice-problems/) — tutorial + curated practice list.
- [LeetCode Discuss — All you need to know about Trie](https://leetcode.com/discuss/post/4161389/All-you-need-to-know-about-trie/) — consolidated patterns & templates.
- [Tech Interview Handbook — Trie cheatsheet](https://www.techinterviewhandbook.org/algorithms/trie/) — concise interview cheat sheet.
- [interviewing.io — Tries Interview Questions](https://interviewing.io/tries-interview-questions) — how tries show up in senior interviews.

---

## 🧮 Visualizers & Tools

- [USFCA — Trie Visualization](https://www.cs.usfca.edu/~galles/visualization/Trie.html) — step through insert/search animations.
- [VisuAlgo — Suffix Trie / Tree](https://visualgo.net/en/suffixtree) — visualize suffix structures related to distinct-substring counting.

---

## ❓ Most-Asked Interview Questions

1. **What is a trie and how does it differ from a hash set?**
   A prefix tree where shared prefixes share nodes; unlike a hash set it answers *prefix* queries in `O(prefix length)` and supports ordered/prefix iteration.

2. **What are the time complexities of insert/search/startsWith?**
   All `O(L)` where `L` is the key length — independent of the number of stored keys.

3. **Why doesn't `startsWith` check the end flag?**
   Prefix existence only requires the path to exist; the terminal flag marks whole words, which is irrelevant for a prefix query.

4. **How much space does a trie use?**
   `O(total characters · R)` with `R`-slot arrays (`R`=alphabet), or `O(total characters)` amortized with hash-map children.

5. **How do you delete a word from a trie?**
   Use `countEnd`/`countPrefix` counters; decrement along the path. Only physically free a node when both counters reach zero and it has no children.

6. **How do you count how many words start with a prefix?**
   Store a `countPrefix` at each node incremented on insert; return the prefix-node's value.

7. **What is a bit-trie and when do you use it?**
   A trie with branching factor 2 storing numbers' binary bits MSB→LSB; used for XOR maximization and range/bitmask queries.

8. **Why does the greedy opposite-bit strategy give the maximum XOR?**
   XOR of higher bits contributes more (`2^i`); greedily setting the highest possible bits to 1 (by choosing opposite bits when available) dominates any lower-bit gain.

9. **How many bits should the bit-trie use?**
   Enough to cover the max value — typically 31 for signed ints up to ~2·10⁹, or 32 for unsigned.

10. **How do you solve "max XOR with an element ≤ m" efficiently?**
    Offline: sort array and queries by the limit, insert elements incrementally as they become eligible, then greedy-query; restore original order.

11. **How do you count distinct substrings with a trie?**
    Insert all suffixes; the number of newly created nodes equals the number of distinct substrings.

12. **Array-of-children vs hash-map-of-children — trade-offs?**
    Arrays are `O(1)` and cache-friendly but waste memory for sparse/large alphabets; hash maps save space at the cost of constant-factor speed.

13. **Can a trie store duplicate words?**
    Yes — use a `countEnd` counter instead of a boolean flag to track multiplicity.

14. **What real systems use tries?**
    Autocomplete/typeahead, spell-checkers, IP routing (longest-prefix match), and dictionary/word-game engines.

15. **Trie vs suffix automaton for substring counting?**
    A suffix trie is `O(n²)`; a suffix automaton (or suffix array + LCP) achieves `O(n)`/`O(n log n)` for large strings.

---

## 📚 Books & Courses

- **CLRS — Introduction to Algorithms** — Chapter on strings/radix structures (radix trees / tries background). See cross-links in [../../../books/](../../../books/) if present.
- **Sedgewick & Wayne — Algorithms (4th ed.)** — Chapter 5.2 "Tries" (R-way tries and TSTs), an excellent formal treatment.
- **Competitive Programmer's Handbook (Antti Laaksonen)** — string algorithms & tries chapter (free PDF).
- [Educative — Implementing Tries in C++ and Java](https://www.educative.io/courses/advanced-data-structures-implementing-tries-in-cpp-and-java/maximum-xor) — course module including bit-trie max-XOR.

---

## 🔗 Official Problem Sources

- [takeUforward — A2Z DSA Sheet, Step 17: Tries](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the official Striver step this package covers.
- [LeetCode — Trie tag](https://leetcode.com/tag/trie/) — all trie-tagged problems.
- [LeetCode — Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) — the canonical trie problem.
- [LeetCode — Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) — bit-trie XOR.
- [LeetCode — Maximum XOR With an Element From Array](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/) — offline constrained XOR.
