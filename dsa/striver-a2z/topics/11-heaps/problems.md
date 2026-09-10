# Heaps — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern** (the sub-steps of Striver's A2Z Heaps section). Every problem has an intuition, a worked example, and a memorable analogy. Do them in order — earlier ones build the mechanics used later.

---

## Learning

### Heaps (Theory Video)  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps)

**Intuition / Approach:** Learn the heap as a **complete binary tree stored in an array**, obeying the heap property (parent ≥ children for max-heap, ≤ for min-heap). Master the index math — parent `(i-1)/2`, children `2i+1`, `2i+2` — and the two engine operations sift-up (on insert) and sift-down (on delete). Everything else in this section is an application of these two moves.

**Example:** Array `[9,7,6,5,4,3,2]` → viewed as a tree, root `9` ≥ children `7,6`; `7` ≥ `5,4`; `6` ≥ `3,2`. Valid max-heap. Insert `8`: append → `[...,2,8]`, sift-up past `4` and `7`, landing under `9`.

**Analogy:** A **hospital triage queue** — patients aren't fully sorted, but the most critical one is always seen next, and adding a new patient just bubbles them to their right urgency level.

---

### Implement Min Heap  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps)

**Intuition / Approach:** Back the heap with a `vector<int>`. `insert(x)`: `push_back` then **sift-up** while the child is smaller than its parent. `extractMin()`: return index 0, move the last element to the root, shrink, then **sift-down** while a child is smaller. `getMin()` is just `a[0]`.

**Example:** insert `5,3,8,1` → after inserts the array reorders to `[1,3,8,5]` (root `1`). `extractMin()` → returns `1`, moves `5` to root, sift-down swaps with `3` → `[3,5,8]`.

**Analogy:** A **stack of cafeteria trays with the lightest on top** — put a new tray in and it floats up if lighter than the one above; take the top and the pile resettles so the next-lightest surfaces.

---

### Check if an array represents a min heap  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/check-if-an-array-represents-a-min-heap)

**Intuition / Approach:** You only need to verify the **internal nodes** (indices `0 … n/2 - 1`). For each such node `i`, confirm `a[i] <= a[2i+1]` and (if it exists) `a[i] <= a[2i+2]`. If any check fails, it's not a min-heap. Leaves trivially satisfy the property.

**Example:** `[10,20,30,21,23]`, n=5, internal nodes 0,1. Node0 `10 ≤ 20,30` ✓. Node1 `20 ≤ 21,23` ✓ → **is a min-heap**. `[10,20,30,15]` → node1 `20 ≤ 15`? ✗ → not a min-heap.

**Analogy:** An **org chart sanity check** — every manager must earn less-or-equal "rank number" than their direct reports; you only inspect people who actually manage someone, not the individual contributors at the bottom.

---

### Convert Min Heap to Max Heap  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps)

**Intuition / Approach:** The min-heap ordering is useless for a max-heap, so **rebuild** with build-heap under the max comparator: run sift-down from the last internal node `n/2 - 1` down to `0`. Thanks to the height-sum bound this is `O(n)`, not `O(n log n)`.

**Example:** min-heap `[1,3,6,5,9,8]`. Heapify-max from index 2 upward: node2 `6` vs `8` → swap → `[1,3,8,5,9,6]`; node1 `3` vs `5,9` → swap with `9` → `[1,9,8,5,3,6]`; node0 `1` vs `9,8` → swap with `9`, cascade → `[9,5,8,1,3,6]` (a valid max-heap).

**Analogy:** Flipping a **"cheapest-first" bargain bin into a "most-expensive-first" showcase** — the items are the same, but you re-stack the whole display so the priciest is on top now.

---

## Medium Problems

### K-th Largest element in an array  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/kth-largest-smallest-element-in-an-array/)

**Intuition / Approach:** Maintain a **min-heap of size K**. Push each element; if size exceeds K, pop the smallest. After processing, the root is the K-th largest because the heap holds exactly the K largest values with the smallest of them on top.

**Example:** `nums=[3,2,1,5,6,4], k=2`. Heap grows/evicts: after all inserts it holds `{5,6}` (min-heap root `5`). Answer = `5`.

**Analogy:** A **VIP rope line that fits only K guests** — every new arrival tries to enter, and the least important current guest gets bounced; the person nearest the door is exactly the K-th most important.

