# Strings [Basic and Medium] — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by pattern (the JSON sub-steps), in data order. Every problem from the data appears exactly once, each with intuition, a worked example, and a memorable analogy.

---

## Basic and Easy String Problems

### Remove Outermost Parentheses  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/remove-outermost-parentheses/) · [Article](https://takeuforward.org/data-structure/remove-outermost-parentheses)

**Intuition / Approach:** Keep a running `depth`. When you see `(`, add it to the result only if `depth > 0` (i.e., it is *not* an outermost open), then increment depth. When you see `)`, decrement depth first, then add it only if `depth > 0`. This strips exactly the outer layer of each primitive group.

**Example:** `"(()())(())"` → primitives `(()())` and `(())`. Removing outer of each gives `()()` + `()` = `"()()()"`.

**Analogy:** Peeling the outer shell off each nut in a bag — keep the kernel, discard the shell.

**Complexity:** `O(n)` time, `O(1)` extra (besides output).

### Reverse words in a given string / Palindrome Check  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/) · [Article](https://takeuforward.org/data-structure/reverse-words-in-a-string/)

**Intuition / Approach:** Split on spaces, drop empty tokens (handles multiple/leading/trailing spaces), then join the words in reverse order with single spaces. A palindrome check is the sibling problem: two pointers from both ends comparing characters.

**Example:** `"  the sky  is blue "` → tokens `[the, sky, is, blue]` → reversed → `"blue is sky the"`.

**Analogy:** Reading a sentence written on train cars, then re-coupling the cars in reverse order onto the track.

**Complexity:** `O(n)` time, `O(n)` space.

### Largest Odd Number in a String  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/largest-odd-number-in-string/) · [Article](https://takeuforward.org/data-structure/largest-odd-number-in-a-string)

**Intuition / Approach:** The largest odd sub-number is the longest prefix ending in an odd digit. Scan from the right; at the first odd digit at index `i`, the answer is `s[0..i]`. If no odd digit exists, return `""`.

**Example:** `"35427"` → rightmost odd digit is `7` at the end → answer `"35427"`. `"5482"` → rightmost odd is `5` at index 0 → answer `"5"`.

**Analogy:** Trimming a ruler from the right until the last visible mark is odd — everything left of it stays.

**Complexity:** `O(n)` time, `O(1)` space.

### Longest Common Prefix  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/longest-common-prefix/) · [Article](https://takeuforward.org/data-structure/longest-common-prefix)

**Intuition / Approach:** Compare characters column by column: take the first string as a reference, and for each position check that every other string has the same character. Stop at the first mismatch or when any string ends.

**Example:** `["flower","flow","flight"]` → column 0 `f`, column 1 `l`, column 2 `o` vs `i` mismatch → prefix `"fl"`.

**Analogy:** Several people spelling the same word aloud together — you write down letters only as long as everyone says the same one.

**Complexity:** `O(m·n)` time, `O(1)` extra.

### Isomorphic String  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/isomorphic-strings/) · [Article](https://takeuforward.org/data-structure/isomorphic-string)

**Intuition / Approach:** Characters must map one-to-one and consistently. Maintain two maps: `s→t` and `t→s`. For each pair `(a,b)`, if either mapping exists and disagrees, reject; otherwise record both. The reverse map prevents two source chars mapping to the same target.

**Example:** `"egg"`, `"add"` → `e→a`, `g→d`, `g→d` consistent → true. `"foo"`, `"bar"` → `o→a` then `o→r` conflict → false.

**Analogy:** A substitution cipher where each letter always encodes to exactly one other letter and no two letters share a code.

**Complexity:** `O(n)` time, `O(1)` space.

### Rotate String  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/rotate-string/) · [Article](https://takeuforward.org/data-structure/check-if-one-string-is-rotation-of-another)

**Intuition / Approach:** `b` is a rotation of `a` iff they have equal length and `b` is a substring of `a + a`, because concatenating `a` with itself contains every rotation of `a` as a window.

