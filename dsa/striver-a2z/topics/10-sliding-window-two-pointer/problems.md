# Sliding Window & Two Pointer — Problems (by Pattern)

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)
>
> Problems are **grouped by pattern (sub-step)**, in data order. Every problem from the data appears exactly once, with an intuition, a worked example, and a memorable analogy.

---

## Medium Problems

### Longest Substring Without Repeating Characters  🟡

**Links:** [LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/) · [🎥 YouTube](https://youtu.be/-zSxTJkcdAo?si=I2zfR-vlDMg0zU9z) · [Article](https://takeuforward.org/data-structure/length-of-longest-substring-without-any-repeating-character/)

**Intuition / Approach:** Longest **variable window** with the invariant "no repeated character". Expand `right`; store each char's last index. When `s[right]` was seen inside the current window, jump `left` to `lastIndex+1`. Track the max window length throughout.

**Example:** `s = "abcabcbb"` → windows grow `a, ab, abc` (len 3); at second `a`, `left` jumps past first `a`; best stays 3. Output `3`.

**Analogy:** A hallway of numbered lockers where you can't have two lockers with the same label open at once — the moment you open a duplicate, you must close everything up to and including the earlier copy.

*Complexity: O(n) time, O(Σ) space.*

### Max Consecutive Ones III  🟡

**Links:** [LeetCode](https://leetcode.com/problems/max-consecutive-ones-iii/) · [🎥 YouTube](https://youtu.be/3E4JBHSLpYk?si=SoOW64pP6otEKxBw) · [Article](https://takeuforward.org/data-structure/max-consecutive-ones-iii)

**Intuition / Approach:** Longest window containing **at most K zeros** (each zero is a "flip"). Expand `right`, count zeros; while `zeros > K`, shrink `left` (decrementing the zero count when a zero leaves). Answer is the max window length.

**Example:** `nums = [1,1,1,0,0,0,1,1,1,1,0], K = 2` → best window `[1,1,1,1,0]`-region of length **6** (flip the two zeros inside). Output `6`.

**Analogy:** You have 2 "cheat coupons" to turn a broken bulb (0) into a working one (1). Walk the string of bulbs keeping the longest stretch where you never need more than 2 coupons.

*Complexity: O(n) time, O(1) space.*

### Fruit Into Baskets  🟡

**Links:** [LeetCode](https://leetcode.com/problems/fruit-into-baskets/description/) · [🎥 YouTube](https://youtu.be/e3bs0uA1NhQ?si=gR8pO62u-nJeFAXk) · [Article](https://takeuforward.org/data-structure/fruit-into-baskets)

**Intuition / Approach:** This is exactly "**longest subarray with at most 2 distinct** values". Maintain a frequency map; expand `right`; while the map has more than 2 keys, shrink `left`. Track the max window size.

**Example:** `fruits = [1,2,3,2,2]` → window `[2,3,2,2]` has 2 distinct types, length **4**. Output `4`.

**Analogy:** You carry exactly two baskets and can only pick from consecutive trees; as soon as a third fruit type appears, you must drop trees from the start until you're back to two kinds.

*Complexity: O(n) time, O(1) space (≤ 3 keys).*

### Longest Repeating Character Replacement  🔴

**Links:** [LeetCode](https://leetcode.com/problems/longest-repeating-character-replacement/) · [🎥 YouTube](https://youtu.be/_eNhaDCr6P0?si=pBWcEjozF5poom0p) · [Article](https://takeuforward.org/data-structure/longest-repeating-character-replacement)

**Intuition / Approach:** A window is valid if `windowLength − maxFreqInWindow ≤ K` (the non-dominant chars can all be replaced). Expand `right`, update the dominant-char frequency. If `len − maxFreq > K`, shrink once. `maxFreq` need not be decreased — the answer only ever grows.

**Example:** `s = "AABABBA", K = 1` → window `"AABA"` (dominant `A`×3, 1 replacement) length **4**. Output `4`.

**Analogy:** Painting a fence where you're allowed **K** touch-up strokes. Keep the longest stretch where the majority color already covers all but at most K planks.

*Complexity: O(n) time, O(1) space (26 letters).*

### Binary Subarrays With Sum  🔴

**Links:** [LeetCode](https://leetcode.com/problems/binary-subarrays-with-sum/) · [🎥 YouTube](https://youtu.be/XnMdNUkX6VM?si=Nyt8EveeLUg8lmty) · [Article](https://takeuforward.org/data-structure/binary-subarray-with-sum)

**Intuition / Approach:** Count subarrays with sum **exactly = goal** in a 0/1 array via `atMost(goal) − atMost(goal−1)`. `atMost(x)` slides a window, shrinking while `windowSum > x`, adding `(right − left + 1)` per step.

**Example:** `nums = [1,0,1,0,1], goal = 2` → `atMost(2)=8`, `atMost(1)=4`, answer `8 − 4 = 4`. Output `4`.

**Analogy:** Counting exactly-$2 shopping baskets = (baskets costing ≤ $2) minus (baskets costing ≤ $1). The "exactly" ledger is the difference of two "at most" ledgers.

*Complexity: O(n) time, O(1) space.*

### Count number of Nice subarrays  🔴

**Links:** [LeetCode](https://leetcode.com/problems/count-number-of-nice-subarrays/) · [🎥 YouTube](https://youtu.be/j_QOv9OT9Og?si=Oq5-5hyFkzVSOZpP) · [Article](https://takeuforward.org/data-structure/count-number-of-nice-subarrays)

**Intuition / Approach:** Map each element to `1` if odd, `0` if even; a "nice" subarray has **exactly k odd numbers** → exactly-k of the transformed array. Reuse `atMost(k) − atMost(k−1)`.

**Example:** `nums = [1,1,2,1,1], k = 3` → transform `[1,1,0,1,1]`, count subarrays with exactly 3 ones = **2** (`[1,1,2,1]` and `[1,2,1,1]`). Output `2`.

**Analogy:** Same "exactly = atMost minus atMost" ledger trick as before, just relabeling odd numbers as the coins that count.

*Complexity: O(n) time, O(1) space.*

### Number of Substrings Containing All Three Characters  🔴

**Links:** [LeetCode](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/) · [🎥 YouTube](https://youtu.be/xtqN4qlgr8s?si=kuaLHVOLXhh5Z2tW) · [Article](https://takeuforward.org/data-structure/number-of-substring-containing-all-three-characters)

**Intuition / Approach:** For each `right`, track the **last seen index** of `a`, `b`, `c`. Any substring ending at `right` and starting at or before `min(lastA,lastB,lastC)` contains all three. Add `min(lastA,lastB,lastC) + 1` to the count each step.

**Example:** `s = "abcabc"` → at index 2 (`c`) add 1; index 3 add 2; index 4 add 3; index 5 add 4 → total **10**. Output `10`.

**Analogy:** To photograph all three friends in one shot, your left edge can be anywhere up to the earliest of their most-recent appearances — every such starting point is a valid group photo.

*Complexity: O(n) time, O(1) space.*

### Maximum Points You Can Obtain from Cards  🟡

**Links:** [LeetCode](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/) · [🎥 YouTube](https://youtu.be/pBWCOCS636U?si=-X64rY67noxvOwrG) · [Article](https://takeuforward.org/data-structure/maximum-point-you-can-obtain-from-cards)

**Intuition / Approach:** You take `k` cards from either end → the **untaken** cards form a contiguous window of size `n − k`. Maximize picked = `total − (minimum-sum window of size n−k)`. A single fixed-size window pass finds that minimum. (Equivalently, slide a prefix from the left and a suffix from the right.)

**Example:** `cards = [1,2,3,4,5,6,1], k = 3`, `total = 22`, min window of size 4 = `2+3+4+5 = 14` → answer `22 − 14 = 8`? Check ends `6+1 + 1 = ...`; taking `[1,6,5]`→ **12**. Best = `total − min(n−k window)` = `22 − 10`? min window `[1,2,3,4]=10` → **12**. Output `12`.

**Analogy:** You must eat 3 cookies only from the two ends of a row; the ones you leave behind are a solid middle chunk — leave behind the *cheapest* contiguous chunk so what you eat is worth the most.

*Complexity: O(k) or O(n) time, O(1) space.*

---

## Hard Problems

### Longest Substring With At Most K Distinct Characters  🔴

**Links:** [LeetCode](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) · [🎥 YouTube](https://youtu.be/teM9ZsVRQyc?si=Kh0_u6aCkkBU3Q33) · [Article](https://takeuforward.org/data-structure/longest-substring-with-at-most-k-distinct-characters)

**Intuition / Approach:** Longest variable window with a frequency map; expand `right`; while the map holds more than `K` distinct keys, shrink `left`. Record the max window length. (Fruit Into Baskets is this with `K = 2`.)

**Example:** `s = "eceba", K = 2` → best window `"ece"` length **3**. Output `3`.

**Analogy:** A tasting menu where your tray can display at most K distinct dishes; keep adding to the right, and when a `K+1`-th dish appears, clear from the left until only K kinds remain.

*Complexity: O(n) time, O(K) space.*

### Subarrays with K Different Integers  🟡

**Links:** [LeetCode](https://leetcode.com/problems/subarrays-with-k-different-integers/) · [🎥 YouTube](https://youtu.be/7wYGbV_LsX4?si=KWa48RgLDCvdNqRb) · [Article](https://takeuforward.org/data-structure/subarray-with-k-different-integers)

**Intuition / Approach:** Count subarrays with **exactly K** distinct integers = `atMostKDistinct(K) − atMostKDistinct(K−1)`. Each `atMost` is a linear distinct-count window that adds `(right − left + 1)` per step.

**Example:** `nums = [1,2,1,2,3], K = 2` → `atMost(2)=12`, `atMost(1)=5`, answer `12 − 5 = 7`. Output `7`.

**Analogy:** Same "exactly = atMost − atMost" accounting, but the thing we cap is *how many distinct flavors* are in the bag, not a sum.

*Complexity: O(n) time, O(K) space.*

### Minimum Window Substring  🔴

**Links:** [LeetCode](https://leetcode.com/problems/minimum-window-substring/) · [🎥 YouTube](https://youtu.be/WJaij9ffOIY?si=-xnsWIH84zWU0ICd)

**Intuition / Approach:** Shortest **valid** window: expand `right` until the window contains every character of `t` (with multiplicity), then greedily shrink `left` while it stays feasible, recording the shortest length. Use `need[]`/`have[]` counts and a `formed == required` feasibility flag.

**Example:** `s = "ADOBECODEBANC", t = "ABC"` → first feasible window `"ADOBEC"`, shrinks and later finds `"BANC"` of length **4**. Output `"BANC"`.

**Analogy:** Packing a survival kit that must include one of each required item; you keep adding items walking forward, and once the kit is complete you throw away everything non-essential from the back to make it as small as possible.

*Complexity: O(n + |t|) time, O(Σ) space.*

### Minimum Window Subsequence  🔴

**Links:** [LeetCode](https://leetcode.com/problems/minimum-window-subsequence/)

**Intuition / Approach:** Find the smallest window of `s` where `t` appears as a **subsequence** (order preserved, gaps allowed). Two-pointer two-pass: sweep `right` forward matching `t` in order; when all of `t` is matched, walk a second pointer **backward** from `right` to tighten the start, record the window, then continue. (A DP `dp[i][j]` = start index also works.)

**Example:** `s = "abcdebdde", t = "bde"` → candidate `"bcde"` (indices 1–4) and later `"bdde"`; shortest is `"bcde"` length **4**. Output `"bcde"`.

**Analogy:** Finding the shortest sentence in a paragraph that still spells out your secret word in order (skipping letters is allowed) — you scan forward to complete the word, then trim the front as tight as possible without breaking the order.

*Complexity: O(m·n) time, O(1) or O(m·n) space.*

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---|---|---|---|
| 1 | Longest Substring Without Repeating Characters | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/) |
| 2 | Max Consecutive Ones III | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/max-consecutive-ones-iii/) |
| 3 | Fruit Into Baskets | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/fruit-into-baskets/description/) |
| 4 | Longest Repeating Character Replacement | 🔴 Hard | Medium Problems | [LeetCode](https://leetcode.com/problems/longest-repeating-character-replacement/) |
| 5 | Binary Subarrays With Sum | 🔴 Hard | Medium Problems | [LeetCode](https://leetcode.com/problems/binary-subarrays-with-sum/) |
| 6 | Count number of Nice subarrays | 🔴 Hard | Medium Problems | [LeetCode](https://leetcode.com/problems/count-number-of-nice-subarrays/) |
| 7 | Number of Substrings Containing All Three Characters | 🔴 Hard | Medium Problems | [LeetCode](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/) |
| 8 | Maximum Points You Can Obtain from Cards | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/) |
| 9 | Longest Substring With At Most K Distinct Characters | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) |
| 10 | Subarrays with K Different Integers | 🟡 Medium | Hard Problems | [LeetCode](https://leetcode.com/problems/subarrays-with-k-different-integers/) |
| 11 | Minimum Window Substring | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/minimum-window-substring/) |
| 12 | Minimum Window Subsequence | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/minimum-window-subsequence/) |
