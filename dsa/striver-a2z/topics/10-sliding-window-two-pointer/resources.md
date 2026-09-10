# Sliding Window & Two Pointer — Resources & References

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

All links below are real (from research or the topic data file). Striver/takeUforward first, then broader references.

---

## 📺 Videos & Playlists

- [Striver — Longest Substring Without Repeating Characters](https://youtu.be/-zSxTJkcdAo?si=I2zfR-vlDMg0zU9z) — the canonical variable-window walkthrough.
- [Striver — Max Consecutive Ones III](https://youtu.be/3E4JBHSLpYk?si=SoOW64pP6otEKxBw) — "at most K zeros" longest window.
- [Striver — Fruit Into Baskets](https://youtu.be/e3bs0uA1NhQ?si=gR8pO62u-nJeFAXk) — at-most-2-distinct as a window.
- [Striver — Longest Repeating Character Replacement](https://youtu.be/_eNhaDCr6P0?si=pBWcEjozF5poom0p) — the `len − maxFreq ≤ K` invariant.
- [Striver — Binary Subarrays With Sum](https://youtu.be/XnMdNUkX6VM?si=Nyt8EveeLUg8lmty) — the `atMost(goal) − atMost(goal−1)` trick.
- [Striver — Count Number of Nice Subarrays](https://youtu.be/j_QOv9OT9Og?si=Oq5-5hyFkzVSOZpP) — odd→1 mapping + exactly-K.
- [Striver — Number of Substrings Containing All Three Characters](https://youtu.be/xtqN4qlgr8s?si=kuaLHVOLXhh5Z2tW) — last-seen-index counting.
- [Striver — Maximum Points You Can Obtain from Cards](https://youtu.be/pBWCOCS636U?si=-X64rY67noxvOwrG) — complement fixed window.
- [Striver — Longest Substring With At Most K Distinct Characters](https://youtu.be/teM9ZsVRQyc?si=Kh0_u6aCkkBU3Q33) — generalized distinct-count window.
- [Striver — Subarrays with K Different Integers](https://youtu.be/7wYGbV_LsX4?si=KWa48RgLDCvdNqRb) — exactly-K distinct.
- [Striver — Minimum Window Substring](https://youtu.be/WJaij9ffOIY?si=-xnsWIH84zWU0ICd) — shortest valid window with need/have.

---

## 📝 Articles & Tutorials

- [takeUforward — Longest Substring Without Repeating Characters](https://takeuforward.org/data-structure/length-of-longest-substring-without-any-repeating-character/) — step-by-step article companion to the video.
- [takeUforward — Max Consecutive Ones III](https://takeuforward.org/data-structure/max-consecutive-ones-iii) — window with limited flips.
- [takeUforward — Longest Substring With At Most K Distinct](https://takeuforward.org/data-structure/longest-substring-with-at-most-k-distinct-characters) — distinct-count template.
- [GeeksforGeeks — Window Sliding Technique](https://www.geeksforgeeks.org/window-sliding-technique/) — the foundational GfG tutorial.
- [GeeksforGeeks — Sliding Window: Identify, Solve & Interview Questions](https://www.geeksforgeeks.org/sliding-window-problems-identify-solve-and-interview-questions/) — how to recognize window problems.
- [GeeksforGeeks — Sliding Window Interview Questions](https://www.geeksforgeeks.org/dsa/commonly-asked-interview-questions-on-sliding-window-technique/) — fixed vs variable, curated Qs.
- [LeetCode Discuss — Summary of Sliding Window Patterns for Subarray/Substring](https://leetcode.com/discuss/post/1122776/summary-of-sliding-window-patterns-for-subarray-substring/) — the famous "at most / exactly K" pattern post.
- [LeetCode Discuss — Sliding Window Technique and Question Bank](https://leetcode.com/discuss/study-guide/1773891/sliding-window-technique-and-question-bank) — grouped problem bank.
- [LeetCode Discuss — Two Pointers and Sliding Window Study Guide](https://leetcode.com/discuss/post/5078450/two-pointers-and-sliding-window-study-gu-tx1w/) — differences and when to use each.
- [LeetCode Discuss — Sliding Window Made Simple: 5 Templates](https://leetcode.com/discuss/post/8397648/sliding-window-made-simple-the-only-5-te-wwj8/) — five reusable templates.
- [labuladong — Sliding Window Algorithm Code Template](https://labuladong.online/en/algo/essential-technique/sliding-window-framework/) — a single unified framework.
- [NeetCode — Minimum Window Substring solution](https://www.neetcode.io/solutions/minimum-window-substring) — clean shortest-window write-up.
- [Medium (leetCode-patterns) — Sliding Windows for Strings](https://medium.com/leetCode-patterns/leetCode-pattern-2-sliding-windows-for-strings-e19af105316b) — pattern catalogue for string windows.

---

## 🧮 Visualizers & Tools

- [GeeksforGeeks — Sliding Window Visualizer (HTML/CSS/JS)](https://www.geeksforgeeks.org/sliding-window-visualizer-using-html-css-and-javascript/) — interactive window animation.
- [LeetCode Discuss — Fixed and Variable Window Visualized](https://leetcode.com/discuss/post/8374718/this-is-what-sliding-window-actually-loo-g3e5/) — visual mental model of both variants.
- [algo.monster — Minimum Window Substring (animated)](https://algo.monster/liteproblems/76) — annotated animated solution.

---

## ❓ Most-Asked Interview Questions

1. **What is the difference between fixed and variable sliding windows?** Fixed: window size `k` is given, both ends move together, no inner loop. Variable: window grows on expand and shrinks on a condition; size is not fixed.
2. **When can you use a sliding window at all?** Only when the feasibility is monotone: extending an invalid window keeps it invalid, and shrinking a valid window keeps it valid. Otherwise use prefix sums + hashing.
3. **Why is sliding window O(n) even with a nested-looking loop?** Because `left` and `right` each advance at most `n` times total across the whole run — the inner `while` is amortized, not per-iteration.
4. **How do you count subarrays with *exactly* K of something?** `exactly(K) = atMost(K) − atMost(K−1)`; counting "exactly" directly in one pass is error-prone.
5. **Longest vs shortest valid window — how does the code differ?** Longest: record the answer *after* restoring validity. Shortest: record *while* the window is feasible, then shrink to try to beat it.
6. **Why does sliding window sum fail with negative numbers?** Growing the window can decrease the sum, breaking monotonicity; use prefix-sum + hashmap for arbitrary integers.
7. **Explain Longest Repeating Character Replacement's `maxFreq` not decreasing.** The window only expands when a strictly longer valid window is achievable, so a stale `maxFreq` never produces a wrong larger answer.
8. **How do you solve "at most K distinct"?** Frequency map; expand right, shrink left while `map.size() > K`; track max length (longest) or sum of `(r−l+1)` (count).
9. **How is Maximum Points from Cards a window problem?** Taking k from the ends = leaving a contiguous middle of size `n−k`; maximize taken = `total − min-sum window of size n−k`.
10. **What data structure tracks the window summary?** A fixed-size frequency array for small alphabets (O(1) ops) or a hash map for large/unknown key spaces.
11. **Two pointers vs sliding window — are they the same?** Sliding window is a same-direction two-pointer specialization that validates a contiguous range; classic two-pointer (e.g., opposite ends on a sorted array) need not track a window at all.
12. **How do you handle Minimum Window Substring's multiplicity?** Track `need[c]` and `have[c]`; a char is "satisfied" when `have[c] == need[c]`; the window is feasible when all distinct required chars are satisfied (`formed == required`).
13. **Why is Minimum Window *Subsequence* not O(n) sliding window?** Order matters and gaps are allowed, so simple contiguous feasibility isn't monotone; use two-pass two-pointer or DP → O(m·n).
14. **How do you avoid off-by-one on window length?** For the closed range `[left, right]`, length is `right − left + 1`.
15. **What's a fast way to spot a window problem in an interview?** Keywords: *contiguous*, *subarray/substring*, *longest/shortest/number of*, *at most/exactly K* — combined they almost always mean a window.

---

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*** — while it has no dedicated "sliding window" chapter, the amortized-analysis chapter (aggregate/accounting method) is the theory behind why two moving pointers cost O(n). See also [`../../../books/`](../../../books/) if present in this repo.
- **Competitive Programmer's Handbook (Antti Laaksonen)** — free PDF; sections on two-pointers and range queries. [cses.fi/book/book.pdf](https://cses.fi/book/book.pdf)
- **NeetCode 150 / roadmap** — the "Sliding Window" group with video solutions. [neetcode.io](https://neetcode.io/)
- **LeetCode Explore — Learn cards** on arrays/strings cover two-pointer fundamentals.

---

## 🔗 Official Problem Sources

- **takeUforward A2Z Sheet — Step 10 (Sliding Window & Two Pointer):** [takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/)
- **LeetCode Tag — Sliding Window:** [leetcode.com/tag/sliding-window/](https://leetcode.com/tag/sliding-window/)
- **LeetCode Tag — Two Pointers:** [leetcode.com/tag/two-pointers/](https://leetcode.com/tag/two-pointers/)
- **LeetCode Discuss — Sliding Window Question Bank:** [leetcode.com/discuss/study-guide/1773891](https://leetcode.com/discuss/study-guide/1773891/sliding-window-technique-and-question-bank)
- **GeeksforGeeks — Sliding Window Problems hub:** [geeksforgeeks.org/sliding-window-problems-identify-solve-and-interview-questions](https://www.geeksforgeeks.org/sliding-window-problems-identify-solve-and-interview-questions/)