**Example:** `a="abcde"`, `b="cdeab"` → `a+a = "abcdeabcde"` which contains `"cdeab"` → true.

**Analogy:** A round dial of letters — spin it any number of clicks and the new reading is always somewhere in two full turns of the dial.

**Complexity:** `O(n²)` naive `find` / `O(n)` with KMP, `O(n)` space.

### Check if two strings are anagram of each other  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/valid-anagram/) · [Article](https://takeuforward.org/data-structure/check-if-two-strings-are-anagrams-of-each-other/)

**Intuition / Approach:** Anagrams share the same character multiset. Use `freq[26]`: increment for the first string, decrement for the second. If lengths match and no count goes negative (or all end at zero), they are anagrams.

**Example:** `"anagram"`, `"nagaram"` → counts `a:3,n:1,g:1,r:1,m:1` identical → true.

**Analogy:** Two bags of Scrabble tiles — same tiles, different arrangement means you can spell one from the other.

**Complexity:** `O(n)` time, `O(1)` space.

---

## Medium String Problems

### Sort Characters by Frequency  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/sort-characters-by-frequency/) · [Article](https://takeuforward.org/data-structure/sort-characters-by-frequency)

**Intuition / Approach:** Count each character's frequency, then sort characters by count descending and rebuild the string, repeating each character `count` times. A hash map + sort (or bucket sort by frequency) does it.

**Example:** `"tree"` → counts `t:1,r:1,e:2` → sort → `e` first → `"eert"` (or `"eetr"`).

**Analogy:** Sorting a jar of coins by denomination count — stack the most common coins at the top.

**Complexity:** `O(n + k log k)` time, `O(k)` space.

### Maximum Nesting Depth of the Parentheses  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/) · [Article](https://takeuforward.org/data-structure/maximum-nesting-depth-of-parenthesis)

**Intuition / Approach:** Track a running balance: `+1` on `(`, `-1` on `)`. The answer is the maximum balance ever reached during the scan. Non-bracket characters are ignored.

**Example:** `"(1+(2*3)+((8)/4))+1"` → balances rise to 3 at the innermost `((8)` → answer `3`.

**Analogy:** Descending into nested rooms — the deepest floor you ever stand on is the maximum nesting depth.

**Complexity:** `O(n)` time, `O(1)` space.

### Roman to Integer  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/roman-to-integer/) · [Article](https://takeuforward.org/data-structure/roman-numerals-to-integer)

**Intuition / Approach:** Map each symbol to its value. Scan left to right: if the current symbol's value is less than the next one's, subtract it (subtractive form like IV, IX); otherwise add it.

**Example:** `"MCMXCIV"` → `M(+1000) C(-100) M(+1000) X(-10) C(+100) I(-1) V(+5)` = `1994`.

**Analogy:** Reading tally marks where a smaller mark placed before a bigger one means "one less than" — like `4` written as `IV` (one before five).

**Complexity:** `O(n)` time, `O(1)` space.

### String to Integer (atoi)  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/string-to-integer-atoi/) · [Article](https://takeuforward.org/data-structure/recursive-implementation-of-atoi)

**Intuition / Approach:** Follow the state machine: skip leading spaces → read optional sign → read digits until a non-digit → clamp the result to `[INT_MIN, INT_MAX]`. Accumulate in a wider type and clamp *during* the loop to avoid overflow.

**Example:** `"   -042abc"` → skip spaces → sign `-` → digits `042` → `-42` (stops at `a`).

**Analogy:** A strict ticket scanner: ignore blank leading space, note the +/- direction, read digits until it hits garbage, and refuse anything beyond the machine's numeric limit.

**Complexity:** `O(n)` time, `O(1)` space.

### Count Number of Substrings  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/count-number-of-substrings)

**Intuition / Approach:** Count substrings containing exactly `k` distinct characters as `exactly(k) = atMost(k) - atMost(k-1)`. `atMost(k)` uses a sliding window that shrinks when distinct count exceeds `k`, adding `(right - left + 1)` at each step.

