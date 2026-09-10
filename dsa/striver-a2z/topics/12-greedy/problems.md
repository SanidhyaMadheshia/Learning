# Greedy Algorithms — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** exactly as they appear in the Striver A2Z data (two sub-steps: *Easy Problems* and *Medium/Hard*). Every problem includes intuition, a worked example, and a memorable analogy. 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Easy Problems

### Assign Cookies  🟢

**Links:** [LeetCode](https://leetcode.com/problems/assign-cookies/) · [🎥 YouTube](https://youtu.be/DIX2p7vb9co?si=GofAIDimue-Av0Fi)

**Intuition / Approach:** Sort both greed factors and cookie sizes ascending. Use two pointers; give the *smallest cookie that satisfies* the current child, so large cookies stay available for greedier children. Move the child pointer only when satisfied; always advance the cookie pointer.

**Example:** greed = `[1,2,3]`, size = `[1,1]`. Child(1) ← cookie(1) ✓; Child(2) needs cookie ≥ 2, only cookie(1) left ✗. → **1** content child.

**Analogy:** Handing out snacks at a party — give the smallest cookie that still makes each kid happy, saving the big ones for the pickier kids.

**Complexity:** `O(n log n + m log m)` time, `O(1)` space.

---

### Fractional Knapsack  🟡

**Links:** [Article](https://takeuforward.org/data-structure/fractional-knapsack-problem-greedy-approach/) · [🎥 YouTube](https://youtu.be/1ibsQrnuEEg?si=8R2By3wpHo0zZVHE)

**Intuition / Approach:** Because you can take *fractions*, sort items by **value/weight ratio** descending and fill greedily. Take whole items while they fit; when the next item overflows the capacity, take the fraction that exactly fills it. Greedy is optimal here (unlike 0/1 knapsack, which needs DP).

**Example:** W = 50, items {60,10},{100,20},{120,30} → ratios 6, 5, 4. Take {60,10}→W=40, {100,20}→W=20, then 20/30 of {120} = 80. Total = **240**.

**Analogy:** Filling a backpack with gold *dust* instead of bars — you scoop the densest (most value-per-kilo) dust first and can pour in a partial scoop to top it off.

**Complexity:** `O(n log n)` time, `O(1)` space.

---

### Lemonade Change  🟢

**Links:** [LeetCode](https://leetcode.com/problems/lemonade-change/) · [🎥 YouTube](https://youtu.be/n_tmibEhO6Q?si=q1NW8MfPy0QU6fIl)

**Intuition / Approach:** Each lemonade costs $5. Track counts of $5 and $10 bills. For a $10 bill return one $5; for a $20 prefer returning $10+$5 (save $5 bills, which are more flexible), else three $5s. If change can't be made, return false.

**Example:** bills = `[5,5,5,10,20]`. Collect three $5s; $10 → give back $5 (two $5 left, one $10); $20 → give $10+$5. → **true**.

**Analogy:** A cashier making change — you hoard your small bills because they're useful in more situations, spending big bills first.

**Complexity:** `O(n)` time, `O(1)` space.

---

### Valid Paranthesis Checker  🔴

**Links:** [LeetCode](https://leetcode.com/problems/valid-parenthesis-string/) · [🎥 YouTube](https://youtu.be/cHT6sG_hUZI?si=XRHeyh7jOaLaTy3g)

**Intuition / Approach:** With `*` acting as `(`, `)`, or empty, track a **range** `[low, high]` of possible unmatched `(` counts. On `(` add to both; on `)` subtract from both; on `*` widen (`low--`, `high++`). Clamp `low` at 0; if `high` ever goes negative, fail. Valid iff `low == 0` at the end.

**Example:** `"(*)"`. Start [0,0]; `(`→[1,1]; `*`→[0,2]; `)`→[-1,1]→clamp low to [0,1]. End low=0 → **true**.

**Analogy:** Walking a tightrope with a flexible balance pole — the `*` lets you lean either way, but you must be able to end perfectly balanced with no leftover lean.

**Complexity:** `O(n)` time, `O(1)` space.

---

## Medium/Hard

### N meetings in one room  🟡

**Links:** [Article](https://takeuforward.org/data-structure/n-meetings-in-one-room/) · [🎥 YouTube](https://youtu.be/mKfhTotEguk?si=2RELeq18mpmIIN3Q)

**Intuition / Approach:** Classic activity selection. Sort meetings by **end time**; greedily attend a meeting whenever its start is *after* the last chosen meeting's end. Earliest-finish-first frees the room soonest, maximizing the count.

**Example:** meetings (start,end) = (1,2),(3,4),(0,6),(5,7),(8,9). Sorted by end: (1,2),(3,4),(0,6),(5,7),(8,9). Pick (1,2),(3,4),(5,7),(8,9) → **4**.

**Analogy:** Booking a single conference room — you say yes to whoever will vacate it earliest, so more people get a turn.

**Complexity:** `O(n log n)` time, `O(n)` space.

---

### Jump Game - I  🟢

**Links:** [LeetCode](https://leetcode.com/problems/jump-game/) · [🎥 YouTube](https://youtu.be/tZAa_jJ3SwQ?si=voKd7n9VTLDRRNzJ)

**Intuition / Approach:** Track the **farthest reachable** index while scanning. If you ever stand on an index beyond `maxReach`, you're stuck → false. Otherwise update `maxReach = max(maxReach, i + nums[i])`. Reaching or passing the last index → true.

**Example:** nums = `[2,3,1,1,4]`. i0 reach 2; i1 reach 4 (≥ last). → **true**. For `[3,2,1,0,4]`: reach stalls at index 3 → **false**.

**Analogy:** Crossing a river on stepping stones where each stone tells you the max stones you can leap — you only care about the farthest stone still within reach.

**Complexity:** `O(n)` time, `O(1)` space.

---

### Jump Game II  🟡

**Links:** [LeetCode](https://leetcode.com/problems/jump-game-ii/) · [🎥 YouTube](https://youtu.be/7SBVnw7GSTk?si=9uUouBELh9K3m2jZ)

**Intuition / Approach:** Minimize jumps via a BFS-style window. Maintain the current jump's reachable window `[l, r]`; compute the farthest index reachable from anywhere in it, then jump to that new window and increment the jump counter. Each window boundary is one jump.

**Example:** nums = `[2,3,1,1,4]`. Window [0,0] reaches 2 → jump1, window [1,2] reaches 4 (≥ last) → jump2. → **2**.

**Analogy:** Planning the fewest flights across countries — from every airport reachable on the current ticket, you look for the one that gets you furthest before booking the next flight.

**Complexity:** `O(n)` time, `O(1)` space.

---

### Minimum number of platforms required for a railway  🟡

**Links:** [Article](https://takeuforward.org/data-structure/minimum-number-of-platforms-required-for-a-railway/) · [🎥 YouTube](https://youtu.be/AsGzwR_FWok?si=165acXU_dtqOHuo9)

**Intuition / Approach:** Sort arrival and departure times separately. Sweep with two pointers: when the next arrival ≤ next departure, a train needs a platform (`+1`); otherwise a train left (`-1`). The maximum concurrent count is the answer.

**Example:** arr = `[900,940,950,1100]`, dep = `[910,1200,1120,1130]`. Overlaps at 940/950 while 910 not yet departed → peak **3** platforms.

**Analogy:** Counting how many parking spots a busy taxi rank needs — at the busiest instant, every cab present simultaneously needs its own spot.

**Complexity:** `O(n log n)` time, `O(1)` space.

---

### Job sequencing Problem  🟡

**Links:** [Article](https://takeuforward.org/data-structure/job-sequencing-problem/) · [🎥 YouTube](https://youtu.be/QbwltemZbRg?si=wvcemJ5BLPlTRmkG)

**Intuition / Approach:** Each job earns profit if finished by its deadline (unit time each). Sort by **profit descending**; for each job, assign it to the *latest* free slot at or before its deadline. Occupying late slots keeps earlier slots open for other jobs.

**Example:** jobs (id,deadline,profit) = (1,4,20),(2,1,10),(3,1,40),(4,1,30). Sorted by profit: 40,30,20,10. Place 3@slot1, 20@slot4, drop 30 & 10 (slot1 taken) → count 2, profit **60**.

**Analogy:** A freelancer scheduling gigs — take the highest-paying jobs first and slot each as close to its deadline as possible to leave room for others.

**Complexity:** `O(n log n + n·maxDeadline)` time, `O(maxDeadline)` space.

---

### Candy  🔴

**Links:** [LeetCode](https://leetcode.com/problems/candy/) · [🎥 YouTube](https://youtu.be/IIqVFvKE6RY?si=EjmuXZJNLQLUkEd7)

**Intuition / Approach:** Every child gets ≥1 candy; a child with a higher rating than a neighbor gets more than that neighbor. Do a left→right pass (enforce left rule) then a right→left pass taking the `max` (enforce right rule). Sum the result.

**Example:** ratings = `[1,0,2]`. L→R: [1,1,2]; R→L: [2,1,2]. Sum = **5**.

**Analogy:** Handing out raises where anyone paid more than a *worse-performing* neighbor must earn strictly more — you reconcile both the person on your left and right before finalizing.

**Complexity:** `O(n)` time, `O(n)` space (or `O(1)` with slope tracking).

---

### Shortest Job First  🟡

**Links:** [Article](https://takeuforward.org/Greedy/shortest-job-first-or-sjf-cpu-scheduling) · [🎥 YouTube](https://youtu.be/3-QbX1iDbXs?si=IH8QZUblr01F7UoQ)

**Intuition / Approach:** To minimize average waiting time (non-preemptive, all arrive at 0), serve jobs in **ascending burst time**. Sort bursts, accumulate a running clock as each job's waiting time equals the sum of all shorter jobs before it, then average.

**Example:** bursts = `[4,3,7,1,2]` → sorted `[1,2,3,4,7]`. Waits = 0,1,3,6,10 → sum 20, avg = 20/5 = **4**.

**Analogy:** A checkout line that lets the person with the fewest items go first — total time everyone spends waiting drops the most.

**Complexity:** `O(n log n)` time, `O(1)` space.

---

### Program for Least Recently Used (LRU) Page Replacement Algorithm  🟡

**Links:** [Article](https://takeuforward.org/data-structure/program-for-least-recently-used-lru-page-replacement-algorithm)

**Intuition / Approach:** With a fixed number of frames, on a page fault evict the page that was **used least recently**. Track recency with a queue/list (or hashmap + doubly linked list for O(1)). On a hit, mark the page as most recently used; on a miss with full frames, drop the stalest page.

**Example:** frames = 3, refs = `[1,2,3,1,4]`. Load 1,2,3 (3 faults); ref 1 → hit; ref 4 → evict LRU=2, load 4 (fault). → **4 faults**.

**Analogy:** A small desk that only holds a few books — when it's full and you need a new one, you shelve the book you haven't touched in the longest time.

**Complexity:** `O(1)` per access with hashmap + doubly linked list; `O(capacity)` space.

---

### Insert Interval  🟡

**Links:** [LeetCode](https://leetcode.com/problems/insert-interval/) · [🎥 YouTube](https://youtu.be/xxRE-46OCC8?si=a7aPuIw16zDx2lAa)

**Intuition / Approach:** Given a sorted, non-overlapping interval list and a new interval, push all intervals ending before the new one, merge every interval that overlaps the new one (expand its bounds), then push the merged interval and all remaining intervals.

**Example:** intervals = `[[1,3],[6,9]]`, new = `[2,5]`. `[1,3]` overlaps → merge to `[1,5]`; `[6,9]` after → append. Result `[[1,5],[6,9]]`.

**Analogy:** Slotting a new meeting into a tidy calendar — anything it bumps into gets absorbed into one longer block, and the rest of the day shifts around it untouched.

**Complexity:** `O(n)` time, `O(n)` space.

---

### Merge Intervals  🟡

**Links:** [LeetCode](https://leetcode.com/problems/merge-intervals/) · [🎥 YouTube](https://www.youtube.com/watch?v=2JzRBPFYbKE&list=PLgUwDviBIf0rPG3Ictpu74YWBQ1CaBkm2&index=6)

**Intuition / Approach:** Sort intervals by **start**. Keep a running merged interval; if the next start ≤ current end, extend the end via `max`; otherwise push the current interval and start a new one.

**Example:** `[[1,3],[2,6],[8,10],[15,18]]` → merge [1,3]+[2,6]=[1,6]; [8,10]; [15,18]. Result `[[1,6],[8,10],[15,18]]`.

**Analogy:** Consolidating overlapping highlighter marks on a page — touching or overlapping strokes fuse into one continuous highlight.

**Complexity:** `O(n log n)` time, `O(n)` space.

---

### Non-overlapping Intervals  🟡

**Links:** [LeetCode](https://leetcode.com/problems/non-overlapping-intervals/) · [🎥 YouTube](https://youtu.be/HDHQ8lAWakY?si=JVtLqboGdpUTOVjf)

**Intuition / Approach:** Find the minimum removals so none overlap = total minus the maximum set of compatible intervals. Sort by **end**; greedily keep an interval if its start ≥ last kept end. Removals = `n - kept`.

**Example:** `[[1,2],[2,3],[3,4],[1,3]]`. Sort by end: [1,2],[2,3],[1,3],[3,4]. Keep [1,2],[2,3],[3,4]; drop [1,3] → **1** removal.

**Analogy:** Trimming a double-booked calendar — you keep the meetings that finish earliest so the fewest have to be cancelled.

**Complexity:** `O(n log n)` time, `O(1)` extra space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Assign Cookies | 🟢 Easy | Easy Problems | [LeetCode](https://leetcode.com/problems/assign-cookies/) |
| 2 | Fractional Knapsack | 🟡 Medium | Easy Problems | [Article](https://takeuforward.org/data-structure/fractional-knapsack-problem-greedy-approach/) |
| 3 | Lemonade Change | 🟢 Easy | Easy Problems | [LeetCode](https://leetcode.com/problems/lemonade-change/) |
| 4 | Valid Paranthesis Checker | 🔴 Hard | Easy Problems | [LeetCode](https://leetcode.com/problems/valid-parenthesis-string/) |
| 5 | N meetings in one room | 🟡 Medium | Medium/Hard | [Article](https://takeuforward.org/data-structure/n-meetings-in-one-room/) |
| 6 | Jump Game - I | 🟢 Easy | Medium/Hard | [LeetCode](https://leetcode.com/problems/jump-game/) |
| 7 | Jump Game II | 🟡 Medium | Medium/Hard | [LeetCode](https://leetcode.com/problems/jump-game-ii/) |
| 8 | Minimum number of platforms required for a railway | 🟡 Medium | Medium/Hard | [Article](https://takeuforward.org/data-structure/minimum-number-of-platforms-required-for-a-railway/) |
| 9 | Job sequencing Problem | 🟡 Medium | Medium/Hard | [Article](https://takeuforward.org/data-structure/job-sequencing-problem/) |
| 10 | Candy | 🔴 Hard | Medium/Hard | [LeetCode](https://leetcode.com/problems/candy/) |
| 11 | Shortest Job First | 🟡 Medium | Medium/Hard | [Article](https://takeuforward.org/Greedy/shortest-job-first-or-sjf-cpu-scheduling) |
| 12 | Program for Least Recently Used (LRU) Page Replacement Algorithm | 🟡 Medium | Medium/Hard | [Article](https://takeuforward.org/data-structure/program-for-least-recently-used-lru-page-replacement-algorithm) |
| 13 | Insert Interval | 🟡 Medium | Medium/Hard | [LeetCode](https://leetcode.com/problems/insert-interval/) |
| 14 | Merge Intervals | 🟡 Medium | Medium/Hard | [LeetCode](https://leetcode.com/problems/merge-intervals/) |
| 15 | Non-overlapping Intervals | 🟡 Medium | Medium/Hard | [LeetCode](https://leetcode.com/problems/non-overlapping-intervals/) |
