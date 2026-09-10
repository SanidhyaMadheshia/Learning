# Recursion [PatternWise] — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** (in sheet order). Every problem has an intuition, a worked example, and a real-world analogy. Nothing is skipped — 25 problems across 3 patterns.

---

## Get a Strong Hold

### Recursive Implementation of atoi()  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/string-to-integer-atoi/) · [Article](https://takeuforward.org/data-structure/recursive-implementation-of-atoi)
**Intuition / Approach:** Convert a numeric string to an integer by peeling one digit at a time. Handle optional leading whitespace and a sign first, then define `value(s) = value(s_without_last) * 10 + lastDigit`, or process left-to-right accumulating `acc*10 + digit`. Clamp to `INT_MIN / INT_MAX` on overflow and stop at the first non-digit.
**Example:** `"  -042abc"` → skip spaces → sign `-` → digits `0,4,2` → `((0*10+4)*10+2)=42` → apply sign → **-42** (stop at `a`).
**Analogy:** Reading a price tag digit by digit aloud — you build the number as you scan left to right, and stop the moment you hit a non-number character.
**Complexity:** O(len) time, O(len) recursion depth.

### Pow(x, n)  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/powx-n/) · 🎥 [YouTube](https://youtu.be/l0YC3876qxg)
**Intuition / Approach:** Use **binary exponentiation**: `x^n = (x^{n/2})²`, and multiply an extra `x` when `n` is odd. Handle negative `n` by inverting `x` and negating `n` (use `long long` to avoid `INT_MIN` overflow). This turns O(n) multiplications into O(log n).
**Example:** `x=2, n=10` → `pow(2,5)²` → `pow(2,2)²·2` … → `2^10 = 1024`.
**Analogy:** Folding a paper to double its layers — 10 doublings get you to 1024 layers in far fewer moves than adding one sheet at a time.
**Complexity:** O(log n) time, O(log n) stack.

### Count Good Numbers  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/count-good-numbers/) · [Article](https://takeuforward.org/data-structure/count-good-numbers)
**Intuition / Approach:** Even indices (0-based) must hold an even digit (5 choices: 0,2,4,6,8), odd indices a prime digit (4 choices: 2,3,5,7). For length `n` there are `ceil(n/2)` even positions and `floor(n/2)` odd positions, so the answer is `5^ceil(n/2) · 4^floor(n/2)` computed with **fast modular exponentiation** under `1e9+7`.
**Example:** `n=4` → even positions=2, odd=2 → `5² · 4² = 25·16 = 400`.
**Analogy:** Filling a form where every other blank is a menu with 5 options and the rest a menu with 4 options — total combos multiply out, and you compute the powers fast.
**Complexity:** O(log n) time (fast pow), O(log n) stack.

### Sort a stack using recursion  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/sort-a-stack)
**Intuition / Approach:** Pop the top, recursively sort the smaller stack, then **insert the popped value into its sorted position** using a helper that keeps popping while the top is greater and pushes the value when the right spot is found. The call stack replaces any extra container.
**Example:** Stack `[3,1,2]` (top=2) → sort `[3,1]` → `[1,3]` → insert `2` → **`[1,2,3]`**.
**Analogy:** Sorting a stack of plates by lifting the top plate off, tidying the rest, then sliding that plate back into its right spot in the neat pile.
**Complexity:** O(n²) time, O(n) stack.

### Reverse a Stack  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/reverse-a-stack-using-recursion)
**Intuition / Approach:** Remove the top element, recursively reverse the remaining stack, then **insert the removed element at the bottom** using a helper. No auxiliary data structure — only recursion.
**Example:** `[1,2,3]` (top=3) → hold 3, reverse `[1,2]`→`[2,1]` → insert 3 at bottom → **`[3,2,1]`** (top=1).
**Analogy:** Reversing a queue of people by pulling the front person aside, reversing everyone behind them, then sending that person to the very back.
**Complexity:** O(n²) time, O(n) stack.

---

## Subsequences Pattern

