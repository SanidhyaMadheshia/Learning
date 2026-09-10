# Tries — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** (data sub-step). Every problem from the dataset appears exactly once, each with an intuition, a worked example, and a real-world analogy.

---

## Theory

### Trie Implementation and Operations  🔴 Hard

**Links:** [LeetCode](https://leetcode.com/problems/implement-trie-prefix-tree/) · [Article](https://takeuforward.org/data-structure/implement-trie-1/) · 🎥 [YouTube](https://www.youtube.com/watch?v=dBGUmUQhjaM&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp)

**Intuition / Approach:** Build a `Node` with `links[26]` and a boolean `flag`. `insert` walks the word creating nodes on the fly and sets `flag` on the last node. `search` walks the word and returns the last node's `flag`. `startsWith` walks the prefix and returns `true` if the whole path exists (ignoring `flag`). Every operation is `O(word length)`.

**Example:** Insert `"apple"`, then `search("app")` → `false` (path exists but no `flag`), `startsWith("app")` → `true`, `search("apple")` → `true`. Insert `"app"`, now `search("app")` → `true`.

**Analogy:** Like a **library card catalog organized by spelling** — to check whether a title exists you follow its letters drawer-by-drawer; a "starts with" query just needs the drawer path to exist, not a final book.

**Complexity:** `O(L)` per op, `O(ΣL·26)` space.

---

## Problems

### Trie Implementation and Advanced Operations  🔴 Hard

**Links:** [Article](https://takeuforward.org/data-structure/implement-trie-ii/)

**Intuition / Approach:** Extend the basic trie with two counters per node — `countEnd` (words ending here) and `countPrefix` (words passing through). `insert` bumps `countPrefix` along the path and `countEnd` at the end. `countWordsEqualTo(w)` returns the end-node's `countEnd`; `countWordsStartingWith(p)` returns the prefix-node's `countPrefix`; `erase(w)` mirrors insert by decrementing the same counters.

**Example:** Insert `"apple"` twice and `"apps"` once. `countWordsEqualTo("apple")` → 2, `countWordsStartingWith("app")` → 3, then `erase("apple")` → `countWordsStartingWith("app")` → 2.

**Analogy:** Like a **turnstile with two tallies** at each corridor junction — one counting how many people *pass through* and one counting how many people *stop here as their final destination*.

**Complexity:** `O(L)` per op.

---

### Longest Word with All Prefixes  🟡 Medium

**Links:** [Article](https://takeuforward.org/data-structure/implement-trie-ii/) · 🎥 [YouTube](https://www.youtube.com/watch?v=AWnBa91lThI&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=3)

**Intuition / Approach:** Insert all words into a trie. For each word, walk it character by character; it qualifies only if **every** intermediate node has `isEnd = true` (i.e. every prefix is itself a complete word). Track the longest qualifying word, breaking ties by lexicographic order.

**Example:** Words `["a","ap","app","appl","apple","b"]`. `"apple"` qualifies because `a`, `ap`, `app`, `appl`, `apple` are all present → answer `"apple"`. `"b"` alone qualifies too but is shorter.

**Analogy:** Like **climbing a ladder where every rung must exist** — you can only reach the top word if each shorter word beneath it (each prefix) is a solid rung you can stand on.

**Complexity:** `O(ΣL)` time, `O(ΣL·26)` space.

---

### Number of distinct substrings in a string  🟡 Medium

**Links:** [Article](https://takeuforward.org/data-structure/number-of-distinct-substrings-in-a-string-using-trie/) · 🎥 [YouTube](https://www.youtube.com/watch?v=RV0QeTyHZxo&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=4)

**Intuition / Approach:** Every substring is a prefix of some suffix. Insert all `n` suffixes of `s` into a trie; each **new node created** during insertion is a distinct substring. Count nodes created (add 1 if you also count the empty substring).

**Example:** `s = "ab"`. Suffixes: `"ab"`, `"b"`. Inserting `"ab"` creates nodes `a`, `ab`. Inserting `"b"` creates node `b`. Total new nodes = 3 → distinct substrings `{"a","ab","b"}` = 3.

**Analogy:** Like **cataloguing every unique street name by driving from every possible starting corner** — a road already mapped costs nothing, only brand-new stretches get a new signpost, and the signpost count is your answer.

**Complexity:** `O(n²)` time and space (suffix automaton gets `O(n)`).

---

### Bit PreRequisites for TRIE Problems  🟢 Easy

**Links:** 🎥 [YouTube](https://youtu.be/5iyuU4hQFrw)

**Intuition / Approach:** A warm-up on the bit operations needed for XOR tries. Learn to extract the i-th bit `(num >> i) & 1`, set a bit `res |= (1 << i)`, understand `^` (XOR gives 1 when bits differ), and represent a number as a fixed-width MSB→LSB bit string. This is the vocabulary every bit-trie problem uses.

**Example:** `num = 5` (`0101`). Bit 0 = `(5>>0)&1 = 1`, bit 2 = `(5>>2)&1 = 1`, bit 1 = 0. `5 ^ 3` = `0101 ^ 0011` = `0110` = 6.

**Analogy:** Like **learning the alphabet before reading** — you can't spell out numbers into a binary trie until you can reliably read and write each individual bit.

**Complexity:** `O(1)` per bit operation.

---

### Maximum XOR of two numbers in an array  🔴 Hard

**Links:** [LeetCode](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) · [Article](https://takeuforward.org/data-structure/maximum-xor-of-two-numbers-in-an-array/) · 🎥 [YouTube](https://www.youtube.com/watch?v=EIhAwfHubE8&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=6)

**Intuition / Approach:** Insert every number's fixed-width binary (MSB→LSB) into a bit-trie. For each number, walk the trie greedily always preferring the **opposite bit** (`1 - current bit`); if that child exists this bit contributes `2^i` to the XOR, else follow the same bit. The maximum over all numbers is the answer. Higher bits dominate, so greedy is optimal.

**Example:** `arr = [3,10,5,25,2,8]`. Binary of 5 = `00101`, 25 = `11001`. Walking 5 against the trie prefers bits opposite to 5's → matches 25 → `5 ^ 25 = 28`, which is the maximum.

**Analogy:** Like **two spies choosing disguises to look as different as possible** — starting with the most noticeable feature (the tallest bit), each picks the opposite trait when available, maximizing how distinct (XOR) they appear.

**Complexity:** `O(n·B)` time, `O(n·B)` space (`B≈31`).

---

### Maximum Xor with an element from an array  🔴 Hard

**Links:** [LeetCode](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/) · [Article](https://takeuforward.org/trie/maximum-xor-queries-trie/) · 🎥 [YouTube](https://www.youtube.com/watch?v=Q8LhG9Pi5KM&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=7)

**Intuition / Approach:** Each query `(x, m)` asks for the max `x ^ y` where `y ≤ m`. Solve **offline**: sort the array ascending and sort queries by `m` ascending. Sweep queries; before answering each, insert all array elements `≤ m` into the bit-trie, then run the standard greedy max-XOR of `x`. If no element `≤ m` exists, answer `-1`. Restore answers to original query order.

**Example:** `nums = [0,1,2,3,4]`, query `(x=3, m=1)`. Only `{0,1}` are `≤ 1`. Max of `3^0=3`, `3^1=2` → answer `3`. Query `(x=5, m=-1)` → no valid `y` → `-1`.

**Analogy:** Like a **shopping trip with a rising budget** — you sort your errands by budget, and only stock the shelf (trie) with items you can now afford before picking the one that best "contrasts" with your target.

**Complexity:** `O((n + q)·B + q log q)` time, `O(n·B)` space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|------------|---------|---------------|
| 1 | Trie Implementation and Operations | 🔴 Hard | Theory | [LeetCode](https://leetcode.com/problems/implement-trie-prefix-tree/) |
| 2 | Trie Implementation and Advanced Operations | 🔴 Hard | Problems | [Article](https://takeuforward.org/data-structure/implement-trie-ii/) |
| 3 | Longest Word with All Prefixes | 🟡 Medium | Problems | [YouTube](https://www.youtube.com/watch?v=AWnBa91lThI&list=PLgUwDviBIf0pcIDCZnxhv0LkHf5KzG9zp&index=3) |
| 4 | Number of distinct substrings in a string | 🟡 Medium | Problems | [Article](https://takeuforward.org/data-structure/number-of-distinct-substrings-in-a-string-using-trie/) |
| 5 | Bit PreRequisites for TRIE Problems | 🟢 Easy | Problems | [YouTube](https://youtu.be/5iyuU4hQFrw) |
| 6 | Maximum XOR of two numbers in an array | 🔴 Hard | Problems | [LeetCode](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) |
| 7 | Maximum Xor with an element from an array | 🔴 Hard | Problems | [LeetCode](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/) |