*Complexity:* `O(n log K)` time, `O(K)` space.

---

### Kth smallest element in an array [use priority queue]  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/kth-largest-smallest-element-in-an-array/)

**Intuition / Approach:** Symmetric to K-th largest — use a **max-heap of size K**. Push each element; if size exceeds K, pop the largest. The root is then the K-th smallest, since the heap retains the K smallest values with the largest of them on top.

**Example:** `nums=[7,10,4,3,20,15], k=3`. Max-heap of size 3 ends holding `{3,4,7}` (root `7`). Answer = `7`.

**Analogy:** A **"K cheapest quotes" shortlist** — keep only K bids and always drop the most expensive one still on the list; the priciest survivor is the K-th cheapest overall.

*Complexity:* `O(n log K)` time, `O(K)` space.

---

### Sort K sorted array  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/sort-k-sorted-array)

**Intuition / Approach:** In a K-sorted (nearly sorted) array, each element is at most K positions from its final spot. Keep a **min-heap of size `K+1`**: push the first `K+1` items, then for each subsequent index pop the min into the output and push the next element. Drain the heap at the end.

**Example:** `arr=[6,5,3,2,8,10,9], k=3`. Push first 4 → heap `{2,3,5,6}`. Pop `2`, push `8`; pop `3`, push `10`; pop `5`, push `9`; then drain → `2,3,5,6,8,9,10`.

**Analogy:** A **conveyor belt of nearly-sorted parcels** with a small K+1 sized buffer bin — you always ship the smallest parcel currently in the bin, keeping the buffer just big enough to catch any parcel that arrived slightly early.

*Complexity:* `O(n log K)` time, `O(K)` space.

---

### Merge K sorted Lists  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/merge-k-sorted-lists/) · [Article](https://takeuforward.org/data-structure/merge-m-sorted-lists)

**Intuition / Approach:** Classic **K-way merge**. Put the head node of each of the K lists into a **min-heap** keyed by value. Repeatedly pop the global minimum, append it to the merged list, and push that node's `next`. Continue until the heap empties.

**Example:** lists `[1→4→5], [1→3→4], [2→6]`. Heap heads `{1,1,2}`. Pop `1`(list0)→push`4`; pop`1`(list1)→push`3`; pop`2`→push`6`; pop`3`→push`4`; … result `1→1→2→3→4→4→5→6`.

**Analogy:** **Merging several already-sorted lines at airport security** into one line — a supervisor repeatedly waves through whoever is at the front of the shortest-numbered ticket across all lines, then that line advances by one.

*Complexity:* `O(N log K)` time (N total nodes), `O(K)` space.

---

### Replace Elements by Their Rank  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/replace-elements-by-its-rank-in-the-array/)

**Intuition / Approach:** The rank of an element = its position among the **distinct sorted values** (smallest distinct → rank 1). Either sort with a min-heap / set, assign increasing ranks to distinct values in a map, then rewrite the array by lookup. Equal values share the same rank.

**Example:** `[20,15,26,2,98,6]` → sorted distinct `2,6,15,20,26,98` → ranks `2→1,6→2,15→3,20→4,26→5,98→6`. Rewrite → `[4,3,5,1,6,2]`.

**Analogy:** **Race finishing positions** — replace each runner's raw finish time with their placement (1st, 2nd, 3rd…); ties get the same medal position.

*Complexity:* `O(n log n)` time, `O(n)` space.

---

### Task Scheduler  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/task-scheduler/) · [Article](https://takeuforward.org/data-structure/task-scheduler)

**Intuition / Approach:** Count task frequencies and greedily run the **most frequent available** task each tick using a **max-heap of counts**, respecting an `n`-tick cooldown before a task can repeat. Use a temporary buffer/queue to hold cooling tasks and re-admit them when their cooldown expires; count idle ticks when nothing is runnable. (A closed-form using the max frequency also exists.)

**Example:** `tasks=["A","A","A","B","B","B"], n=2`. Order like `A B idle A B idle A B` → 8 intervals. Heap always picks the highest remaining count first to space repeats.

**Analogy:** A **DJ avoiding repeating the same song too soon** — always play the track with the most remaining requests that has cleared its "cooldown," inserting filler silence only when every popular track is still on cooldown.

*Complexity:* `O(m log 26)` = `O(m)` time (fixed 26 letters), `O(1)` space.