### Generate Binary Strings Without Consecutive 1s  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/generate-all-binary-strings)
**Intuition / Approach:** Build the string position by position. You can always append `'0'`; you may append `'1'` only if the previous character was not `'1'`. Recurse until the string reaches length `n`, then record it.
**Example:** `n=2` → `"00","01","10"` (skip `"11"`).
**Analogy:** Placing non-adjacent guards along a wall — you can leave a gap anywhere, but you can never post two guards right next to each other.
**Complexity:** O(Fib(n)) outputs, O(n) depth.

### Generate Parentheses  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/generate-parentheses/) · [Article](https://takeuforward.org/data-structure/generate-parenthesis)
**Intuition / Approach:** Track counts of open and close brackets. Add `'('` while `open < n`; add `')'` only while `close < open` (invariant keeps the string valid). When length hits `2n`, record it.
**Example:** `n=2` → `"(())"`, `"()()"`.
**Analogy:** Nesting boxes — you can open a new box anytime you still have lids, but you can only close a box that is currently open.
**Complexity:** O(4ⁿ / √n) (Catalan) outputs.

### Power Set  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/power-set-print-all-the-possible-subsequences-of-the-string/) · 🎥 [YouTube](https://www.youtube.com/watch?v=b7AYbpM5YrE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=67)
**Intuition / Approach:** Each element is either **picked or not picked**, giving `2ⁿ` subsets. Recurse with pick/not-pick, or iterate masks `0..2ⁿ-1` where bit `i` decides inclusion of element `i`.
**Example:** `{a,b}` → `{}, {a}, {b}, {a,b}`.
**Analogy:** Deciding which toppings go on a pizza — each topping is an independent yes/no, and every combination is a valid pizza.
**Complexity:** O(2ⁿ · n) time.

### Learn All Patterns of Subsequences (Theory)  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/learn-all-patterns-of-subsequences-theory) · 🎥 [YouTube](https://www.youtube.com/watch?v=eQCS_v3bw0Q&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=7)
**Intuition / Approach:** A meta-lesson: any subsequence problem reduces to a recursion tree where at each index you **pick or skip**. Three flavors — *print all*, *count how many*, *check if one exists*. Print collects paths at the leaf; count returns `f(pick)+f(skip)`; exists returns `f(pick) OR f(skip)` (short-circuit).
**Example:** For sum-K: `printAll` returns lists; `count` returns an int; `exists` returns a bool — same tree, different aggregation at the return.
**Analogy:** One map, three questions — "show me every route", "how many routes exist", "is there at least one route" — all traverse the same road network.
**Complexity:** O(2ⁿ) tree.

### Count all subsequences with sum K  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/count-all-subsequences-with-sum-k)
**Intuition / Approach:** Pick/not-pick recursion returning an **integer count**. At index `n`, return `1` if the accumulated sum equals `K` else `0`. Total = `count(pick) + count(skip)`.
**Example:** `arr=[1,2,1], K=2` → subsequences `{2}` and `{1,1}` → **count = 2**.
**Analogy:** Counting how many ways to pick coins from your pocket that add up to exactly ₹2 — try every include/exclude combo and tally the successes.
**Complexity:** O(2ⁿ) time, O(n) depth.

### Check if there exists a subsequence with sum K  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/check-if-there-exists-a-subsequence-with-sum-k)
**Intuition / Approach:** Same tree as counting but return a **boolean** with short-circuit: `exists(pick) || exists(skip)`. Stop the instant a `true` bubbles up — no need to explore further.
**Example:** `arr=[1,2,3], K=5` → `{2,3}` → **true**.
**Analogy:** Checking if any combination of your bills can pay an exact bill of ₹5 — the moment you find one, you stop looking.
**Complexity:** O(2ⁿ) worst case, O(n) depth.

### Combination Sum  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/combination-sum/) · 🎥 [YouTube](https://www.youtube.com/watch?v=OyZFFqQtu98&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=49)
**Intuition / Approach:** Distinct candidates, each usable **unlimited** times. On *pick*, stay at the same index (allows reuse); on *not-pick*, move to the next index. Prune when the candidate exceeds the remaining target.
**Example:** `candidates=[2,3,6,7], target=7` → `[2,2,3]`, `[7]`.
**Analogy:** Making exact change with an unlimited supply of each coin denomination — you can reuse the ₹2 coin as many times as needed.
**Complexity:** ~O(2^t) bounded by number of combinations.

