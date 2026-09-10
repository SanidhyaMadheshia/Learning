# Solve Problems on Arrays [Easy → Medium → Hard] — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by pattern (Striver's Easy → Medium → Hard sub-steps). Every problem from the data appears exactly once, with intuition, a worked example, and a memorable analogy. Emoji: 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Pattern Group 1 — Easy: Scanning, Two-Pointer Overwrite & Hashing

### Largest Element  🟢
**Links:** [Article](https://takeuforward.org/data-structure/find-the-largest-element-in-an-array/) · [🎥 YouTube](https://youtu.be/37E9ckMDdTk?t=526)
**Intuition / Approach:** Single linear scan, keep `mx = max(mx, a[i])`. No sorting needed.
**Example:** `[3,1,7,4]` → track 3 → 3 → 7 → 7 ⇒ **7**.
**Analogy:** Walking a line of people and remembering only the tallest seen so far.
_Complexity:_ O(n) / O(1).

### Second Largest Element  🟢
**Links:** [Article](https://takeuforward.org/data-structure/find-second-smallest-and-second-largest-element-in-an-array/) · [🎥 YouTube](https://youtu.be/37E9ckMDdTk?t=810)
**Intuition / Approach:** One pass with two trackers `largest`, `second`. On a new max, push old max down to `second`; else update `second` if strictly between.
**Example:** `[3,1,7,4]` → largest=3 → 3/1 → 7/3 → 7/4 ⇒ **4**.
**Analogy:** Podium at a race — when a faster runner arrives, the previous winner slides to the silver spot.
_Complexity:_ O(n) / O(1).

### Check if the Array is Sorted II  🟢
**Links:** [LeetCode](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/) · [🎥 YouTube](https://youtu.be/37E9ckMDdTk?t=17224)
**Intuition / Approach:** Sorted-and-rotated is true if there is **at most one** "drop" `a[i] > a[(i+1)%n]` across the circular array.
**Example:** `[3,4,5,1,2]` → one drop (5→1) ⇒ **true**. `[2,1,3,4]` → drops 2→1 and none else, but check circular 4→2 gives 2 drops ⇒ **false**.
**Analogy:** A clock face read once around — a valid rotation has a single "midnight" wrap, not many.
_Complexity:_ O(n) / O(1).

### Remove duplicates from Sorted array  🟢
**Links:** [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) · [🎥 YouTube](https://youtu.be/37E9ckMDdTk?t=1887)
**Intuition / Approach:** Slow/fast pointers. `j` marks last unique; when `a[i] != a[j]`, write `a[++j] = a[i]`. Returns new length `j+1`.
**Example:** `[0,0,1,1,2]` → `[0,1,2,...]`, length **3**.
**Analogy:** Compacting a bookshelf of sorted books, keeping one copy of each title and pushing them left.
_Complexity:_ O(n) / O(1).

### Left Rotate Array by One  🟢
**Links:** [LeetCode](https://leetcode.com/problems/rotate-array/) · [🎥 YouTube](https://youtu.be/wvcQg43_V8U?t=61)
**Intuition / Approach:** Save `a[0]`, shift every element left by one, place saved value at the end.
**Example:** `[1,2,3,4]` → `[2,3,4,1]`.
**Analogy:** A queue where the front person walks to the back.
_Complexity:_ O(n) / O(1).

### Left Rotate Array by K Places  🟢
**Links:** [LeetCode](https://leetcode.com/problems/rotate-array/) · [🎥 YouTube](https://youtu.be/wvcQg43_V8U?t=485)
**Intuition / Approach:** `k %= n`; reverse first `k`, reverse rest, reverse whole (reversal algorithm).
**Example:** `[1,2,3,4,5], k=2` → rev[0,1]=`[2,1,3,4,5]` → rev[2,4]=`[2,1,5,4,3]` → rev all=`[3,4,5,1,2]`.
**Analogy:** Flipping two halves of a pancake stack then flipping the whole plate lands them in rotated order.
_Complexity:_ O(n) / O(1).

### Move Zeros to End  🟢
**Links:** [LeetCode](https://leetcode.com/problems/move-zeroes/) · [🎥 YouTube](https://youtu.be/wvcQg43_V8U?t=1633)
**Intuition / Approach:** Write pointer `j` for next non-zero slot; scan, copy non-zeros forward, fill the rest with zeros (or swap).
**Example:** `[0,1,0,3,12]` → `[1,3,12,0,0]`.
**Analogy:** Sweeping crumbs (zeros) to the edge of a table while keeping the plates (non-zeros) in order.
_Complexity:_ O(n) / O(1).

### Linear Search  🟢
**Links:** [Article](https://takeuforward.org/data-structure/linear-search-in-c/) · [🎥 YouTube](https://youtu.be/wvcQg43_V8U?t=2465)
**Intuition / Approach:** Scan left to right; return the first index equal to the target, else -1.
**Example:** `[4,2,7], target=7` → index **2**.
**Analogy:** Checking coat pockets one by one until you find your keys.
_Complexity:_ O(n) / O(1).

### Union of two sorted arrays  🟢
**Links:** [Article](https://takeuforward.org/data-structure/union-of-two-sorted-arrays/) · [🎥 YouTube](https://youtu.be/wvcQg43_V8U?t=2584)
**Intuition / Approach:** Two-pointer merge; push the smaller, skip duplicates (including equal front elements).
**Example:** `[1,2,3]`,`[2,3,4]` → `[1,2,3,4]`.
**Analogy:** Merging two sorted guest lists into one with no name repeated.
_Complexity:_ O(n+m) / O(n+m) output.

### Find missing number  🟢
**Links:** [Article](https://www.geeksforgeeks.org/find-the-missing-number/)
**Intuition / Approach:** Expected sum `n(n+1)/2` minus actual sum = missing; or XOR all indices `0..n` with all values (overflow-safe).
**Example:** `[0,1,3], n=3` → expected 6, actual 4 ⇒ missing **2**.
**Analogy:** A roll call of numbered tickets 0..n — the ticket whose stub is missing is the absent number.
_Complexity:_ O(n) / O(1).

### Maximum Consecutive Ones  🟢
**Links:** [LeetCode](https://leetcode.com/problems/max-consecutive-ones/) · [🎥 YouTube](https://youtu.be/bYWLJb3vCWY?t=1124)
**Intuition / Approach:** Running streak counter; on `1` increment and update best, on `0` reset to 0.
**Example:** `[1,1,0,1,1,1]` → streaks 2 then 3 ⇒ **3**.
**Analogy:** Counting your longest unbroken daily gym streak; a missed day resets the count.
_Complexity:_ O(n) / O(1).

### Find the number that appears once, and other numbers twice.  🟡
**Links:** [LeetCode](https://leetcode.com/problems/single-number/) · [🎥 YouTube](https://youtu.be/bYWLJb3vCWY?t=1369)
**Intuition / Approach:** XOR all elements; pairs cancel (`x^x=0`), leaving the unique value.
**Example:** `[4,1,2,1,2]` → `4^1^2^1^2 = 4`.
**Analogy:** Everyone at a dance has a partner except one — after all pairs leave together, one person remains.
_Complexity:_ O(n) / O(1).

### Longest subarray with given sum K(positives)  🟡
**Links:** [Article](https://takeuforward.org/data-structure/longest-subarray-with-given-sum-k/) · [🎥 YouTube](https://www.youtube.com/watch?v=frf7qxiN2qU&feature=youtu.be)
**Intuition / Approach:** Sliding window (all positives): expand `right`, shrink `left` while `sum > k`; record length when `sum == k`.
**Example:** `[1,2,3,1,1,1,1], k=3` → windows `[1,2]`, `[3]`, `[1,1,1]` ⇒ longest **3**.
**Analogy:** Adjusting the length of an accordion so the air (sum) inside stays exactly at a target pressure.
_Complexity:_ O(n) / O(1).

### Longest subarray with sum K  🟡
**Links:** [Article](https://takeuforward.org/arrays/longest-subarray-with-sum-k-postives-and-negatives) · [🎥 YouTube](https://youtu.be/frf7qxiN2qU)
**Intuition / Approach:** With negatives, use prefix-sum + hashmap of earliest index of each prefix; if `pre - k` was seen at `idx`, length `= i - idx`.
**Example:** `[1,-1,5,-2,3], k=3` → prefixes 1,0,5,3,6; `pre=3` at i=3 with `pre-k=0` first at i=1 ⇒ length **... best is 4** (`[1,-1,5,-2]`).
**Analogy:** Bank balance timeline — the longest stretch whose net change equals K is found by comparing two dates with the right balance difference.
_Complexity:_ O(n) / O(n).

---

## Pattern Group 2 — Medium: Two-Pointer, Kadane, Dutch Flag, Moore Voting & Matrix

### Two Sum  🟢
**Links:** [LeetCode](https://leetcode.com/problems/two-sum/) · [🎥 YouTube](https://youtu.be/UXDSeD9mN-k)
**Intuition / Approach:** Hashmap of value→index; for each `x` check if `target-x` was seen.
**Example:** `[2,7,11], target=9` → see 2, need 7 later ⇒ indices **[0,1]**.
**Analogy:** Matching puzzle pieces — you carry a bag of seen pieces and check if the current one completes a pair.
_Complexity:_ O(n) / O(n).

### Sort an array of 0's 1's and 2's  🟡
**Links:** [LeetCode](https://leetcode.com/problems/sort-colors/) · [🎥 YouTube](https://youtu.be/tp8JIuCXBaU)
**Intuition / Approach:** Dutch National Flag three-pointer partition (`low`, `mid`, `high`) in a single pass.
**Example:** `[2,0,1]` → swap 2↔1: `[1,0,2]` → mid on 1 advances → swap 0: `[0,1,2]`.
**Analogy:** Sorting mixed red/white/blue balls into three bins with three hands moving inward.
_Complexity:_ O(n) / O(1).

### Majority Element-I  🟢
**Links:** [LeetCode](https://leetcode.com/problems/majority-element/) · [🎥 YouTube](https://youtu.be/nP_ns3uSh80)
**Intuition / Approach:** Boyer–Moore voting: candidate with a counter, cancel opposing votes; survivor is the >n/2 majority.
**Example:** `[2,2,1,1,2,2]` → cand 2 survives ⇒ **2**.
**Analogy:** An election where each opposing pair of voters cancels out; the party still standing had the majority.
_Complexity:_ O(n) / O(1).

### Kadane's Algorithm  🟡
**Links:** [LeetCode](https://leetcode.com/problems/maximum-subarray/) · [🎥 YouTube](https://youtu.be/AHZpyENo7k4?si=QJpof4R1hHokm1hw)
**Intuition / Approach:** Running `cur += a[i]`, update `best`, reset `cur` to 0 when it goes negative (a negative prefix never helps a future sum).
**Example:** `[-2,1,-3,4,-1,2,1]` → best subarray `[4,-1,2,1]` ⇒ **6**.
**Analogy:** A hiker tracking elevation gain — drop the backpack of accumulated loss whenever it becomes dead weight.
_Complexity:_ O(n) / O(1).

### Print subarray with maximum subarray sum (extended version of above problem)  🟡
**Links:** [Article](https://takeuforward.org/data-structure/kadanes-algorithm-maximum-subarray-sum-in-an-array/) · [🎥 YouTube](https://youtu.be/AHZpyENo7k4)
**Intuition / Approach:** Same as Kadane but record `start` when resetting and freeze `[start..end]` whenever `best` improves.
**Example:** `[-2,1,-3,4,-1,2,1]` → indices **[3..6]** = `[4,-1,2,1]`.
**Analogy:** Not just knowing your best winning streak length, but writing down exactly which days it spanned.
_Complexity:_ O(n) / O(1).

### Stock Buy and Sell  🟡
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) · [🎥 YouTube](https://youtu.be/excAOvwF_Wk)
**Intuition / Approach:** Track minimum price so far; profit candidate = `price - min`; keep the best.
**Example:** `[7,1,5,3,6,4]` → min hits 1, sell at 6 ⇒ profit **5**.
**Analogy:** Remember the cheapest day to buy, and each later day ask "if I sold today, what's my gain?"
_Complexity:_ O(n) / O(1).

### Rearrange array elements by sign  🟡
**Links:** [LeetCode](https://leetcode.com/problems/rearrange-array-elements-by-sign/) · [🎥 YouTube](https://youtu.be/h4aBagy4Uok)
**Intuition / Approach:** Place positives at even indices, negatives at odd indices using two write pointers into a result array.
**Example:** `[3,1,-2,-5,2,-4]` → `[3,-2,1,-5,2,-4]`.
**Analogy:** Seating alternating boys and girls (positive/negative) in a row starting with a boy.
_Complexity:_ O(n) / O(n).

### Next Permutation  🟡
**Links:** [LeetCode](https://leetcode.com/problems/next-permutation/) · [🎥 YouTube](https://youtu.be/JDOXKqF60RQ)
**Intuition / Approach:** From the right find first `a[i] < a[i+1]` (pivot); swap it with the next-larger element to its right; reverse the suffix.
**Example:** `[1,2,3]` → pivot at 2, swap with 3 → `[1,3,2]`.
**Analogy:** An odometer rolling to the next reading — flip the smallest possible high digit and reset the rest to the lowest order.
_Complexity:_ O(n) / O(1).

### Leaders in an Array  🟡
**Links:** [Article](https://takeuforward.org/data-structure/leaders-in-an-array/) · [🎥 YouTube](https://youtu.be/cHrH9CQ8pmY)
**Intuition / Approach:** Scan right to left keeping `maxRight`; an element is a leader if it is greater than everything to its right.
**Example:** `[10,22,12,3,0,6]` → leaders **22,12,6** (reverse to get order).
**Analogy:** Mountain peaks — a peak is a "leader" if nothing taller stands between it and the horizon on its right.
_Complexity:_ O(n) / O(1).

### Longest Consecutive Sequence in an Array  🟡
**Links:** [LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/) · [🎥 YouTube](https://youtu.be/oO5uLE7EUlM)
**Intuition / Approach:** Put all in a hashset; start counting a run only from numbers with no predecessor (`x-1` absent), then extend `x+1, x+2,...`.
**Example:** `[100,4,200,1,3,2]` → run `1,2,3,4` ⇒ length **4**.
**Analogy:** Finding the longest unbroken chain of days marked on a calendar, starting only from the first day of each chain.
_Complexity:_ O(n) / O(n).

### Set Matrix Zeroes  🟡
**Links:** [LeetCode](https://leetcode.com/problems/set-matrix-zeroes/) · [🎥 YouTube](https://youtu.be/N0MgLvceX7M)
**Intuition / Approach:** Use first row and first column as markers of which rows/cols to zero; handle the first column with a separate flag.
**Example:** `[[1,1,1],[1,0,1],[1,1,1]]` → `[[1,0,1],[0,0,0],[1,0,1]]`.
**Analogy:** Marking a spreadsheet's row/column headers with a red flag, then wiping every flagged line at the end.
_Complexity:_ O(n·m) / O(1).

### Rotate matrix by 90 degrees  🟡
**Links:** [LeetCode](https://leetcode.com/problems/rotate-image/) · [🎥 YouTube](https://youtu.be/Z0R2u6gd3GU)
**Intuition / Approach:** Transpose (swap `a[i][j]`↔`a[j][i]`), then reverse each row for clockwise rotation.
**Example:** `[[1,2],[3,4]]` → transpose `[[1,3],[2,4]]` → reverse rows `[[3,1],[4,2]]`.
**Analogy:** Flipping a photo along its diagonal, then mirroring left-right lands it turned a quarter-turn.
_Complexity:_ O(n²) / O(1).

### Print the matrix in spiral manner  🟡
**Links:** [LeetCode](https://leetcode.com/problems/spiral-matrix/) · [🎥 YouTube](https://youtu.be/3Zv-s9UUrFM)
**Intuition / Approach:** Maintain four boundaries `top,bottom,left,right`; traverse top row, right col, bottom row, left col, then shrink inward.
**Example:** `[[1,2,3],[4,5,6],[7,8,9]]` → `1,2,3,6,9,8,7,4,5`.
**Analogy:** Peeling an onion layer by layer, walking around each ring before moving inward.
_Complexity:_ O(n·m) / O(1) extra.

### Count subarrays with given sum  🟡
**Links:** [LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/) · [🎥 YouTube](https://www.youtube.com/watch?v=xvNwoz-ufXA&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=32)
**Intuition / Approach:** Prefix sum + hashmap seeded `{0:1}`; add `freq[pre - k]` at each step; increment `freq[pre]`.
**Example:** `[1,1,1], k=2` → prefixes 1,2,3; matches at i=1 and i=2 ⇒ **2** subarrays.
**Analogy:** At each mile marker, ask how many earlier markers were exactly K miles behind — each pairs into a valid segment.
_Complexity:_ O(n) / O(n).

---

## Pattern Group 3 — Hard: Prefix-XOR, Merge-Sort Counting, Cyclic/Math & Intervals

### Pascal's Triangle I  🟢
**Links:** [LeetCode](https://leetcode.com/problems/pascals-triangle/) · [🎥 YouTube](https://youtu.be/bR7mQgwQ_o8)
**Intuition / Approach:** Each row starts/ends with 1; interior `= row[j-1]+row[j]` of the previous row, or build each entry with the running `nCr` update.
**Example:** rows → `[1]`, `[1,1]`, `[1,2,1]`, `[1,3,3,1]`.
**Analogy:** A cascade of coins where each pocket catches the sum of the two pockets above it.
_Complexity:_ O(n²) / O(1) extra beyond output.

### Majority Element-II  🔴
**Links:** [LeetCode](https://leetcode.com/problems/majority-element-ii/) · [🎥 YouTube](https://youtu.be/vwZj1K0e9U8)
**Intuition / Approach:** Extended Boyer–Moore with **two** candidates and counters (at most two elements exceed n/3); verify both with a final count pass.
**Example:** `[3,2,3]` → candidates 3,2; verify ⇒ **[3]**.
**Analogy:** A three-way election can crown at most two "over one-third" winners — track two front-runners, then recount to confirm.
_Complexity:_ O(n) / O(1).

### 3 Sum  🟡
**Links:** [LeetCode](https://leetcode.com/problems/3sum/) · [🎥 YouTube](https://youtu.be/DhFh8Kw7ymk)
**Intuition / Approach:** Sort; fix `i`, then two-pointer `j,k` inward looking for `-a[i]`; skip duplicates for unique triplets.
**Example:** `[-1,0,1,2,-1,-4]` → `[[-1,-1,2],[-1,0,1]]`.
**Analogy:** Pin one guest, then send two others toward each other across a sorted table until their tabs cancel the pinned bill.
_Complexity:_ O(n²) / O(1) extra.

### 4 Sum  🟡
**Links:** [LeetCode](https://leetcode.com/problems/4sum/) · [🎥 YouTube](https://youtu.be/eD95WRfh81c)
**Intuition / Approach:** Sort; fix two outer indices `i,j`, two-pointer the rest; use `long long` for the sum; skip duplicates at all four levels.
**Example:** `[1,0,-1,0,-2,2], target=0` → `[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]`.
**Analogy:** 3-Sum with an extra fixed anchor — two pins and two runners closing in.
_Complexity:_ O(n³) / O(1) extra.

### Largest Subarray with Sum 0  🟡
**Links:** [Article](https://takeuforward.org/data-structure/length-of-the-longest-subarray-with-zero-sum/) · [🎥 YouTube](https://www.youtube.com/watch?v=xmguZ6GbatA&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=23)
**Intuition / Approach:** Prefix sum + hashmap of earliest index; if a prefix repeats, the span between them sums to 0.
**Example:** `[15,-2,2,-8,1,7,10]` → longest zero-sum span length **5** (`[-2,2,-8,1,7]`).
**Analogy:** Two points on a hiking trail at the same altitude — the segment between them has net zero elevation change.
_Complexity:_ O(n) / O(n).

### Count subarrays with given xor K  🔴
**Links:** [Article](https://takeuforward.org/data-structure/count-the-number-of-subarrays-with-given-xor-k/) · [🎥 YouTube](https://youtu.be/eZr-6p0B7ME)
**Intuition / Approach:** Prefix-XOR + hashmap seeded `{0:1}`; at each step add `freq[xr ^ k]` (a previous prefix that makes the segment XOR to K).
**Example:** `[4,2,2,6,4], k=6` → count **4**.
**Analogy:** Toggle switches along a hallway — count how many earlier switch-states differ from now by exactly the pattern K.
_Complexity:_ O(n) / O(n).

### Merge Overlapping Subintervals  🟡
**Links:** [LeetCode](https://leetcode.com/problems/merge-intervals/) · [🎥 YouTube](https://youtu.be/IexN60k62jo)
**Intuition / Approach:** Sort by start; sweep, extending the last interval's end when the next start is within it, else push a new interval.
**Example:** `[[1,3],[2,6],[8,10]]` → `[[1,6],[8,10]]`.
**Analogy:** Merging overlapping calendar meetings into single blocks so your schedule shows continuous busy times.
_Complexity:_ O(n log n) / O(n).

### Merge two sorted arrays without extra space  🟡
**Links:** [LeetCode](https://leetcode.com/problems/merge-sorted-array/) · [🎥 YouTube](https://youtu.be/n7uwj04E0I4)
**Intuition / Approach:** Gap method (Shell-like) or fill from the back: compare largest remaining of each and place at the end of the combined space.
**Example:** `a=[1,3,5,7], b=[0,2,6,8]` → `a=[0,1,2,3], b=[5,6,7,8]`.
**Analogy:** Zipping two sorted lines of people into one line without a waiting room — swap out-of-order pairs across the boundary.
_Complexity:_ O((n+m) log(n+m)) gap / O(1).

### Find the repeating and missing number  🔴
**Links:** [Article](https://takeuforward.org/data-structure/find-the-repeating-and-missing-numbers/) · [🎥 YouTube](https://youtu.be/2D0D8HE6uak)
**Intuition / Approach:** Two equations: `S - Sn = X - Y` (sum diff) and `S2 - S2n = X² - Y²` (sum-of-squares diff); solve for repeating `X` and missing `Y`. Use `long long`.
**Example:** `[3,1,2,5,3]`, n=5 → repeating **3**, missing **4**.
**Analogy:** Two clues (a total mismatch and a squared-total mismatch) pin down exactly which number was double-counted and which vanished.
_Complexity:_ O(n) / O(1).

### Count Inversions  🔴
**Links:** [Article](https://takeuforward.org/data-structure/count-inversions-in-an-array) · [🎥 YouTube](https://youtu.be/AseUmwVNaoY)
**Intuition / Approach:** Merge sort; while merging, when `left[i] > right[j]`, all remaining left elements form inversions with `right[j]`.
**Example:** `[2,4,1,3,5]` → inversions **3** (`(2,1),(4,1),(4,3)`).
**Analogy:** Counting how many pairs of runners finished out of their bib-number order.
_Complexity:_ O(n log n) / O(n).

### Reverse Pairs  🔴
**Links:** [LeetCode](https://leetcode.com/problems/reverse-pairs/) · [🎥 YouTube](https://youtu.be/0e4bZaP3MDI)
**Intuition / Approach:** Merge sort with an extra count pass counting `left[i] > 2*right[j]` before the standard merge.
**Example:** `[1,3,2,3,1]` → reverse pairs **2**.
**Analogy:** Like counting inversions, but the "out of order" rule is stricter — one runner must be more than double the other.
_Complexity:_ O(n log n) / O(n).

### Maximum Product Subarray in an Array  🔴
**Links:** [LeetCode](https://leetcode.com/problems/maximum-product-subarray/)
**Intuition / Approach:** Track both running `maxProd` and `minProd` (a negative times a negative can flip to the max); swap them on a negative element.
**Example:** `[2,3,-2,4]` → best contiguous product **6** (`[2,3]`).
**Analogy:** Betting where two negatives multiply into a big positive — keep your "worst" (most negative) hand around because it might become the winner.
_Complexity:_ O(n) / O(1).

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Largest Element | 🟢 Easy | Easy: Scanning | [Article](https://takeuforward.org/data-structure/find-the-largest-element-in-an-array/) |
| 2 | Second Largest Element | 🟢 Easy | Easy: Scanning | [Article](https://takeuforward.org/data-structure/find-second-smallest-and-second-largest-element-in-an-array/) |
| 3 | Check if the Array is Sorted II | 🟢 Easy | Easy: Scanning | [LeetCode](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/) |
| 4 | Remove duplicates from Sorted array | 🟢 Easy | Easy: Two-pointer overwrite | [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) |
| 5 | Left Rotate Array by One | 🟢 Easy | Easy: Rotation | [LeetCode](https://leetcode.com/problems/rotate-array/) |
| 6 | Left Rotate Array by K Places | 🟢 Easy | Easy: Rotation | [LeetCode](https://leetcode.com/problems/rotate-array/) |
| 7 | Move Zeros to End | 🟢 Easy | Easy: Two-pointer overwrite | [LeetCode](https://leetcode.com/problems/move-zeroes/) |
| 8 | Linear Search | 🟢 Easy | Easy: Scanning | [Article](https://takeuforward.org/data-structure/linear-search-in-c/) |
| 9 | Union of two sorted arrays | 🟢 Easy | Easy: Merge scan | [Article](https://takeuforward.org/data-structure/union-of-two-sorted-arrays/) |
| 10 | Find missing number | 🟢 Easy | Easy: Math/XOR | [Article](https://www.geeksforgeeks.org/find-the-missing-number/) |
| 11 | Maximum Consecutive Ones | 🟢 Easy | Easy: Scanning | [LeetCode](https://leetcode.com/problems/max-consecutive-ones/) |
| 12 | Find the number that appears once, others twice | 🟡 Medium | Easy: Math/XOR | [LeetCode](https://leetcode.com/problems/single-number/) |
| 13 | Longest subarray with given sum K (positives) | 🟡 Medium | Easy: Sliding window | [Article](https://takeuforward.org/data-structure/longest-subarray-with-given-sum-k/) |
| 14 | Longest subarray with sum K | 🟡 Medium | Easy: Prefix-sum hashmap | [Article](https://takeuforward.org/arrays/longest-subarray-with-sum-k-postives-and-negatives) |
| 15 | Two Sum | 🟢 Easy | Medium: Two-pointer/Hashing | [LeetCode](https://leetcode.com/problems/two-sum/) |
| 16 | Sort an array of 0's 1's and 2's | 🟡 Medium | Medium: Dutch flag | [LeetCode](https://leetcode.com/problems/sort-colors/) |
| 17 | Majority Element-I | 🟢 Easy | Medium: Moore voting | [LeetCode](https://leetcode.com/problems/majority-element/) |
| 18 | Kadane's Algorithm | 🟡 Medium | Medium: Kadane | [LeetCode](https://leetcode.com/problems/maximum-subarray/) |
| 19 | Print subarray with maximum subarray sum | 🟡 Medium | Medium: Kadane | [Article](https://takeuforward.org/data-structure/kadanes-algorithm-maximum-subarray-sum-in-an-array/) |
| 20 | Stock Buy and Sell | 🟡 Medium | Medium: Greedy scan | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) |
| 21 | Rearrange array elements by sign | 🟡 Medium | Medium: Placement | [LeetCode](https://leetcode.com/problems/rearrange-array-elements-by-sign/) |
| 22 | Next Permutation | 🟡 Medium | Medium: Greedy scan | [LeetCode](https://leetcode.com/problems/next-permutation/) |
| 23 | Leaders in an Array | 🟡 Medium | Medium: Greedy scan | [Article](https://takeuforward.org/data-structure/leaders-in-an-array/) |
| 24 | Longest Consecutive Sequence | 🟡 Medium | Medium: Hashing | [LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/) |
| 25 | Set Matrix Zeroes | 🟡 Medium | Medium: Matrix | [LeetCode](https://leetcode.com/problems/set-matrix-zeroes/) |
| 26 | Rotate matrix by 90 degrees | 🟡 Medium | Medium: Matrix | [LeetCode](https://leetcode.com/problems/rotate-image/) |
| 27 | Print the matrix in spiral manner | 🟡 Medium | Medium: Matrix | [LeetCode](https://leetcode.com/problems/spiral-matrix/) |
| 28 | Count subarrays with given sum | 🟡 Medium | Medium: Prefix-sum hashmap | [LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/) |
| 29 | Pascal's Triangle I | 🟢 Easy | Hard: Combinatorics | [LeetCode](https://leetcode.com/problems/pascals-triangle/) |
| 30 | Majority Element-II | 🔴 Hard | Hard: Moore voting (n/3) | [LeetCode](https://leetcode.com/problems/majority-element-ii/) |
| 31 | 3 Sum | 🟡 Medium | Hard: Two-pointer k-sum | [LeetCode](https://leetcode.com/problems/3sum/) |
| 32 | 4 Sum | 🟡 Medium | Hard: Two-pointer k-sum | [LeetCode](https://leetcode.com/problems/4sum/) |
| 33 | Largest Subarray with Sum 0 | 🟡 Medium | Hard: Prefix-sum hashmap | [Article](https://takeuforward.org/data-structure/length-of-the-longest-subarray-with-zero-sum/) |
| 34 | Count subarrays with given xor K | 🔴 Hard | Hard: Prefix-XOR | [Article](https://takeuforward.org/data-structure/count-the-number-of-subarrays-with-given-xor-k/) |
| 35 | Merge Overlapping Subintervals | 🟡 Medium | Hard: Intervals | [LeetCode](https://leetcode.com/problems/merge-intervals/) |
| 36 | Merge two sorted arrays without extra space | 🟡 Medium | Hard: Intervals/Merge | [LeetCode](https://leetcode.com/problems/merge-sorted-array/) |
| 37 | Find the repeating and missing number | 🔴 Hard | Hard: Math/XOR | [Article](https://takeuforward.org/data-structure/find-the-repeating-and-missing-numbers/) |
| 38 | Count Inversions | 🔴 Hard | Hard: Merge-sort counting | [Article](https://takeuforward.org/data-structure/count-inversions-in-an-array) |
| 39 | Reverse Pairs | 🔴 Hard | Hard: Merge-sort counting | [LeetCode](https://leetcode.com/problems/reverse-pairs/) |
| 40 | Maximum Product Subarray | 🔴 Hard | Hard: Prefix/suffix products | [LeetCode](https://leetcode.com/problems/maximum-product-subarray/) |