---

### Hand of Straights  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/hand-of-straights/) · [Article](https://takeuforward.org/data-structure/hands-of-straights)

**Intuition / Approach:** Group cards into consecutive runs of length `groupSize`. Count occurrences; repeatedly start a run from the **smallest remaining card** (a min-heap or ordered map front) and consume `x, x+1, …, x+groupSize-1`, decrementing counts. If any needed card is missing, it's impossible. Total count must be divisible by `groupSize`.

**Example:** `hand=[1,2,3,6,2,3,4,7,8], size=3`. Smallest `1`→run `1,2,3`; next smallest `2`→`2,3,4`; next `6`→`6,7,8`. All consumed → **true**.

**Analogy:** Dealing a deck into **valid straight melds in rummy** — always begin the next straight from the lowest leftover card; if you can't extend it consecutively, the hand can't be arranged.

*Complexity:* `O(n log n)` time, `O(n)` space.

---

## Hard Problems

### Design Twitter  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/design-twitter/) · [Article](https://takeuforward.org/data-structure/design-twitter)

**Intuition / Approach:** Store per-user tweet lists (each tweet tagged with a global timestamp) and a follow set. For `getNewsFeed`, do a **K-way merge** over the user's own + followees' most recent tweets using a **max-heap keyed by timestamp**, pulling the 10 newest.

**Example:** user1 posts tweet5, follows user2 who posted tweet6. Feed = merge of `{5}` and `{6}` by timestamp → newest first `[6,5]` (top 10).

**Analogy:** A **combined "latest news" ticker** merging several friends' timelines — you keep peeking at whichever friend posted most recently and pull the 10 freshest headlines overall.

*Complexity:* feed `O(K log K)` for K followees' newest tweets; follow/unfollow/post `O(1)`.

---

### Minimum Cost to Connect Sticks  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/minimum-cost-to-connect-sticks)

**Intuition / Approach:** Huffman-style greedy: repeatedly pop the **two smallest** sticks from a min-heap, pay their sum as cost, and push the combined stick back. Combining small sticks first minimizes how many times their length is re-added. Accumulate total cost until one stick remains. Use `long long`.

**Example:** `[1,8,3,5]` → min-heap. Pop `1,3`→cost `4`, push `4`; pop `4,5`→cost `9` (total 13), push `9`; pop `8,9`→cost `17` (total 30). Answer = `30`.

**Analogy:** **Joining ropes by always tying the two shortest first** — every rope's length gets "paid for" once per knot it participates in, so tying small ones early keeps the total pulling effort minimal.

*Complexity:* `O(n log n)` time, `O(n)` space.

---

### Kth largest element in a stream of running integers  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/kth-largest-element-in-a-stream/) · [Article](https://takeuforward.org/data-structure/kth-largest-element-in-a-stream-of-running-integers)

**Intuition / Approach:** Keep a **permanent min-heap of size K**. On each `add(val)`, push it and, if the heap exceeds K, pop the smallest. The root is always the current K-th largest across everything seen so far, answered in `O(log K)` per add.

**Example:** `k=3`, init `[4,5,8,2]` → heap keeps `{4,5,8}` (root `4`). `add(3)`→still `{4,5,8}`, return `4`. `add(5)`→`{5,5,8}`, return `5`. `add(10)`→`{5,8,10}`, return `8`.

**Analogy:** A **rolling leaderboard that only remembers the top K scores** — each new score competes for a slot; the lowest of the retained top K is the current "cutoff to make the board."

*Complexity:* `O(log K)` per add, `O(K)` space.

---

### Maximum Sum Combination  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/maximum-sum-combination)

**Intuition / Approach:** Given arrays A, B (each length n), find the top C sums `A[i]+B[j]`. Sort both descending; the largest sum is `A[0]+B[0]`. Use a **max-heap** seeded with that pair's sum and expand lazily to neighbours `(i+1,j)` and `(i,j+1)`, using a visited set to avoid duplicates. Pop C times.

**Example:** `A=[3,2], B=[1,4], C=2`. Best `3+4=7`; neighbours `2+4=6` and `3+1=4`. Pop `7`, then `6` → top-2 sums `[7,6]`.

**Analogy:** Exploring the **best deals in a 2-D price grid without listing all combos** — start at the top-right corner (biggest discount), then only peek at the immediate neighbours of cells you've already visited, always taking the next-best from a shortlist.