**Example:** `s="pqpqs", k=2` → `atMost(2) - atMost(1)` counts windows with ≤2 distinct minus ≤1 distinct → 7 substrings with exactly 2 distinct.

**Analogy:** Counting recipes that use *exactly* two spices = (recipes with at most two spices) minus (recipes with at most one spice).

**Complexity:** `O(n)` time, `O(1)` space (fixed alphabet).

### Longest Palindromic Substring  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)

**Intuition / Approach:** Expand around every center. Each of the `2n-1` centers (each index for odd-length, each gap for even-length) grows outward while both sides match. Track the longest window found. Length of a window `(l,r)` after failure is `r - l - 1`.

**Example:** `"babad"` → center at index 1 (`a`) expands to `bab` (len 3); center at index 2 also gives `aba`. Answer `"bab"` (or `"aba"`).

**Analogy:** Standing at a mirror's midline and stepping backward on both sides as long as your reflection matches — the longest matching stretch is your palindrome.

**Complexity:** `O(n²)` time, `O(1)` space.

### Sum of Beauty of All Substrings  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/) · [Article](https://takeuforward.org/data-structure/sum-of-beauty-of-all-substring)

**Intuition / Approach:** Beauty of a substring = (highest character frequency) − (lowest non-zero frequency). Fix a start index, extend the end one char at a time while maintaining a `freq[26]`, and for each substring add `max − min` over non-zero counts.

**Example:** `"aabcb"` → substring `"aab"` has freqs `a:2,b:1` → beauty `2-1=1`; summing over all substrings gives `5`.

**Analogy:** Rating each playlist by how lopsided the artist mix is — the gap between the most-played and least-played artist, summed across every playlist you could form.

**Complexity:** `O(n²)` time, `O(1)` space (26 buckets).

### Reverse every word in a string  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/) · [Article](https://takeuforward.org/data-structure/reverse-words-in-a-string/)

**Intuition / Approach:** Same core as "Reverse words in a given string": tokenize on whitespace, discard empties to handle extra spaces, then concatenate the tokens in reverse order separated by single spaces. Can be done in-place by reversing the whole string then reversing each word.

**Example:** `"a good   example"` → tokens `[a, good, example]` → reversed → `"example good a"`.

**Analogy:** Rearranging books left-to-right on a shelf so the last book becomes first, while each book's title stays readable.

**Complexity:** `O(n)` time, `O(n)` space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|------------|---------|---------------|
| 1 | Remove Outermost Parentheses | 🟡 Medium | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/remove-outermost-parentheses/) |
| 2 | Reverse words in a given string / Palindrome Check | 🟡 Medium | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/) |
| 3 | Largest Odd Number in a String | 🟢 Easy | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/largest-odd-number-in-string/) |
| 4 | Longest Common Prefix | 🟢 Easy | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/longest-common-prefix/) |
| 5 | Isomorphic String | 🟢 Easy | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/isomorphic-strings/) |
| 6 | Rotate String | 🟢 Easy | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/rotate-string/) |
| 7 | Check if two strings are anagram of each other | 🟢 Easy | Basic and Easy String Problems | [LeetCode](https://leetcode.com/problems/valid-anagram/) |
| 8 | Sort Characters by Frequency | 🟢 Easy | Medium String Problems | [LeetCode](https://leetcode.com/problems/sort-characters-by-frequency/) |
| 9 | Maximum Nesting Depth of the Parentheses | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/) |
| 10 | Roman to Integer | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/roman-to-integer/) |
| 11 | String to Integer (atoi) | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/string-to-integer-atoi/) |
| 12 | Count Number of Substrings | 🟢 Easy | Medium String Problems | [Article](https://takeuforward.org/data-structure/count-number-of-substrings) |
| 13 | Longest Palindromic Substring | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/longest-palindromic-substring/) |
| 14 | Sum of Beauty of All Substrings | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/) |
| 15 | Reverse every word in a string | 🟡 Medium | Medium String Problems | [LeetCode](https://leetcode.com/problems/reverse-words-in-a-string/) |
