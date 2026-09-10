# Learn the Basics — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** (sub-step). Every problem from the data appears exactly once, each with an intuition, a worked example, and a real-world analogy. Links use the exact URLs from the dataset — LeetCode where available, else the takeUforward Article.

---

## Things to Know in C++/Java/Python or any language

### Input Output  🟢
**Links:** [Article](https://takeuforward.org/c/c-basic-input-output/) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=250)
**Intuition / Approach:** Read data with `cin`/`scanf` and write with `cout`/`printf`. For competitive I/O, add `ios::sync_with_stdio(false); cin.tie(nullptr);` to speed up streams.
**Example:** Input `3 5` → read two ints `a=3,b=5` → print `a+b` → output `8`.
**Analogy:** Like a mailroom — `cin` is the inbox where letters arrive, `cout` is the outbox where you send replies.

### Cpp Basics  🟢
**Links:** [Article](https://takeuforward.org/data-structure/what-are-arrays-strings) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=2415)
**Intuition / Approach:** Learn data types (`int`, `long long`, `double`, `char`, `bool`), operators, and basic syntax so you can express any logic. Choose types by range to avoid overflow.
**Example:** `long long big = 1e18;` stores a value an `int` (max ~2.1e9) can't hold.
**Analogy:** Like choosing the right size box before packing — a tiny box (`int`) overflows if the item (value) is too big.

### If ElseIf  🟢
**Links:** [Article](https://takeuforward.org/if-else/if-else-statements/) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=1259)
**Intuition / Approach:** Branch execution based on boolean conditions, checked top to bottom; the first true branch wins, `else` catches the rest.
**Example:** For `marks=75`: `if(m>=90)"A" else if(m>=60)"B" else "C"` → prints `B`.
**Analogy:** A road with forks — at each fork a sign (condition) decides which way you turn; you take the first matching path.

### Switch Case  🟢
**Links:** [Article](https://takeuforward.org/switch-case/switch-case-statements/) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4)
**Intuition / Approach:** Cleaner multi-way branch on a single discrete value; each `case` needs `break` or it "falls through" to the next. Use `default` for unmatched values.
**Example:** `day=3` → `switch(day){case 3: cout<<"Wed"; break;}` → output `Wed`.
**Analogy:** A vending machine — you press a button (value), it dispenses exactly one matching item (case); forgetting `break` is like the machine dumping every item below it too.

### What are arrays, strings?  🟢
**Links:** [Article](https://takeuforward.org/data-structure/what-are-arrays-strings) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=2415)
**Intuition / Approach:** An array stores fixed-type elements in contiguous memory with O(1) index access; a string is essentially an array of characters. Indexing is 0-based.
**Example:** `int a[3]={10,20,30}; a[1]` → `20`. `string s="hi"; s[0]` → `'h'`.
**Analogy:** A row of numbered lockers — knowing the locker number (index) lets you open exactly one instantly, no searching.

### For loops  🟢
**Links:** [Article](https://takeuforward.org/for-loop/understanding-for-loop/) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=3096)
**Intuition / Approach:** Repeat a block a known number of times using init/condition/update. Ideal when you know the count up front.
**Example:** `for(int i=0;i<3;i++) cout<<i;` → prints `012`.
**Analogy:** Doing 20 push-ups — you count reps (`i`), stop at the target, add one each rep.

### While loops  🟢
**Links:** [Article](https://takeuforward.org/while-loop/while-loops-in-programming/) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=3459)
**Intuition / Approach:** Repeat *while* a condition holds — best when the number of iterations is unknown ahead of time (e.g., "until `n` becomes 0").
**Example:** `int n=13; while(n){ n/=10; }` runs twice (13→1→0).
**Analogy:** Stirring soup "until it boils" — you don't know how many stirs; you stop when the condition (boiling) is met.

### Functions (Pass by Reference and Value)  🟢
**Links:** [Article](https://takeuforward.org/data-structure/functions-pass-by-reference-and-value) · [🎥 YouTube](https://youtu.be/EAR7De6Goz4?t=3677)
**Intuition / Approach:** Pass-by-value copies the argument (changes stay local); pass-by-reference (`&`) shares the original (changes persist, no copy cost).
**Example:** `void inc(int&x){x++;}` called on `a=5` makes `a=6`; `void inc(int x)` leaves `a=5`.
**Analogy:** Value = handing someone a *photocopy* of your document (their scribbles don't touch yours); reference = handing them the *original*.

### Theory with examples  🟢
**Links:** [Article](https://takeuforward.org/time-complexity/time-and-space-complexity-strivers-a2z-dsa-course/) · [🎥 YouTube](https://youtu.be/FPu9Uld7W-E)
**Intuition / Approach:** Time/space complexity measures how work/memory grows with input size, in Big-O (drop constants & lower-order terms). Compare algorithms by growth, not raw seconds. Rule: ~10⁸ ops ≈ 1s.
**Example:** A single loop over `n` = O(n); two nested loops = O(n²). For `n=10⁵`, O(n²)=10¹⁰ is too slow.
**Analogy:** Comparing cars by *how mileage scales with distance*, not by their color — Big-O is the scaling curve, ignoring paint (constants).

---

## Build-up Logical Thinking

### Easy and Medium  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Warm-up pattern set: translate a drawn shape into loops. Outer loop = rows, inner loop(s) = columns; find the formula linking row index to what/how-many to print.
**Example:** Right triangle of height 3 → rows print `*`, `**`, `***`.
**Analogy:** Bricklaying — you lay each course (row) left to right, and each higher course may have a different brick count.

### Hard  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Harder shapes (hollow/symmetric) split each row into spaces + border + spaces, or combine an upper half with a mirrored lower half. Decompose the shape into independent regions.
**Example:** Hollow square of side 4 → first/last row all `*`; middle rows print `*`, spaces, `*`.
**Analogy:** Building a picture frame — only the border gets material; the middle stays empty (spaces).

---

## Patterns

> All 22 are the same skeleton — outer loop for rows, inner loop(s) for content. For each, derive `spaces(i)` and `stars/number(i)` on paper first. Links are identical across the set (the takeUforward patterns article + the pattern playlist video).

### Pattern 1  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Solid square of stars — `n` rows, each with `n` stars. Two simple nested loops.
**Example:** n=3 → three rows of `***`.
**Analogy:** A chessboard filled completely — every cell in the grid gets a piece.

### Pattern 2  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Right-angled triangle — row `i` prints `i+1` stars.
**Example:** n=3 → `*`, `**`, `***`.
**Analogy:** A staircase seen from the side — each step is one unit longer than the last.

### Pattern 3  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Number triangle — row `i` prints numbers `1..i+1`.
**Example:** n=3 → `1`, `12`, `123`.
**Analogy:** Counting steps as you climb — each higher step you recount from 1 up to the current level.

### Pattern 4  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Repeated-number triangle — row `i` prints the value `i+1` repeated `i+1` times.
**Example:** n=3 → `1`, `22`, `333`.
**Analogy:** Labeling floors of a building — each floor's number is stamped once per room on that floor.

### Pattern 5  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Inverted star triangle — row `i` prints `n-i` stars, shrinking each row.
**Example:** n=3 → `***`, `**`, `*`.
**Analogy:** An ice-cream cone melting from the top — each row is a bit narrower going down.

### Pattern 6  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Inverted number triangle — row `i` prints `1..n-i`.
**Example:** n=3 → `123`, `12`, `1`.
**Analogy:** A countdown board losing one digit each round.

### Pattern 7  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Star pyramid — row `i` prints `n-i-1` spaces then `2*i+1` stars, centering the triangle.
**Example:** n=3 → `  *`, ` ***`, `*****`.
**Analogy:** A Christmas tree — centered and widening symmetrically as you go down.

### Pattern 8  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Inverted pyramid — row `i` prints `i` spaces then `2*(n-i)-1` stars.
**Example:** n=3 → `*****`, ` ***`, `  *`.
**Analogy:** A funnel — wide at the top, narrowing to a point at the bottom.

### Pattern 9  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Diamond = pyramid (Pattern 7) stacked on top of an inverted pyramid (Pattern 8).
**Example:** n=3 → `  *`, ` ***`, `*****`, ` ***`, `  *`.
**Analogy:** A diamond gemstone — symmetric top and bottom halves meeting at the widest middle.

### Pattern 10  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Increasing-then-decreasing triangle (half diamond of stars) — first `n` rows grow `1..n` stars, next `n-1` rows shrink.
**Example:** n=3 → `*`, `**`, `***`, `**`, `*`.
**Analogy:** A hill profile — climb up to the peak, then walk back down.

### Pattern 11  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Binary triangle — start each row with `1` if the row index is even else `0`, then alternate `0/1`.
**Example:** rows → `1`, `01`, `101`.
**Analogy:** A checkerboard row pattern — colors (0/1) alternate as you move along and reset per row.

### Pattern 12  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Number crown — print `1..i` numbers, a block of spaces in the middle, then `i..1`.
**Example:** n=2 → `1    1`, `1221`.
**Analogy:** A mirror over a lake — the left half's reflection appears on the right with a gap of water between.

### Pattern 13  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Continuous number triangle — keep a running counter that increments across all rows.
**Example:** → `1`, `2 3`, `4 5 6`.
**Analogy:** Numbering seats in a stadium section — you keep counting up as you fill each new row.

### Pattern 14  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Character triangle — row `i` prints letters `A` up to the `i`-th letter using `char`+offset.
**Example:** → `A`, `AB`, `ABC`.
**Analogy:** Reciting the alphabet a little further each round.

### Pattern 15  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Inverted character triangle — row `i` prints `A..(n-i)`-th letter, shrinking.
**Example:** n=3 → `ABC`, `AB`, `A`.
**Analogy:** Forgetting the alphabet from the end backward each day.

### Pattern 16  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Repeated-character triangle — row `i` prints the single letter `('A'+i)` repeated `i+1` times.
**Example:** → `A`, `BB`, `CCC`.
**Analogy:** Stamping a rubber stamp more times as its label advances through the alphabet.

### Pattern 17  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Alpha hill — a centered pyramid where letters rise `A..` to the middle then fall back.
**Example:** row 3 → `A B C B A` (centered).
**Analogy:** A mountain path labeled with milestones that count up to the summit and back down.

### Pattern 18  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Reverse-letter triangle — row `i` prints letters descending from `('A'+n-1)` down for `i+1` letters.
**Example:** n=3 → `C`, `CB`, `CBA`.
**Analogy:** Reading a bookshelf's spine labels from Z-side toward A, one more each row.

### Pattern 19  🟢
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Symmetric butterfly (top half) — stars on both sides with a shrinking-then-growing space gap in the middle.
**Example:** n=4 top → `********`, `***  ***`, `**    **`, `*      *`.
**Analogy:** Butterfly wings — solid at the edges, hollow toward the body, mirrored left/right.

### Pattern 20  🟡
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Full butterfly — the top half (growing stars, shrinking gap) followed by its mirror as the bottom half. Track `stars` and `spaces = 2*(n-i)` per row.
**Example:** n=3 → `*    *`, `**  **`, `******`, `**  **`, `*    *`.
**Analogy:** A butterfly viewed head-on — top wings and bottom wings mirror across the midline.

### Pattern 21  🟡
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Hollow rectangle/square — print `*` only on the border (first/last row, first/last column); interior is spaces.
**Example:** 4×4 → `****`, `*  *`, `*  *`, `****`.
**Analogy:** A picture frame — only the outer edge is filled; the glass in the middle is empty.

### Pattern 22  🟡
**Links:** [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) · [🎥 YouTube](https://www.youtube.com/watch?v=tNm_NNSB3_w&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=3)
**Intuition / Approach:** Concentric squares of numbers — for cell `(i,j)`, the value is `n` minus the minimum distance to any edge. Uses `min(min(i,j), min(2n-2-i, 2n-2-j))`.
**Example:** n=2 (side 3) → `222`, `212`, `222`.
**Analogy:** Tree rings / topographic contour lines — each ring outward from the center shares the same value.

---

## Learn STL/Java-Collections or similar thing in your language

### STL  🟢
**Links:** [Article](https://takeuforward.org/c/c-stl-tutorial-most-frequent-used-stl-containers/) · [🎥 YouTube](https://www.youtube.com/watch?v=RRVYpIET_RU)
**Intuition / Approach:** Master the C++ Standard Template Library: containers (`vector`, `pair`, `set`, `map`, `unordered_map`, `stack`, `queue`, `priority_queue`) and algorithms (`sort`, `reverse`, `lower_bound`, `accumulate`). Pick by required operation & complexity.
**Example:** `vector<int> v={3,1,2}; sort(v.begin(),v.end());` → `v={1,2,3}` in O(n log n).
**Analogy:** A well-stocked toolbox — instead of forging a wrench yourself, you grab the right tool (container) for the job.

### Java Collections  🟢
**Links:** [Article](https://takeuforward.org/data-structure/java-collections)
**Intuition / Approach:** The Java equivalent of STL: `ArrayList`, `HashMap`, `HashSet`, `TreeMap`, `PriorityQueue`, etc., in the Collections Framework, with the same complexity trade-offs (hash vs tree ordering).
**Example:** `HashMap<Integer,Integer> m=new HashMap<>(); m.put(5,m.getOrDefault(5,0)+1);` counts frequency in avg O(1).
**Analogy:** The same toolbox in a different brand — the tools have different names but do the same jobs as C++ STL.

---

## Know Basic Maths

### Count all Digits of a Number  🟢
**Links:** [Article](https://takeuforward.org/data-structure/count-digits-in-a-number/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug)
**Intuition / Approach:** Repeatedly drop the last digit with `n/=10`, counting each drop until `n` is 0. Handle 0 as one digit; take absolute value for negatives. Alternatively `floor(log10(n))+1`.
**Example:** n=7896 → 7896→789→78→7→0, 4 drops → **4 digits**.
**Analogy:** Peeling layers off an onion one at a time and counting how many layers you removed.
**Complexity:** O(log₁₀ n) time, O(1) space.

### Reverse a number  🟢
**Links:** [LeetCode](https://leetcode.com/problems/reverse-integer/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=930)
**Intuition / Approach:** Build the reversed value: `rev = rev*10 + n%10`, then `n/=10`. Watch for 32-bit overflow — on LeetCode, return 0 if the result exceeds `[-2³¹, 2³¹-1]`.
**Example:** n=123 → rev: 3 → 32 → 321 → output **321**.
**Analogy:** Popping coins off a stack and stacking them onto a new pile — the order flips.
**Complexity:** O(log₁₀ n) time, O(1) space.

### Palindrome Number  🟢
**Links:** [LeetCode](https://leetcode.com/problems/palindrome-number/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=1230)
**Intuition / Approach:** A number is a palindrome if it equals its reverse. Negative numbers are never palindromes (the sign breaks symmetry).
**Example:** n=121 → reverse=121 → equal → **true**. n=123 → reverse=321 → **false**.
**Analogy:** A word that reads the same in a mirror, like "MOM" — flipping it changes nothing.
**Complexity:** O(log₁₀ n) time, O(1) space.

### GCD of Two Numbers  🟢
**Links:** [Article](https://takeuforward.org/data-structure/find-gcd-of-two-numbers/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=2684)
**Intuition / Approach:** Euclid's algorithm: `gcd(a,b) = gcd(b, a mod b)`, stopping when `b=0` (then `a` is the GCD). Far faster than checking every candidate.
**Example:** gcd(48,18) → gcd(18,12) → gcd(12,6) → gcd(6,0) → **6**.
**Analogy:** Tiling a rectangular floor with the largest identical square tiles that fit exactly — Euclid keeps carving the remainder.
**Complexity:** O(log min(a,b)) time, O(1) space (iterative).

### Check if the Number is Armstrong  🟢
**Links:** [LeetCode](https://leetcode.com/problems/armstrong-number/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=1418)
**Intuition / Approach:** For a `k`-digit number, sum each digit raised to the power `k`; it's Armstrong if the sum equals the original number.
**Example:** 153 (k=3) → 1³+5³+3³ = 1+125+27 = 153 → **true**.
**Analogy:** A number that "rebuilds itself" from its own digit-powers, like a self-portrait made from its own pixels.
**Complexity:** O(log₁₀ n) time, O(1) space.

### Print all Divisors  🟢
**Links:** [Article](https://takeuforward.org/data-structure/print-all-divisors-of-a-given-number/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=1580)
**Intuition / Approach:** Loop `i` from 1 to √n; whenever `i` divides `n`, both `i` and `n/i` are divisors (add each once). This gives all divisors in O(√n) instead of O(n).
**Example:** n=36 → i=1→(1,36), 2→(2,18), 3→(3,12), 4→(4,9), 6→(6) → **1 2 3 4 6 9 12 18 36**.
**Analogy:** Finding all ways to arrange 36 chairs into a perfect rectangle — each width pairs with a height.
**Complexity:** O(√n) time, O(#divisors) space.

### Check for Prime Number  🟢
**Links:** [Article](https://takeuforward.org/data-structure/check-if-a-number-is-prime-or-not/) · [🎥 YouTube](https://youtu.be/1xNbjMdbjug?t=2381)
**Intuition / Approach:** `n` is prime if it has exactly two divisors (1 and itself). Test divisibility only up to √n — if no divisor is found there, none exists beyond. `n<2` is not prime.
**Example:** n=29 → check 2..5 (√29≈5.4); none divide → **prime**. n=15 → 3 divides → **not prime**.
**Analogy:** A brick that can't be split into equal smaller rows except 1×itself — indivisible.
**Complexity:** O(√n) time, O(1) space.

---

## Learn Basic Recursion

### Understand recursion by print something N times  🟢
**Links:** [Article](https://takeuforward.org/recursion/introduction-to-recursion-understand-recursion-by-printing-something-n-times/) · [🎥 YouTube](https://www.youtube.com/watch?v=yVdKa8dnKiE&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9)
**Intuition / Approach:** A function calls itself with a progressed counter, printing each call, until a base case stops it. Establishes base case + recursive call + the call stack idea.
**Example:** `f(0,3)`: print → `f(1,3)` print → `f(2,3)` print → `f(3,3)` base → stop (3 prints).
**Analogy:** A person passing a message to the next in line, who passes it on, until the last person (base case) stays silent.
**Complexity:** O(n) time, O(n) stack.

### Print name N times using recursion  🟢
**Links:** [Article](https://takeuforward.org/recursion/print-name-n-times-using-recursion/) · [🎥 YouTube](https://www.youtube.com/watch?v=un6PLygfXrA&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=2)
**Intuition / Approach:** Same skeleton as above but printing a fixed string; carry the current index `i` and stop at `i==n`.
**Example:** name="Raj", n=2 → prints `Raj`, `Raj`.
**Analogy:** Signing your name once per page, then handing the pen to "yourself" for the next page until the stack of pages runs out.
**Complexity:** O(n) time, O(n) stack.

### Print 1 to N using Recursion  🟢
**Links:** [Article](https://takeuforward.org/recursion/print-1-to-n-using-recursion/) · [🎥 YouTube](https://www.youtube.com/watch?v=un6PLygfXrA&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=2)
**Intuition / Approach:** Head recursion — print `i` *before* recursing to `i+1`, so numbers come out ascending.
**Example:** `f(1,3)` prints 1 → `f(2,3)` prints 2 → `f(3,3)` prints 3 → stop → **1 2 3**.
**Analogy:** Climbing stairs and calling out each step number as you step up.
**Complexity:** O(n) time, O(n) stack.

### Print N to 1 using Recursion  🟢
**Links:** [Article](https://takeuforward.org/recursion/print-n-to-1-using-recursion/) · [🎥 YouTube](https://www.youtube.com/watch?v=un6PLygfXrA&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=2)
**Intuition / Approach:** Print `i` then recurse to `i-1` (or use the unwinding phase: recurse first, print after) to get descending order.
**Example:** `f(3)` print 3 → `f(2)` print 2 → `f(1)` print 1 → **3 2 1**.
**Analogy:** A rocket launch countdown — 3, 2, 1, then liftoff (base case).
**Complexity:** O(n) time, O(n) stack.

### Sum of First N Numbers  🟢
**Links:** [Article](https://takeuforward.org/data-structure/sum-of-first-n-natural-numbers/) · [🎥 YouTube](https://www.youtube.com/watch?v=69ZCDFy-OUo&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=3)
**Intuition / Approach:** `sum(n) = n + sum(n-1)`, base `sum(0)=0`. (Closed form `n(n+1)/2` is O(1), but recursion teaches the reduction.)
**Example:** sum(3)=3+sum(2)=3+2+sum(1)=3+2+1+0 = **6**.
**Analogy:** Stacking coins — the total is the top coin plus the total of the pile beneath it.
**Complexity:** O(n) time, O(n) stack (recursive).

### Factorial of a given number  🟢
**Links:** [Article](https://takeuforward.org/data-structure/factorial-of-a-number-iterative-and-recursive) · [🎥 YouTube](https://www.youtube.com/watch?v=69ZCDFy-OUo&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=3)
**Intuition / Approach:** `fact(n) = n * fact(n-1)`, base `fact(0)=fact(1)=1`. Use `long long` — factorials explode fast (20! overflows 64-bit signed near there).
**Example:** fact(4)=4·3·2·1 = **24**.
**Analogy:** Nesting Russian dolls — each doll wraps the product of all smaller dolls inside it.
**Complexity:** O(n) time, O(n) stack.

### Reverse an array  🟢
**Links:** [Article](https://takeuforward.org/data-structure/reverse-a-given-array/) · [🎥 YouTube](https://www.youtube.com/watch?v=twuC1F6gLI8&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=4)
**Intuition / Approach:** Two-pointer recursion: swap `a[l]` and `a[r]`, recurse with `l+1, r-1`, stop when `l>=r`. Works in-place.
**Example:** [1,2,3,4] → swap(0,3)→[4,2,3,1] → swap(1,2)→[4,3,2,1] → stop → **[4,3,2,1]**.
**Analogy:** Two people at opposite ends of a bookshelf swapping books and stepping inward until they meet.
**Complexity:** O(n) time, O(n) stack.

### Check if String is Palindrome or Not  🟢
**Links:** [LeetCode](https://leetcode.com/problems/valid-palindrome/) · [🎥 YouTube](https://www.youtube.com/watch?v=twuC1F6gLI8&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=4)
**Intuition / Approach:** Compare outer characters `s[l]` and `s[r]`; if unequal return false, else recurse inward `l+1, r-1` until `l>=r` (true). (LeetCode variant: ignore non-alphanumerics and case.)
**Example:** "madam" → m=m, a=a, middle → **true**. "abca" → a=a, b≠c → **false**.
**Analogy:** Folding a strip of paper in half — a palindrome's letters line up perfectly along the crease.
**Complexity:** O(n) time, O(n) stack.

### Fibonacci Number  🟢
**Links:** [LeetCode](https://leetcode.com/problems/fibonacci-number/) · [🎥 YouTube](https://www.youtube.com/watch?v=kvRjNm4rVBE&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=5)
**Intuition / Approach:** `fib(n) = fib(n-1) + fib(n-2)`, base `fib(0)=0, fib(1)=1`. Naive recursion is O(2ⁿ) due to overlapping subproblems — memoization or iteration makes it O(n).
**Example:** fib(5) = fib(4)+fib(3) = 3+2 = **5** (sequence 0,1,1,2,3,5).
**Analogy:** A family tree of rabbits where each pair produces the next generation — counts grow by summing the two prior generations.
**Complexity:** O(2ⁿ) naive time / O(n) with memo, O(n) stack.

---

## Learn Basic Hashing

### Basic Hashing  🟢
**Links:** [Article](https://takeuforward.org/hashing/hashing-maps-time-complexity-collisions-division-rule-of-hashing-strivers-a2z-dsa-course/) · [🎥 YouTube](https://www.youtube.com/watch?v=KEs5UyBJ39g)
**Intuition / Approach:** Pre-compute answers (e.g., counts) into a hash structure in one pass, then answer queries in O(1). Understand collisions, the division rule, and load factor. Use a frequency array for small integer keys, `unordered_map` otherwise.
**Example:** Array [2,3,2] with queries "count of 2?" → pre-store {2:2,3:1} → answer 2 instantly.
**Analogy:** A hotel front desk keeping a guest register — instead of walking every floor to find someone, they check the ledger in one glance.
**Complexity:** O(n) build, O(1) query; O(k) space.

### Counting Frequencies of Array Elements  🟢
**Links:** [Article](https://takeuforward.org/data-structure/count-frequency-of-each-element-in-the-array/)
**Intuition / Approach:** Iterate once, incrementing `freq[x]` in a map/array for each element; then print each key with its count. One pass, O(1) per update.
**Example:** [10,5,10,15,10,5] → {10:3, 5:2, 15:1}.
**Analogy:** Tallying votes — each ballot adds a mark next to its candidate's name.
**Complexity:** O(n) time, O(k) space.

### Highest Occurring Element in an Array  🟢
**Links:** [LeetCode](https://leetcode.com/problems/frequency-of-the-most-frequent-element/) · Article: [find highest/lowest frequency element](https://takeuforward.org/arrays/find-the-highest-lowest-frequency-element/)
**Intuition / Approach:** Build the frequency map (as above), then scan it once tracking the key with the maximum count. Two linear passes total.
**Example:** [1,2,2,3,2,1] → freq {1:2,2:3,3:1} → max count is 3 for element **2**.
**Analogy:** Finding the best-selling item in a store — tally every sale, then pick the product with the tallest tally bar.
**Complexity:** O(n) time, O(k) space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
| --- | --- | --- | --- | --- |
| 1 | Input Output | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/c/c-basic-input-output/) |
| 2 | Cpp Basics | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/data-structure/what-are-arrays-strings) |
| 3 | If ElseIf | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/if-else/if-else-statements/) |
| 4 | Switch Case | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/switch-case/switch-case-statements/) |
| 5 | What are arrays, strings? | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/data-structure/what-are-arrays-strings) |
| 6 | For loops | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/for-loop/understanding-for-loop/) |
| 7 | While loops | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/while-loop/while-loops-in-programming/) |
| 8 | Functions (Pass by Reference and Value) | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/data-structure/functions-pass-by-reference-and-value) |
| 9 | Theory with examples | 🟢 Easy | Language Foundations | [Article](https://takeuforward.org/time-complexity/time-and-space-complexity-strivers-a2z-dsa-course/) |
| 10 | Easy and Medium | 🟢 Easy | Build-up Logical Thinking | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 11 | Hard | 🟢 Easy | Build-up Logical Thinking | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 12 | Pattern 1 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 13 | Pattern 2 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 14 | Pattern 3 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 15 | Pattern 4 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 16 | Pattern 5 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 17 | Pattern 6 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 18 | Pattern 7 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 19 | Pattern 8 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 20 | Pattern 9 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 21 | Pattern 10 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 22 | Pattern 11 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 23 | Pattern 12 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 24 | Pattern 13 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 25 | Pattern 14 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 26 | Pattern 15 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 27 | Pattern 16 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 28 | Pattern 17 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 29 | Pattern 18 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 30 | Pattern 19 | 🟢 Easy | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 31 | Pattern 20 | 🟡 Medium | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 32 | Pattern 21 | 🟡 Medium | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 33 | Pattern 22 | 🟡 Medium | Patterns | [Article](https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/) |
| 34 | STL | 🟢 Easy | STL/Collections | [Article](https://takeuforward.org/c/c-stl-tutorial-most-frequent-used-stl-containers/) |
| 35 | Java Collections | 🟢 Easy | STL/Collections | [Article](https://takeuforward.org/data-structure/java-collections) |
| 36 | Count all Digits of a Number | 🟢 Easy | Basic Maths | [Article](https://takeuforward.org/data-structure/count-digits-in-a-number/) |
| 37 | Reverse a number | 🟢 Easy | Basic Maths | [LeetCode](https://leetcode.com/problems/reverse-integer/) |
| 38 | Palindrome Number | 🟢 Easy | Basic Maths | [LeetCode](https://leetcode.com/problems/palindrome-number/) |
| 39 | GCD of Two Numbers | 🟢 Easy | Basic Maths | [Article](https://takeuforward.org/data-structure/find-gcd-of-two-numbers/) |
| 40 | Check if the Number is Armstrong | 🟢 Easy | Basic Maths | [LeetCode](https://leetcode.com/problems/armstrong-number/) |
| 41 | Print all Divisors | 🟢 Easy | Basic Maths | [Article](https://takeuforward.org/data-structure/print-all-divisors-of-a-given-number/) |
| 42 | Check for Prime Number | 🟢 Easy | Basic Maths | [Article](https://takeuforward.org/data-structure/check-if-a-number-is-prime-or-not/) |
| 43 | Understand recursion by print something N times | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/recursion/introduction-to-recursion-understand-recursion-by-printing-something-n-times/) |
| 44 | Print name N times using recursion | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/recursion/print-name-n-times-using-recursion/) |
| 45 | Print 1 to N using Recursion | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/recursion/print-1-to-n-using-recursion/) |
| 46 | Print N to 1 using Recursion | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/recursion/print-n-to-1-using-recursion/) |
| 47 | Sum of First N Numbers | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/data-structure/sum-of-first-n-natural-numbers/) |
| 48 | Factorial of a given number | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/data-structure/factorial-of-a-number-iterative-and-recursive) |
| 49 | Reverse an array | 🟢 Easy | Basic Recursion | [Article](https://takeuforward.org/data-structure/reverse-a-given-array/) |
| 50 | Check if String is Palindrome or Not | 🟢 Easy | Basic Recursion | [LeetCode](https://leetcode.com/problems/valid-palindrome/) |
| 51 | Fibonacci Number | 🟢 Easy | Basic Recursion | [LeetCode](https://leetcode.com/problems/fibonacci-number/) |
| 52 | Basic Hashing | 🟢 Easy | Basic Hashing | [Article](https://takeuforward.org/hashing/hashing-maps-time-complexity-collisions-division-rule-of-hashing-strivers-a2z-dsa-course/) |
| 53 | Counting Frequencies of Array Elements | 🟢 Easy | Basic Hashing | [Article](https://takeuforward.org/data-structure/count-frequency-of-each-element-in-the-array/) |
| 54 | Highest Occurring Element in an Array | 🟢 Easy | Basic Hashing | [LeetCode](https://leetcode.com/problems/frequency-of-the-most-frequent-element/) |

**Totals:** 54 problems across 7 patterns (🟢 Easy: 51 · 🟡 Medium: 3 · 🔴 Hard: 0). Every problem from the dataset appears exactly once above.