### Combination Sum II  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/combination-sum-ii/) · 🎥 [YouTube](https://www.youtube.com/watch?v=G1fRTGRxXU8&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=50)
**Intuition / Approach:** Each element used **at most once**, and the input may contain duplicates. Sort first; iterate from `start`, move to `i+1` on pick, and **skip duplicate siblings** (`if (i>start && a[i]==a[i-1]) continue;`) to avoid repeated combinations.
**Example:** `[10,1,2,7,6,1,5], target=8` → `[1,1,6]`, `[1,2,5]`, `[1,7]`, `[2,6]`.
**Analogy:** Picking items off a shelf where some look identical — you take each physical item once, and you don't record two combos that look the same.
**Complexity:** ~O(2ⁿ) with pruning.

### Subsets I  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/subset-sum-sum-of-all-subsets/) · 🎥 [YouTube](https://www.youtube.com/watch?v=rYkfBRtMJr8&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=52)
**Intuition / Approach:** Generate all `2ⁿ` subsets via pick/not-pick (or by adding the current path at every node in the loop form). The "subset sum" variant just records the sum at each leaf.
**Example:** `[1,2,3]` → `{},{1},{2},{3},{1,2},{1,3},{2,3},{1,2,3}` (8 subsets).
**Analogy:** Choosing which of three switches to flip on — every on/off pattern is one subset, and there are `2³` patterns.
**Complexity:** O(2ⁿ · n).

### Subsets II  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/subsets-ii/) · 🎥 [YouTube](https://www.youtube.com/watch?v=RIn3gOkbhQE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=53)
**Intuition / Approach:** Same as Subsets I but the input has duplicates. Sort, and in the loop form skip equal siblings (`if (i>start && a[i]==a[i-1]) continue;`) so each *unique* subset appears once.
**Example:** `[1,2,2]` → `{},{1},{1,2},{1,2,2},{2},{2,2}` (6 unique subsets).
**Analogy:** Choosing scoops of ice cream where two scoops are the same flavor — "one chocolate" is the same choice no matter which identical scoop you grab.
**Complexity:** O(2ⁿ · n).

### Combination Sum III  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/combination-sum-iii/) · [Article](https://takeuforward.org/data-structure/combination-sum-iii)
**Intuition / Approach:** Use exactly `k` distinct numbers from `1..9` summing to `n`, each used once. Loop from a `start` digit, pick, recurse with `k-1` and `target-digit`, backtrack. Prune when target goes negative or digits run out.
**Example:** `k=3, n=7` → `[1,2,4]`.
**Analogy:** Picking exactly 3 different lottery balls (1–9) whose numbers add up to a jackpot total — a fixed count of distinct choices hitting an exact sum.
**Complexity:** O(C(9,k)) combinations.

### Letter Combinations of a Phone Number  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) · [Article](https://takeuforward.org/data-structure/letter-combinations-of-a-phone-number)
**Intuition / Approach:** Map each digit to its letters (like an old T9 keypad). Recurse over digit positions; for each digit try **every** mapped letter, append it, recurse to the next digit, then backtrack. At the last position record the built string.
**Example:** `"23"` → `ad,ae,af,bd,be,bf,cd,ce,cf`.
**Analogy:** Typing a word on a numeric keypad — each key offers a few letters, and you spell out every possible word by trying each letter for each key press.
**Complexity:** O(4ⁿ · n) time (≤4 letters per digit).

---

## Trying out all Combos / Hard

