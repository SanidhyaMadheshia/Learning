# Strings [Advanced] — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by the sub-step ("Hard Problems") from the data. Every problem below appears **exactly once**, each with intuition, a worked example, and a memory-hook analogy. Links use the exact URLs from the data file — nothing fabricated.

---

## Hard Problems

### Minimum number of bracket reversals to make an expression balanced  🔴

**Links:** [LeetCode](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/) · [Article](https://takeuforward.org/data-structure/minimum-number-of-bracket-reversals-needed-to-make-an-expression-balanced)

**Intuition / Approach:** If the length is odd, balancing is impossible. Otherwise scan and cancel each `}` against a pending `{`. What remains are `open` unmatched `{` and `close` unmatched `}`. Each group needs `ceil(count/2)` reversals, so the answer is `ceil(open/2) + ceil(close/2)`. (The linked LeetCode 921 asks for minimum *additions* = `open + close`.)

**Example:** `s = "}{{}}{{{"` → after cancelling, `open = 3`, `close = 1` → `ceil(1/2) + ceil(3/2) = 1 + 2 = 3` reversals.

**Analogy:** Like straightening a row of magnets pointing the wrong way — flipping one magnet can fix two mismatches, so you flip in pairs, rounding up when one is left over.

**Complexity:** `O(n)` time, `O(1)` space.

### Count and say  🔴

**Links:** [LeetCode](https://leetcode.com/problems/count-and-say/) · [Article](https://takeuforward.org/data-structure/count-and-say)

**Intuition / Approach:** Build the sequence iteratively starting from `"1"`. To get the next term, "read aloud" the current term: count consecutive equal digits and emit `count` followed by that `digit`. Repeat `n−1` times.

**Example:** `n = 4`: `1 → "one 1" → 11 → "two 1s" → 21 → "one 2, one 1" → 1211`. Output `"1211"`.

**Analogy:** Like describing a bead necklace out loud — "two red, one blue, three red" — where your spoken description literally becomes the next necklace.

**Complexity:** `O(L)` time and space where `L` is the generated length (grows by Conway's constant ≈ 1.303 each step).

### Hashing In Strings | Theory  🟢

**Links:** [Article](https://takeuforward.org/data-structure/hashing-in-strings)

**Intuition / Approach:** Represent a string as a base-`b` polynomial value modulo a large prime so that comparing two strings becomes comparing two integers in `O(1)`. Precompute prefix hashes and powers so any substring hash is retrievable in constant time. This underpins Rabin–Karp, substring equality, and deduplication.

**Example:** For `s = "abc"` with base 31: `h = a·31² + b·31 + c` (using `a=1,b=2,c=3`) `= 1·961 + 2·31 + 3 = 1026`. Any substring's hash is then a windowed subexpression of this.

**Analogy:** Like giving every book a barcode — instead of comparing whole titles letter by letter, you scan the code and compare numbers instantly (with a spine check only when codes collide).

**Complexity:** Precompute `O(n)`; each substring hash query `O(1)`.

### Rabin Karp Algorithm  🔴

**Links:** [LeetCode/Discuss](https://leetcode.com/problems/repeated-string-match/discuss/416144/Rabin-Karp-algorithm-C%2B%2B-implementation)

**Intuition / Approach:** Hash the pattern, then slide a window of the pattern's length across the text, updating the window hash in `O(1)` (drop leading char, shift, add new char). On a hash match, verify character-by-character to eliminate collisions. Expected linear time.

**Example:** text `"abcabc"`, pat `"cab"` (m=3). Window hashes for indices 0,1,2… ; the window at index 2 (`"cab"`) equals `hash(pat)` → verify → match at index 2.

**Analogy:** A moving conveyor scanner reading a fixed-width barcode: as one box leaves the frame and a new one enters, you don't recount — you subtract the old and add the new to update the total instantly.

**Complexity:** `O(n+m)` expected, `O(n·m)` worst; `O(1)` extra space.

### Z function  🔴

**Links:** [Article](https://takeuforward.org/data-structure/hashing-in-strings) *(topic reference — no direct link in data)*

**Intuition / Approach:** `Z[i]` is the length of the longest substring starting at `i` that matches a prefix of the string. Maintain a `[l, r]` window of the rightmost prefix-match to reuse prior computation, then extend by naive comparison. For pattern search, build Z over `pat + '#' + txt` and every `Z[i] == m` is a match.

**Example:** `s = "aabxaab"` → `Z = [-, 1, 0, 0, 3, 1, 0]`. `Z[4]=3` means `"aab"` (from index 4) matches the prefix `"aab"`.

**Analogy:** Like a photocopier that remembers how far it already matched the master page — when it moves to a new spot inside a region it already scanned, it reuses that measurement instead of re-scanning from scratch.

**Complexity:** `O(n)` time, `O(n)` space.

### KMP Algorithm or LPS array  🔴

**Links:** [LeetCode](https://leetcode.com/problems/implement-strstr/) · [Article](https://takeuforward.org/data-structure/kmp-algorithm-or-lps-array)

**Intuition / Approach:** Precompute the LPS (longest proper prefix that is also a suffix) array of the pattern. During search, on a mismatch, instead of restarting, jump the pattern pointer to `lps[j-1]`, reusing already-matched characters. Achieves `O(n+m)`.

**Example:** pat `"aba"`, LPS `[0,0,1]`. Searching `"ababa"`: match `aba` at index 0; on continuing, the `1` in LPS lets the next match reuse the leading `a`, finding `aba` again at index 2 without rescanning.

**Analogy:** Like a detective who, when a lead goes cold, doesn't restart the whole case — they resume from the last clue that still holds, because part of the trail already checks out.

**Complexity:** `O(n+m)` time, `O(m)` space.

### Shortest Palindrome  🔴

**Links:** [Article](https://takeuforward.org/data-structure/kmp-algorithm-or-lps-array) *(KMP-based; no direct link in data)*

**Intuition / Approach:** We may only prepend characters, so we need the *longest palindromic prefix* of `s`; the rest gets mirrored to the front. Build `t = s + '#' + reverse(s)` and compute its LPS. `lps[t.size()-1] = k` is that longest palindromic-prefix length; answer is `reverse(s[k:]) + s`.

**Example:** `s = "aacecaaa"` → longest palindromic prefix is `"aacecaa"` (`k=7`), remaining suffix is `"a"` → prepend its reverse → `"aaacecaaa"`.

**Analogy:** Like completing a half-drawn symmetrical butterfly — you keep the largest already-mirror-symmetric part and only draw the missing wing tip on the front.

**Complexity:** `O(n)` time, `O(n)` space.

### Longest happy prefix  🔴

**Links:** [LeetCode](https://leetcode.com/problems/longest-happy-prefix/) · [Article](https://takeuforward.org/data-structure/longest-happy-prefix)

**Intuition / Approach:** A "happy prefix" is a non-empty proper prefix that is also a suffix — exactly the definition of the last LPS value. Compute the prefix function of `s`; the answer is `s.substr(0, lps[n-1])`.

**Example:** `s = "level"` → LPS `[0,0,0,0,1]` → `lps[4]=1` → happy prefix `"l"`. For `"ababab"` → `lps` ends at `4` → `"abab"`.

**Analogy:** Like finding the largest chunk of a train that is identical at both the front and the back — the matching engine-and-caboose segment is your happy prefix.

**Complexity:** `O(n)` time, `O(n)` space.

### Count Palindromic Subsequences  🟡

**Links:** [LeetCode](https://leetcode.com/problems/count-palindromic-subsequences/)

**Intuition / Approach:** Use interval DP where `dp[i][j]` counts palindromic subsequences within `s[i..j]`. Combine `dp[i+1][j] + dp[i][j-1]`, subtract the double-counted `dp[i+1][j-1]`, and if `s[i]==s[j]` add back the inner count plus one for the new pair (with careful handling of duplicate boundary characters in the distinct-count variant), all modulo `1e9+7`.

**Example:** `s = "aba"` → single chars `a,b,a` (3) + `"aa"` (subsequence of the two a's) + `"aba"` = **5** palindromic subsequences (counting positions).

**Analogy:** Like counting symmetric bead patterns you can pick from a bracelet by choosing beads left-to-right — every time the two ends match, you unlock a whole new family of symmetric picks nested inside.

**Complexity:** `O(n²)` time, `O(n²)` space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Minimum number of bracket reversals to make an expression balanced | 🔴 Hard | Bracket balance / stack | [LeetCode](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/) |
| 2 | Count and say | 🔴 Hard | Run-length simulation | [LeetCode](https://leetcode.com/problems/count-and-say/) |
| 3 | Hashing In Strings \| Theory | 🟢 Easy | String hashing | [Article](https://takeuforward.org/data-structure/hashing-in-strings) |
| 4 | Rabin Karp Algorithm | 🔴 Hard | Rolling hash | [Discuss](https://leetcode.com/problems/repeated-string-match/discuss/416144/Rabin-Karp-algorithm-C%2B%2B-implementation) |
| 5 | Z function | 🔴 Hard | Z-function | [Article](https://takeuforward.org/data-structure/hashing-in-strings) |
| 6 | KMP Algorithm or LPS array | 🔴 Hard | KMP / LPS | [LeetCode](https://leetcode.com/problems/implement-strstr/) |
| 7 | Shortest Palindrome | 🔴 Hard | Prefix-fn application | [Article](https://takeuforward.org/data-structure/kmp-algorithm-or-lps-array) |
| 8 | Longest happy prefix | 🔴 Hard | Prefix-fn application | [LeetCode](https://leetcode.com/problems/longest-happy-prefix/) |
| 9 | Count Palindromic Subsequences | 🟡 Medium | Interval DP | [LeetCode](https://leetcode.com/problems/count-palindromic-subsequences/) |
