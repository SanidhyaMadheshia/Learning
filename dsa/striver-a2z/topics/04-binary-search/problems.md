# Binary Search [1D, 2D Arrays, Search Space] — Problems (by Pattern)

**Navigation:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by pattern (matching the sub-steps in the data). Every problem includes intuition, a worked example, and a real-world analogy. 32 problems total.

---

## BS on 1D Arrays

### Search X in sorted array  🟢
**Links:** [LeetCode](https://leetcode.com/problems/binary-search/) · 🎥 [YouTube](https://youtu.be/MHf6awe89xw)

**Intuition / Approach:** Classic binary search. Keep `[low, high]`, compute `mid`, and discard the half that cannot contain the target. Runs in `O(log n)`.

**Example:** `a = [1,3,5,7,9]`, target `7`. `mid=5`(idx2)<7 → low=3; `mid=9`(idx4)>7 → high=3; `mid=7`(idx3)==7 → return 3.

**Analogy:** Guessing a number 1–100 where a friend says "higher"/"lower" — you halve the range each guess instead of counting one by one.

**Complexity:** `O(log n)` / `O(1)`.

### Lower Bound  🟢
**Links:** [Article](https://takeuforward.org/arrays/implement-lower-bound-bs-2/) · 🎥 [YouTube](https://youtu.be/6zhGS79oQ4k)

**Intuition / Approach:** Find the **first index** where `a[i] >= x`. Use the half-open template: if `a[mid] >= x`, mid is a candidate → move `high = mid`; else `low = mid + 1`. Answer is `low` in `[0, n]`.

**Example:** `a = [1,2,4,4,5]`, `x=4`. Lands on index `2` (first element `>= 4`).

**Analogy:** Finding where you'd stand in a queue sorted by height so nobody shorter than you is behind you — the first spot that's "at least your height".

**Complexity:** `O(log n)` / `O(1)`.

### Upper Bound  🟢
**Links:** [Article](https://takeuforward.org/arrays/implement-upper-bound/) · 🎥 [YouTube](https://youtu.be/6zhGS79oQ4k)

**Intuition / Approach:** First index where `a[i] > x` (strictly greater). Same template but with the strict comparison. Answer in `[0, n]`.

**Example:** `a = [1,2,4,4,5]`, `x=4`. Upper bound is index `4` (first element `> 4`, i.e. `5`).

**Analogy:** In a queue sorted by age, the first person who is *strictly older* than you — you slot in just before them.

**Complexity:** `O(log n)` / `O(1)`.

### Search insert position  🟢
**Links:** [LeetCode](https://leetcode.com/problems/search-insert-position/) · 🎥 [YouTube](https://youtu.be/6zhGS79oQ4k)

**Intuition / Approach:** If the target exists return its index; otherwise return where it would be inserted to keep the array sorted. This is exactly **lower_bound(target)**.

**Example:** `a = [1,3,5,6]`, target `2` → lower_bound → index `1` (insert between 1 and 3).

**Analogy:** Filing a new document alphabetically — you find the slot where it belongs even if no identical file exists yet.

**Complexity:** `O(log n)` / `O(1)`.

### Floor and Ceil in Sorted Array  🟢
**Links:** [Article](https://takeuforward.org/arrays/floor-and-ceil-in-sorted-array/) · 🎥 [YouTube](https://www.youtube.com/watch?v=6zhGS79oQ4k&list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF&index=3)

**Intuition / Approach:** Floor = largest element `<= x`; Ceil = smallest element `>= x`. Ceil is `lower_bound(x)`; Floor is found by tracking the last `a[mid] <= x` while binary searching.

**Example:** `a = [10,20,30,40,50]`, `x=25` → floor `20`, ceil `30`.

**Analogy:** Rounding money to the nearest available coin denomination — floor is the biggest coin that fits, ceil is the smallest coin that covers it.

**Complexity:** `O(log n)` / `O(1)`.

### First and last occurrence  🟢
**Links:** [LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) · 🎥 [YouTube](https://youtu.be/hjR1IYVx9lY)

**Intuition / Approach:** First occurrence = `lower_bound(target)`; last occurrence = `upper_bound(target) - 1`. Validate the found index actually equals target.

**Example:** `a = [5,7,7,8,8,10]`, target `8` → first index `3`, last index `4`.

**Analogy:** Finding the first and last page a chapter spans in a book indexed by topic — the run of identical entries has a start and an end.

**Complexity:** `O(log n)` / `O(1)`.

### Count Occurrences in a Sorted Array  🟢
**Links:** [Article](https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/) · 🎥 [YouTube](https://youtu.be/hjR1IYVx9lY)

**Intuition / Approach:** Count = `upper_bound(x) - lower_bound(x)`. Two binary searches give the span of equal elements.

**Example:** `a = [2,4,4,4,6]`, `x=4` → upper=4, lower=1 → count `3`.

**Analogy:** Counting how many people in a height-sorted line are exactly 170 cm — find where that group starts and where it ends, subtract.

**Complexity:** `O(log n)` / `O(1)`.

### Search in rotated sorted array-I  🟡
**Links:** [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/) · 🎥 [YouTube](https://www.youtube.com/watch?v=r3pMQ8-Ad5s&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=64)

**Intuition / Approach:** At each `mid`, one half `[low..mid]` or `[mid..high]` is sorted. Check if target lies within the sorted half; if yes go there, else go the other way. Unique elements, so `O(log n)`.

**Example:** `a = [4,5,6,7,0,1,2]`, target `0`. `mid=7`(idx3): left `[4..7]` sorted, 0 not in it → go right; find 0 at idx4.

**Analogy:** A clock face cut and re-glued at a random hour — you still know which arc is in ascending order, so you can zero in on the number you want.

**Complexity:** `O(log n)` / `O(1)`.

### Search in rotated sorted array-II  🟡
**Links:** [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) · 🎥 [YouTube](https://youtu.be/w2G2W8l__pc)

**Intuition / Approach:** Same as I, but duplicates can make `a[low]==a[mid]==a[high]`, hiding which half is sorted. In that case shrink both ends (`low++, high--`) and continue. Worst case `O(n)`.

**Example:** `a = [3,1,2,3,3,3,3]`, target `2`. When `a[low]==a[mid]==a[high]==3`, shrink ends until structure re-emerges, then find `2`.

**Analogy:** Same cut clock, but several hands show the same number — when the edges look identical you can't tell the sorted arc, so you nibble one from each end until the picture clears.

**Complexity:** `O(log n)` avg, `O(n)` worst / `O(1)`.

### Find minimum in Rotated Sorted Array  🟢
**Links:** [LeetCode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) · 🎥 [YouTube](https://youtu.be/nhEMDKMB44g)

**Intuition / Approach:** The minimum is the pivot. If `a[mid] > a[high]`, the min is in the right half → `low = mid+1`; else it's in the left (including mid) → `high = mid`. Track candidate min.

**Example:** `a = [4,5,6,7,0,1,2]`. `mid=7 > a[high]=2` → low=4; converge to `0`.

**Analogy:** Walking a mostly-uphill mountain path that was rotated so it dips once — you keep heading toward the side that still descends until you reach the valley.

**Complexity:** `O(log n)` / `O(1)`.

### Find out how many times the array is rotated  🟢
**Links:** [Article](https://takeuforward.org/arrays/find-out-how-many-times-the-array-has-been-rotated/) · 🎥 [YouTube](https://youtu.be/jtSiWTPLwd0)

**Intuition / Approach:** The number of rotations equals the **index of the minimum element**. Find the min using the rotated-min binary search; its index is the answer.

**Example:** `a = [4,5,6,7,0,1,2]` → min `0` at index `4` → rotated `4` times.

**Analogy:** A rotary combination lock that was spun; the position of the "0" mark tells you exactly how many clicks it turned.

**Complexity:** `O(log n)` / `O(1)`.

### Single element in a Sorted Array  🟡
**Links:** [LeetCode](https://leetcode.com/problems/single-element-in-a-sorted-array/) · 🎥 [YouTube](https://youtu.be/AZOmHuHadxQ)

**Intuition / Approach:** Every element appears twice except one. Before the single element, the first of each pair sits at an even index; after it, this parity breaks. Binary search on parity: if `mid` is even and `a[mid]==a[mid+1]` the single is to the right, else to the left.

**Example:** `a = [1,1,2,3,3,4,4,8,8]`. Parity check narrows to index `2` → single element `2`.

**Analogy:** Socks paired on a shelf; up to one point every left sock is at an even slot, but after the lone sock the pairing shifts by one — the shift reveals the odd one out.

**Complexity:** `O(log n)` / `O(1)`.

### Find peak element  🟡
**Links:** [LeetCode](https://leetcode.com/problems/find-peak-element/) · 🎥 [YouTube](https://youtu.be/cXxmbemS6XM)

**Intuition / Approach:** A peak is greater than its neighbors. If `a[mid] < a[mid+1]` a peak lies to the right (climb uphill) → `low = mid+1`; else to the left (including mid) → `high = mid`. Always converges to *a* peak.

**Example:** `a = [1,2,1,3,5,6,4]`. `mid` slopes up → move right → converge to peak index `5` (value `6`).

**Analogy:** Hiking in fog: always step toward the higher neighbor and you're guaranteed to reach a summit, even without seeing the whole terrain.

**Complexity:** `O(log n)` / `O(1)`.

---

## BS on Answers

### Find square root of a number  🟡
**Links:** [Article](https://takeuforward.org/binary-search/finding-sqrt-of-a-number-using-binary-search/) · 🎥 [YouTube](https://youtu.be/Bsv3FPUX_BA)

**Intuition / Approach:** Search space `[1, n]`. Find the largest `x` with `x*x <= n` (floor sqrt). Predicate `x*x <= n` is monotone. Use `long long` to avoid overflow.

**Example:** `n=28`. Largest `x` with `x*x<=28` is `5` (25<=28, 36>28) → floor sqrt `5`.

**Analogy:** Sizing the biggest square tile whose area fits inside a given room without exceeding it — try mid sizes and shrink the range.

**Complexity:** `O(log n)` / `O(1)`.

### Find Nth root of a number  🟡
**Links:** [Article](https://takeuforward.org/data-structure/nth-root-of-a-number-using-binary-search/) · 🎥 [YouTube](https://www.youtube.com/watch?v=WjpswYrS2nY&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=62)

**Intuition / Approach:** Search `[1, m]` for `x` with `x^n == m`. A helper raises `x` to `n` with early cutoff once it exceeds `m` (to avoid overflow). If exact match return `x`, else `-1`.

**Example:** `n=3, m=27`. `x=3` → `3^3=27` → return `3`.

**Analogy:** Finding the exact side length of a cube given its volume — guess a side, cube it, adjust up or down.

**Complexity:** `O(n · log m)` / `O(1)`.

### Koko eating bananas  🟡
**Links:** [LeetCode](https://leetcode.com/problems/koko-eating-bananas/) · 🎥 [YouTube](https://youtu.be/qyfekrNni90)

**Intuition / Approach:** Search eating speed `k` in `[1, max(pile)]`. Predicate: total hours `= sum(ceil(pile/k)) <= h`. Larger `k` → fewer hours (monotone). Find the smallest feasible `k`.

**Example:** `piles=[3,6,7,11], h=8`. `k=4` → hours `1+2+2+3=8<=8` feasible; `k=3` → `1+2+3+4=10>8` infeasible → answer `4`.

**Analogy:** Choosing the slowest comfortable jogging pace that still gets you to work on time — go as slow as possible without being late.

**Complexity:** `O(n log(max))` / `O(1)`.

### Minimum days to make M bouquets  🟡
**Links:** [LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) · 🎥 [YouTube](https://youtu.be/TXAuxeYBTdg)

**Intuition / Approach:** Search `day` in `[min(bloom), max(bloom)]`. Predicate: after `day` days, can we form `m` bouquets each needing `k` adjacent bloomed flowers? Count consecutive bloomed runs. Monotone in days.

**Example:** `bloomDay=[1,10,3,10,2], m=3, k=1`. day `3` → flowers `[1,-,3,-,2]` bloomed = 3 → 3 bouquets → feasible; answer `3`.

**Analogy:** Waiting for a garden to bloom enough to assemble a fixed number of adjacent-flower bouquets — the earliest day everything you need has opened.

**Complexity:** `O(n log(maxDay))` / `O(1)`.

### Find the smallest divisor  🟡
**Links:** [LeetCode](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) · 🎥 [YouTube](https://youtu.be/UvBKTVaG6U8)

**Intuition / Approach:** Search divisor `d` in `[1, max(a)]`. Predicate: `sum(ceil(a[i]/d)) <= threshold`. Larger `d` → smaller sum (monotone). Find smallest feasible `d`.

**Example:** `a=[1,2,5,9], threshold=6`. `d=5` → `1+1+1+2=5<=6` feasible; `d=4` → `1+1+2+3=7>6` → answer `5`.

**Analogy:** Picking the smallest bucket size so that pouring water in "ceiling" scoops keeps the total number of scoops under a cap.

**Complexity:** `O(n log(max))` / `O(1)`.

### Capacity to Ship Packages Within D Days  🟡
**Links:** [LeetCode](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) · 🎥 [YouTube](https://youtu.be/MG-Ac4TAvTY)

**Intuition / Approach:** Search capacity in `[max(weights), sum(weights)]`. Predicate: greedily pack packages in order; count days needed with that capacity; feasible if `days <= D`. Find smallest feasible capacity.

**Example:** `weights=[1..10], D=5`. capacity `15` splits into `[1..5],[6,7],[8,9],[10]`... days check → smallest feasible is `15`.

**Analogy:** Choosing the smallest truck that can still clear a loading dock in a set number of days, loading boxes in the order they arrive.

**Complexity:** `O(n log(sum))` / `O(1)`.

### Kth Missing Positive Number  🟡
**Links:** [LeetCode](https://leetcode.com/problems/kth-missing-positive-number/) · 🎥 [YouTube](https://youtu.be/uZ0N_hZpyps)

**Intuition / Approach:** At index `i`, the count of missing numbers before `a[i]` is `a[i] - (i+1)`. Binary search the first index where missing count `>= k`; answer is `low + k` (or `k + high + 1`).

**Example:** `a=[2,3,4,7,11], k=5`. Missing counts: idx0→1, idx3→3, idx4→6. First index with `>=5` is 4 → answer `low + k = 4 + 5 = 9`.

**Analogy:** Numbered lockers with some missing; you track how many numbers have gone missing by each locker to jump straight to the k-th gap.

**Complexity:** `O(log n)` / `O(1)`.

### Aggressive Cows  🔴
**Links:** [Article](https://takeuforward.org/data-structure/aggressive-cows-detailed-solution/) · 🎥 [YouTube](https://youtu.be/R_Mfw4ew-Vo)

**Intuition / Approach:** Place `k` cows in stalls to **maximize the minimum distance**. Sort stalls. Search distance `d` in `[1, max-min]`. Predicate: greedily place cows keeping gap `>= d`; feasible if we place all `k`. This is a **maximization** — find the largest feasible `d`.

**Example:** `stalls=[1,2,4,8,9], k=3`. `d=3` → place at 1,4,8 → 3 cows feasible; `d=4` → 1,8 only 2 → infeasible → answer `3`.

**Analogy:** Seating rival guests as far apart as possible in a row of chairs so the closest pair is still comfortable — push the minimum gap as large as it can go.

**Complexity:** `O(n log(range))` / `O(1)`.

### Book Allocation Problem  🔴
**Links:** [Article](https://takeuforward.org/data-structure/allocate-minimum-number-of-pages/) · 🎥 [YouTube](https://www.youtube.com/watch?v=gYmWHvRHu-s&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=69)

**Intuition / Approach:** Allocate contiguous books to `m` students to **minimize the maximum pages** any student reads. Search `[max(pages), sum(pages)]`. Predicate: greedily assign; count students needed so no one exceeds `mid`; feasible if `students <= m`. Find smallest feasible max.

**Example:** `pages=[12,34,67,90], m=2`. Answer `113` — student1 gets `[12,34,67]=113`, student2 gets `[90]`; the max is minimized.

**Analogy:** Splitting a book pile between two readers along the shelf so the more-burdened reader has as light a load as possible.

**Complexity:** `O(n log(sum))` / `O(1)`.

### Split array - largest sum  🔴
**Links:** [LeetCode](https://leetcode.com/problems/split-array-largest-sum/) · 🎥 [YouTube](https://www.youtube.com/watch?v=thUd_WJn6wk&list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF&index=20)

**Intuition / Approach:** Identical to Book Allocation. Split into `k` contiguous subarrays minimizing the largest subarray sum. Search `[max, sum]`; predicate counts subarrays whose sum stays `<= mid`; feasible if count `<= k`.

**Example:** `a=[7,2,5,10,8], k=2`. Answer `18` — `[7,2,5]=14` and `[10,8]=18`; largest sum minimized.

**Analogy:** Cutting a long ribbon into k pieces so the longest piece is as short as possible.

**Complexity:** `O(n log(sum))` / `O(1)`.

### Painter's Partition  🟡
**Links:** [Article](https://takeuforward.org/arrays/painters-partition-problem/) · 🎥 [YouTube](https://www.youtube.com/watch?v=thUd_WJn6wk&list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF&index=20)

**Intuition / Approach:** Same template again: `k` painters paint contiguous boards; minimize the time = max board-length assigned to a painter (time proportional to length). Search `[max, sum]`; feasible if boards fit in `<= k` painters within `mid` units.

**Example:** `boards=[10,20,30,40], k=2`. Answer `60` — painter1 `[10,20,30]=60`, painter2 `[40]`.

**Analogy:** Assigning fence sections to painters so the slowest-finishing painter finishes as early as possible.

**Complexity:** `O(n log(sum))` / `O(1)`.

### Minimize Max Distance to Gas Station  🔴
**Links:** [LeetCode](https://leetcode.com/problems/minimize-max-distance-to-gas-station/) · 🎥 [YouTube](https://www.youtube.com/watch?v=kMSBvlZ-_HA&list=PLgUwDviBIf0pMFMWuuvDNMAkoQFi-h0ZF&index=21)

**Intuition / Approach:** Add `k` stations to minimize the maximum gap between adjacent stations. **Binary search on real distance** `d` in `[0, maxGap]`. Predicate: stations needed `= sum(floor(gap/d))`; feasible if `<= k`. Iterate with epsilon or fixed count.

**Example:** `stations=[1,2,3,4,5,...,10], k=9`. Binary search on `d` converges to the minimal achievable max gap (≈ `0.5`).

**Analogy:** Dropping extra rest stops along a highway so the longest stretch without a stop is as short as possible.

**Complexity:** `O(n · iters)` (float) / `O(1)`.

### Median of 2 sorted arrays  🔴
**Links:** [LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/) · 🎥 [YouTube](https://www.youtube.com/watch?v=NTop3VTjmxk&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=65)

**Intuition / Approach:** Binary search a **partition** of the smaller array so that the left halves of both arrays together hold `(m+n+1)/2` elements and every left element `<= every right element` (`l1<=r2 && l2<=r1`). Then the median comes from the boundary max/min. `O(log(min(m,n)))`.

**Example:** `A=[1,3], B=[2]`. Correct partition puts `{1,2}` on the left, `{3}` on the right → median `2`.

**Analogy:** Merging two sorted decks of cards by picking the exact cut point in each deck so the middle card falls out — without actually interleaving them.

**Complexity:** `O(log(min(m,n)))` / `O(1)`.

### Kth element of 2 sorted arrays  🟡
**Links:** [Article](https://takeuforward.org/data-structure/k-th-element-of-two-sorted-arrays/) · 🎥 [YouTube](https://youtu.be/D1oDwWCq50g)

**Intuition / Approach:** Same partition idea as median, but fix the left-side size to exactly `k`. Binary search how many of the `k` come from the smaller array; validate `l1<=r2 && l2<=r1`; answer is `max(l1, l2)`.

**Example:** `A=[2,3,6,7,9], B=[1,4,8,10], k=5`. Partition so left holds 5 elements `{1,2,3,4,6}` → 5th element `6`.

**Analogy:** Finding the k-th finisher across two separate ranking lists without merging them — choose how many of the top-k came from each list.

**Complexity:** `O(log(min(m,n)))` / `O(1)`.

---

## BS on 2D Arrays

### Find row with maximum 1's  🟢
**Links:** [Article](https://takeuforward.org/arrays/find-the-row-with-maximum-number-of-1s/) · 🎥 [YouTube](https://youtu.be/SCz-1TtYxDI)

**Intuition / Approach:** Each row is sorted (0s then 1s). Count of 1s in a row = `n - lower_bound(row, 1)`. Binary search each row for the first `1`; track the row with the most 1s. `O(m log n)`.

**Example:** `mat=[[0,0,1],[0,1,1],[0,0,0]]`. Row1 has 2 ones (most) → answer row `1`.

**Analogy:** Scanning shelves where books are pushed to the right; the shelf whose books start earliest holds the most — a quick binary probe per shelf finds it.

**Complexity:** `O(m log n)` / `O(1)`.

### Search in a 2D matrix  🔴
**Links:** [LeetCode](https://leetcode.com/problems/search-a-2d-matrix/) · 🎥 [YouTube](https://youtu.be/ZYpYur0znng)

**Intuition / Approach:** The matrix is fully sorted row-major (each row's first element > previous row's last). Treat it as one array of length `m*n` and binary search, mapping flat index `i` to `(i/n, i%n)`. `O(log(m*n))`.

**Example:** `mat=[[1,3,5],[7,9,11]]`, target `9`. Flat length 6; `mid=3` → `mat[1][0]=7<9` → search right → find `9`.

**Analogy:** A dictionary where pages continue seamlessly — you binary search the "virtual" single stream of words rather than page by page.

**Complexity:** `O(log(m·n))` / `O(1)`.

### Search in 2D matrix - II  🔴
**Links:** [LeetCode](https://leetcode.com/problems/search-a-2d-matrix-ii/) · 🎥 [YouTube](https://youtu.be/9ZbB397jU4k)

**Intuition / Approach:** Rows and columns are each sorted, but not globally. Start at **top-right**: if `cell > target` move left, if `cell < target` move down. Each step eliminates a row or column → `O(m+n)`.

**Example:** `mat` top-right `= 15`, target `5`. `15>5` → left; `11>5` → left; ... move down/left until `5` found.

**Analogy:** Standing at the northeast corner of a sorted grid city — go west for smaller streets, south for bigger blocks, never backtracking.

**Complexity:** `O(m + n)` / `O(1)`.

### Find Peak Element - II  🟡
**Links:** [LeetCode](https://leetcode.com/problems/find-a-peak-element-ii/) · 🎥 [YouTube](https://youtu.be/nGGp5XBzC4g?si=WCop5C6Azj5gAELH)

**Intuition / Approach:** Binary search on **columns**. For the middle column, find the row of its maximum. If that max is greater than both horizontal neighbors it's a 2D peak; otherwise move toward the larger neighbor's column half. `O(m log n)`.

**Example:** `mat=[[1,4],[3,2]]`. Middle col max is `4`; its neighbor to the left is `1` → `4` is a peak → return `(0,1)`.

**Analogy:** Surveying a mountain range column by column: check the tallest point of a ridge, then walk toward the taller adjacent ridge until you can't go higher.

**Complexity:** `O(m log n)` / `O(1)`.

### Matrix Median  🔴
**Links:** [Article](https://takeuforward.org/data-structure/median-of-row-wise-sorted-matrix/) · 🎥 [YouTube](https://youtu.be/Q9wXgdxJq48?si=ScI_0uzJh7yg8nrX)

**Intuition / Approach:** Binary search on the **value range** `[min, max]`. For a candidate `x`, count elements `<= x` across all rows (each via `upper_bound`). The median is the smallest `x` whose count `>= (m*n+1)/2`. `O(m log n log(range))`.

**Example:** `mat=[[1,3,5],[2,6,9],[3,6,9]]` (9 elems, need count>=5). Binary search value → median `5`.

**Analogy:** Guessing a salary threshold and asking "how many earn at most this?" — adjust the threshold until exactly half the people fall below it.

**Complexity:** `O(m log n · log(range))` / `O(1)`.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Search X in sorted array | 🟢 Easy | BS on 1D | [LeetCode](https://leetcode.com/problems/binary-search/) |
| 2 | Lower Bound | 🟢 Easy | BS on 1D | [Article](https://takeuforward.org/arrays/implement-lower-bound-bs-2/) |
| 3 | Upper Bound | 🟢 Easy | BS on 1D | [Article](https://takeuforward.org/arrays/implement-upper-bound/) |
| 4 | Search insert position | 🟢 Easy | BS on 1D | [LeetCode](https://leetcode.com/problems/search-insert-position/) |
| 5 | Floor and Ceil in Sorted Array | 🟢 Easy | BS on 1D | [Article](https://takeuforward.org/arrays/floor-and-ceil-in-sorted-array/) |
| 6 | First and last occurrence | 🟢 Easy | BS on 1D | [LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) |
| 7 | Count Occurrences in a Sorted Array | 🟢 Easy | BS on 1D | [Article](https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/) |
| 8 | Search in rotated sorted array-I | 🟡 Medium | BS on 1D | [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/) |
| 9 | Search in rotated sorted array-II | 🟡 Medium | BS on 1D | [LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) |
| 10 | Find minimum in Rotated Sorted Array | 🟢 Easy | BS on 1D | [LeetCode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) |
| 11 | Find how many times the array is rotated | 🟢 Easy | BS on 1D | [Article](https://takeuforward.org/arrays/find-out-how-many-times-the-array-has-been-rotated/) |
| 12 | Single element in a Sorted Array | 🟡 Medium | BS on 1D | [LeetCode](https://leetcode.com/problems/single-element-in-a-sorted-array/) |
| 13 | Find peak element | 🟡 Medium | BS on 1D | [LeetCode](https://leetcode.com/problems/find-peak-element/) |
| 14 | Find square root of a number | 🟡 Medium | BS on Answers | [Article](https://takeuforward.org/binary-search/finding-sqrt-of-a-number-using-binary-search/) |
| 15 | Find Nth root of a number | 🟡 Medium | BS on Answers | [Article](https://takeuforward.org/data-structure/nth-root-of-a-number-using-binary-search/) |
| 16 | Koko eating bananas | 🟡 Medium | BS on Answers | [LeetCode](https://leetcode.com/problems/koko-eating-bananas/) |
| 17 | Minimum days to make M bouquets | 🟡 Medium | BS on Answers | [LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) |
| 18 | Find the smallest divisor | 🟡 Medium | BS on Answers | [LeetCode](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) |
| 19 | Capacity to Ship Packages Within D Days | 🟡 Medium | BS on Answers | [LeetCode](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) |
| 20 | Kth Missing Positive Number | 🟡 Medium | BS on Answers | [LeetCode](https://leetcode.com/problems/kth-missing-positive-number/) |
| 21 | Aggressive Cows | 🔴 Hard | BS on Answers | [Article](https://takeuforward.org/data-structure/aggressive-cows-detailed-solution/) |
| 22 | Book Allocation Problem | 🔴 Hard | BS on Answers | [Article](https://takeuforward.org/data-structure/allocate-minimum-number-of-pages/) |
| 23 | Split array - largest sum | 🔴 Hard | BS on Answers | [LeetCode](https://leetcode.com/problems/split-array-largest-sum/) |
| 24 | Painter's Partition | 🟡 Medium | BS on Answers | [Article](https://takeuforward.org/arrays/painters-partition-problem/) |
| 25 | Minimize Max Distance to Gas Station | 🔴 Hard | BS on Answers | [LeetCode](https://leetcode.com/problems/minimize-max-distance-to-gas-station/) |
| 26 | Median of 2 sorted arrays | 🔴 Hard | BS on Answers | [LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/) |
| 27 | Kth element of 2 sorted arrays | 🟡 Medium | BS on Answers | [Article](https://takeuforward.org/data-structure/k-th-element-of-two-sorted-arrays/) |
| 28 | Find row with maximum 1's | 🟢 Easy | BS on 2D | [Article](https://takeuforward.org/arrays/find-the-row-with-maximum-number-of-1s/) |
| 29 | Search in a 2D matrix | 🔴 Hard | BS on 2D | [LeetCode](https://leetcode.com/problems/search-a-2d-matrix/) |
| 30 | Search in 2D matrix - II | 🔴 Hard | BS on 2D | [LeetCode](https://leetcode.com/problems/search-a-2d-matrix-ii/) |
| 31 | Find Peak Element - II | 🟡 Medium | BS on 2D | [LeetCode](https://leetcode.com/problems/find-a-peak-element-ii/) |
| 32 | Matrix Median | 🔴 Hard | BS on 2D | [Article](https://takeuforward.org/data-structure/median-of-row-wise-sorted-matrix/) |