*Complexity:* `O((n + C) log n)` time, `O(n)` space.

---

### Find Median from Data Stream  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/find-median-from-data-stream/) · [Article](https://takeuforward.org/data-structure/find-median-from-data-stream)

**Intuition / Approach:** Classic **two-heaps**: a **max-heap** holds the lower half, a **min-heap** the upper half. On `addNum`, push into the correct half then rebalance so their sizes differ by at most 1. Median is the top of the larger heap, or the average of both tops when equal.

**Example:** add `1,2,3`. After `1`: lo`{1}`. After `2`: lo`{1}`, hi`{2}`, median `(1+2)/2=1.5`. After `3`: lo`{1}`, hi`{2,3}` → rebalance lo`{1,2}`, hi`{3}`, median `2`.

**Analogy:** A **see-saw with a bucket of small numbers on the left and big numbers on the right** — you keep the two sides balanced, and the median is whatever sits right at the pivot point.

*Complexity:* `addNum` `O(log n)`, `findMedian` `O(1)`, `O(n)` space.

---

### Top K Frequent Elements  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/top-k-frequent-elements/) · [Article](https://takeuforward.org/data-structure/top-k-frequent-elements)

**Intuition / Approach:** Count frequencies in a hash map, then select the K highest-frequency keys with a **min-heap of size K keyed by frequency** (evict the least frequent when size exceeds K). The heap ends holding the K most frequent elements. (Bucket sort gives an `O(n)` alternative.)

**Example:** `nums=[1,1,1,2,2,3], k=2`. Freqs `{1:3, 2:2, 3:1}`. Size-2 min-heap keeps `{2:2, 1:3}` → answer `[1,2]`.

**Analogy:** A **"trending topics" board with only K slots** — every hashtag competes by post count, and the least-mentioned one on the board gets dropped whenever a busier one appears.

*Complexity:* `O(n log K)` time, `O(n)` space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---|---|---|---|
| 1 | Heaps (Theory Video) | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps) |
| 2 | Implement Min Heap | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps) |
| 3 | Check if an array represents a min heap | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/check-if-an-array-represents-a-min-heap) |
| 4 | Convert Min Heap to Max Heap | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/introduction-to-priority-queues-using-binary-heaps) |
| 5 | K-th Largest element in an array | 🟡 Medium | Medium Problems | [Article](https://takeuforward.org/data-structure/kth-largest-smallest-element-in-an-array/) |
| 6 | Kth smallest element in an array [use priority queue] | 🟡 Medium | Medium Problems | [Article](https://takeuforward.org/data-structure/kth-largest-smallest-element-in-an-array/) |
| 7 | Sort K sorted array | 🟢 Easy | Medium Problems | [Article](https://takeuforward.org/data-structure/sort-k-sorted-array) |
| 8 | Merge K sorted Lists | 🔴 Hard | Medium Problems | [LeetCode](https://leetcode.com/problems/merge-k-sorted-lists/) |
| 9 | Replace Elements by Their Rank | 🟢 Easy | Medium Problems | [Article](https://takeuforward.org/data-structure/replace-elements-by-its-rank-in-the-array/) |
| 10 | Task Scheduler | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/task-scheduler/) |
| 11 | Hand of Straights | 🟡 Medium | Medium Problems | [LeetCode](https://leetcode.com/problems/hand-of-straights/) |
| 12 | Design Twitter | 🟡 Medium | Hard Problems | [LeetCode](https://leetcode.com/problems/design-twitter/) |
| 13 | Minimum Cost to Connect Sticks | 🟡 Medium | Hard Problems | [Article](https://takeuforward.org/data-structure/minimum-cost-to-connect-sticks) |
| 14 | Kth largest element in a stream of running integers | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/kth-largest-element-in-a-stream/) |
| 15 | Maximum Sum Combination | 🔴 Hard | Hard Problems | [Article](https://takeuforward.org/data-structure/maximum-sum-combination) |
| 16 | Find Median from Data Stream | 🔴 Hard | Hard Problems | [LeetCode](https://leetcode.com/problems/find-median-from-data-stream/) |
| 17 | Top K Frequent Elements | 🟡 Medium | Hard Problems | [LeetCode](https://leetcode.com/problems/top-k-frequent-elements/) |