### Palindrome partitioning  🔴 Hard
**Links:** [Editorial](https://takeuforward.org/plus/dsa/problems/palindrome-partitioning?tab=editorial) · 🎥 [YouTube](https://youtu.be/_H8V5hJUGd0)
**Intuition / Approach:** Try every cut position. For each prefix that is a **palindrome**, add it to the path and recurse on the remaining suffix; backtrack after. When the whole string is consumed, record the partition.
**Example:** `"aab"` → `[["a","a","b"], ["aa","b"]]`.
**Analogy:** Slicing a ribbon into pieces where each piece reads the same forwards and backwards — you only make a cut where the left chunk is a valid mirror-word.
**Complexity:** O(2ⁿ · n) time.

### Word Search  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/word-search/) · [Article](https://takeuforward.org/data-structure/word-search-leetcode/)
**Intuition / Approach:** DFS from every cell that matches the first letter. Move in 4 directions matching the next letter, mark cells visited to avoid reuse, and backtrack (unmark) on failure. Return `true` when the whole word is matched.
**Example:** grid `[[A,B],[C,D]]`, word `"ABDC"` → A→B→D→C path → **true**.
**Analogy:** Tracing a word in a word-search puzzle with your finger — you can move to adjacent letters, but you can't reuse a letter you already touched in this trace.
**Complexity:** O(m·n·4^L) time.

### N Queen  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/n-queens/) · 🎥 [YouTube](https://www.youtube.com/watch?v=i05Ju7AftcM&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=57)
**Intuition / Approach:** Place one queen per column. For each row in the current column, check safety (no queen in same row / both diagonals via O(1) flag arrays), place, recurse to the next column, then remove and try the next row. Record the board when all columns are filled.
**Example:** `n=4` → 2 solutions (queens at rows `[1,3,0,2]` and `[2,0,3,1]`).
**Analogy:** Seating rival chess queens so none can attack another — you audition each seat in a column, and any seat sharing a row or diagonal with a seated queen is off-limits.
**Complexity:** ~O(N!) time, O(N) space.

### Rat in a Maze  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/rat-in-a-maze/) · 🎥 [YouTube](https://www.youtube.com/watch?v=bLGZhJlt4y0&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=60)
**Intuition / Approach:** From the start cell, try moves in lexical order (D,L,R,U). Move only to in-bounds, open, unvisited cells; mark visited, append the direction, recurse, then backtrack. Record the path string when reaching the destination.
**Example:** 4×4 maze → paths like `"DDRDRR"`, `"DRDDRR"` collected in sorted order.
**Analogy:** A rat exploring a maze — it tries a direction, marks where it's been so it won't loop, and retreats to try another turn when it hits a wall.
**Complexity:** ~O(4^(m·n)) worst case.

### Word Break  🟡 Medium
**Links:** [Editorial](https://takeuforward.org/plus/dsa/problems/word-break?tab=editorial)
**Intuition / Approach:** Recursively check if a prefix is in the dictionary; if so, recurse on the remaining suffix. If any split succeeds, return `true`. Memoize on start index to cut the exponential blowup to polynomial.
**Example:** `s="leetcode", dict=["leet","code"]` → `"leet"`+`"code"` → **true**.
**Analogy:** Reading a sign with no spaces (`"leetcode"`) and testing whether you can slice it into words your dictionary knows — try each cut, and remember dead-ends so you don't re-check them.
**Complexity:** O(n²) with memoization.

### M Coloring Problem  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/m-coloring-problem/) · 🎥 [YouTube](https://www.youtube.com/watch?v=wuVwUK25Rfc&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=59)
**Intuition / Approach:** Color vertices one by one. For each vertex try colors `1..m`; a color is valid only if no adjacent vertex already has it. Assign, recurse to the next vertex, backtrack if the rest can't be colored. Return `true` if all vertices are colored.
**Example:** triangle graph, `m=2` → **false**; `m=3` → **true**.
**Analogy:** Coloring a map so neighboring countries differ — you try a crayon on each country, backing up whenever a neighbor already wears that color.
**Complexity:** O(m^V) worst case.

### Sudoku Solver  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/sudoku-solver/) · 🎥 [YouTube](https://www.youtube.com/watch?v=FWAIf_EVUKE&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=58)
**Intuition / Approach:** Find the next empty cell; try digits `1..9` that don't violate row, column, or 3×3 box constraints; place, recurse, and if the recursion fails, erase and try the next digit. Return `true` when no empty cells remain.
**Example:** A valid puzzle fills the single-candidate cells first, then branches on ambiguous cells until the grid is complete.
**Analogy:** Solving Sudoku in pencil — you pencil in a candidate, keep going, and erase back to the last decision the moment a contradiction appears.
**Complexity:** O(9^(empty)) with pruning.

### Expression Add Operators  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/expression-add-operators/) · [Article](https://takeuforward.org/data-structure/expression-add-operators)
**Intuition / Approach:** Between digits, try inserting `+`, `-`, `*`, or nothing (extend the current number). Track the running value and the last operand to correctly handle `*` precedence (`value - prev + prev*cur`). Guard against numbers with leading zeros. Record expressions that equal the target.
**Example:** `num="123", target=6` → `"1+2+3"`, `"1*2*3"`.
**Analogy:** Slipping math symbols into a string of digits like a puzzle — you try every gap (multiply, add, subtract, or glue digits) and keep the arrangements that hit the target.
**Complexity:** O(4ⁿ) time.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|------------|---------|---------------|
| 1 | Recursive Implementation of atoi() | 🟡 Medium | Get a Strong Hold | [LeetCode](https://leetcode.com/problems/string-to-integer-atoi/) |
| 2 | Pow(x, n) | 🟢 Easy | Get a Strong Hold | [LeetCode](https://leetcode.com/problems/powx-n/) |
| 3 | Count Good Numbers | 🟡 Medium | Get a Strong Hold | [LeetCode](https://leetcode.com/problems/count-good-numbers/) |
| 4 | Sort a stack using recursion | 🟡 Medium | Get a Strong Hold | [Article](https://takeuforward.org/data-structure/sort-a-stack) |
| 5 | Reverse a Stack | 🟡 Medium | Get a Strong Hold | [Article](https://takeuforward.org/data-structure/reverse-a-stack-using-recursion) |
| 6 | Generate Binary Strings Without Consecutive 1s | 🟡 Medium | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/generate-all-binary-strings) |
| 7 | Generate Parentheses | 🟡 Medium | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/generate-parentheses/) |
| 8 | Power Set | 🟡 Medium | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/power-set-print-all-the-possible-subsequences-of-the-string/) |
| 9 | Learn All Patterns of Subsequences (Theory) | 🟢 Easy | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/learn-all-patterns-of-subsequences-theory) |
| 10 | Count all subsequences with sum K | 🟢 Easy | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/count-all-subsequences-with-sum-k) |
| 11 | Check if there exists a subsequence with sum K | 🟢 Easy | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/check-if-there-exists-a-subsequence-with-sum-k) |
| 12 | Combination Sum | 🟡 Medium | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/combination-sum/) |
| 13 | Combination Sum II | 🟡 Medium | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/combination-sum-ii/) |
| 14 | Subsets I | 🟡 Medium | Subsequences Pattern | [Article](https://takeuforward.org/data-structure/subset-sum-sum-of-all-subsets/) |
| 15 | Subsets II | 🟡 Medium | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/subsets-ii/) |
| 16 | Combination Sum III | 🟡 Medium | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/combination-sum-iii/) |
| 17 | Letter Combinations of a Phone Number | 🔴 Hard | Subsequences Pattern | [LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) |
| 18 | Palindrome partitioning | 🔴 Hard | Trying out all Combos / Hard | [Editorial](https://takeuforward.org/plus/dsa/problems/palindrome-partitioning?tab=editorial) |
| 19 | Word Search | 🔴 Hard | Trying out all Combos / Hard | [LeetCode](https://leetcode.com/problems/word-search/) |
| 20 | N Queen | 🔴 Hard | Trying out all Combos / Hard | [LeetCode](https://leetcode.com/problems/n-queens/) |
| 21 | Rat in a Maze | 🔴 Hard | Trying out all Combos / Hard | [Article](https://takeuforward.org/data-structure/rat-in-a-maze/) |
| 22 | Word Break | 🟡 Medium | Trying out all Combos / Hard | [Editorial](https://takeuforward.org/plus/dsa/problems/word-break?tab=editorial) |
| 23 | M Coloring Problem | 🔴 Hard | Trying out all Combos / Hard | [Article](https://takeuforward.org/data-structure/m-coloring-problem/) |
| 24 | Sudoku Solver | 🔴 Hard | Trying out all Combos / Hard | [LeetCode](https://leetcode.com/problems/sudoku-solver/) |
| 25 | Expression Add Operators | 🔴 Hard | Trying out all Combos / Hard | [LeetCode](https://leetcode.com/problems/expression-add-operators/) |
