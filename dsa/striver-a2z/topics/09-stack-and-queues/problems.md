# Stack and Queues — Problems (by Pattern)

**Navigation:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by their Striver sub-step (pattern). Every problem from the dataset appears exactly once, with intuition, a worked example, and a real-world analogy.

---

## Learning — Implementations & Basic Applications

### Implement Stack using Arrays  🟢
**Links:** [Article](https://takeuforward.org/data-structure/implement-stack-using-array/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Keep a fixed array and a `top` index starting at `-1`. `push` writes at `++top`, `pop` returns `arr[top--]`, `top()` reads `arr[top]`. All operations are O(1).
**Example:** push(5), push(9) → array `[5,9]`, top=1. pop() → returns 9, top=0. top() → 5.
**Analogy:** A stack of plates on a spring-loaded dispenser — you only add or take from the top plate.
**Complexity:** O(1) per op, O(n) space.

### Implement Queue using Arrays  🟢
**Links:** [Article](https://takeuforward.org/data-structure/implement-queue-using-array/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Use a circular array with `front`, `rear`, and `size`. Enqueue at `(rear+1)%cap`, dequeue from `front`, wrap indices with modulo so freed slots are reused.
**Example:** cap=3, push(1),push(2),push(3) → full. pop() → 1 (front advances). push(4) reuses slot 0.
**Analogy:** A revolving sushi conveyor belt — plates enter at the back, leave at the front, and the belt loops around.
**Complexity:** O(1) per op, O(n) space.

### Implement Stack using Queue  🟢
**Links:** [LeetCode](https://leetcode.com/problems/implement-stack-using-queues/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Single-queue trick: after enqueuing the new element, rotate the queue by dequeuing and re-enqueuing all *older* elements so the newest sits at the front. Then `top`/`pop` are O(1); `push` is O(n).
**Example:** push(1): [1]. push(2): enqueue 2 → [1,2], rotate 1 → [2,1]. pop() → 2.
**Analogy:** A single ticket line where a VIP cuts to the front by making everyone else walk around behind them.
**Complexity:** push O(n), pop/top O(1).

### Implement Queue using Stack  🟢
**Links:** [LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Two stacks `in` and `out`. Push onto `in`. For pop/peek, if `out` is empty, pour all of `in` into `out` (reversing order); then pop from `out`. Amortized O(1).
**Example:** push(1),push(2) → in=[1,2]. pop(): out becomes [2,1] (top=1), pop returns 1.
**Analogy:** Pouring marbles from one tube into another — reversing the tube flips the order from LIFO back to FIFO.
**Complexity:** amortized O(1) per op.

### Implement stack using Linkedlist  🟢
**Links:** [Article](https://takeuforward.org/data-structure/implement-stack-using-linked-list/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Maintain a `head` pointer. `push` creates a node and links it as the new head; `pop` unlinks and returns the head. No capacity limit, O(1) per op.
**Example:** push(3): head→3. push(7): head→7→3. pop() → 7, head→3.
**Analogy:** Adding train cars to the *front* of a train and detaching from the front — the last car coupled is the first uncoupled.
**Complexity:** O(1) per op, O(n) space.

### Implement queue using Linkedlist  🟢
**Links:** [Article](https://takeuforward.org/data-structure/implement-queue-using-linked-list/) · 🎥 [YouTube](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w)
**Intuition / Approach:** Keep both `head` (front) and `tail` (rear). Enqueue links a node after `tail`; dequeue removes from `head`. Both O(1).
**Example:** push(1): head=tail=1. push(2): tail→2. pop() → 1, head→2.
**Analogy:** A checkout line where new customers join at the back and the cashier serves from the front.
**Complexity:** O(1) per op, O(n) space.

### Balanced Paranthesis  🟢
**Links:** [LeetCode](https://leetcode.com/problems/valid-parentheses/) · 🎥 [YouTube](https://youtu.be/xwjS0iZhw4I?si=UoyKpFn4Q3nf5h2R)
**Intuition / Approach:** Push every opening bracket. On a closing bracket, the stack top must be its matching opener — otherwise invalid. The string is balanced iff the stack ends empty.
**Example:** `"{[()]}"` → push `{ [ (`, then `)` matches `(`, `]` matches `[`, `}` matches `{` → empty → valid.
**Analogy:** Nested Russian dolls — each one you close must be the exact partner of the innermost one still open.
**Complexity:** O(n) time, O(n) space.

### Implement Min Stack  🔴
**Links:** [LeetCode](https://leetcode.com/problems/min-stack/) · 🎥 [YouTube](https://youtu.be/NdDIaH91P0g?si=4_Jbsq5trFvfSdUY)
**Intuition / Approach:** Support `getMin` in O(1). Simple version stores `(val, minSoFar)` pairs. Optimal O(1)-extra-space version encodes a "modified" value (`2*val - min`) when a new minimum arrives, and decodes it on pop.
**Example:** push(5)→min5; push(3)→new min3, store `2*3-5=1`; getMin→3; pop→sees 1<min so restore min=`2*3-1=5`.
**Analogy:** A backpack where you clip a note on each item recording the lightest item packed so far, so you can always answer "what's the lightest?" instantly.
**Complexity:** O(1) time, O(1) extra space (encoded variant).

---

## Prefix, Infix, PostFix Conversion Problems

### Infix to Postfix Conversion  🟡
**Links:** [Article](https://takeuforward.org/data-structure/infix-to-postfix/) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=ryeVvQWpCgwbTQrh)
**Intuition / Approach:** Shunting-yard. Scan left→right: operands go straight to output; `(` is pushed; `)` pops until `(`; an operator pops while the stack top has ≥ precedence (strict for right-associative `^`), then is pushed. Flush the stack at the end.
**Example:** `a+b*c` → output `abc*+` (`*` binds tighter, emitted before `+`).
**Analogy:** A railway shunting yard: operands roll straight through, operators wait on a siding until a higher-priority train forces them out.
**Complexity:** O(n) time, O(n) space.

### Prefix to Infix Conversion  🟡
**Links:** [Article](https://takeuforward.org/data-structure/prefix-to-infix-conversion) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=ryeVvQWpCgwbTQrh)
**Intuition / Approach:** Scan the prefix string **right→left** using a stack of strings. On an operand push it; on an operator pop two operands (top is the left one) and push `(left op right)`.
**Example:** `*+ab-cd` → build `(a+b)`, `(c-d)`, then `((a+b)*(c-d))`.
**Analogy:** Assembling flat-pack furniture from the last instruction backwards — combine the two nearest finished sub-assemblies each time you hit a connector.
**Complexity:** O(n) time, O(n) space.

### Prefix to Postfix Conversion  🟡
**Links:** [Article](https://takeuforward.org/data-structure/prefix-to-postfix-conversion) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=0pWtyDC1GhbiYP3P)
**Intuition / Approach:** Scan **right→left**. Push operands. On an operator pop two operands `x` (first) and `y` and push `x y op`.
**Example:** `*+AB-CD` → `AB+`, `CD-`, then `AB+CD-*`.
**Analogy:** Reading a recipe backwards where each verb combines the two most recently prepared ingredients into a new dish, describing action last.
**Complexity:** O(n) time, O(n) space.

### Postfix to Prefix Conversion  🟡
**Links:** [Article](https://takeuforward.org/data-structure/postfix-to-prefix-conversion) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=0pWtyDC1GhbiYP3P)
**Intuition / Approach:** Scan **left→right**. Push operands. On an operator pop two operands `y` (top) then `x` and push `op x y`.
**Example:** `AB+CD-*` → `+AB`, `-CD`, then `*+AB-CD`.
**Analogy:** Stacking building blocks: each operator caps the two blocks below it, and its label goes on top/front of the combined tower.
**Complexity:** O(n) time, O(n) space.

### Postfix to Infix Conversion  🟢
**Links:** [Article](https://takeuforward.org/data-structure/postfix-to-infix) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=0pWtyDC1GhbiYP3P)
**Intuition / Approach:** Scan **left→right**. Push operands. On an operator pop two operands `y` (top) then `x` and push `(x op y)`.
**Example:** `ab+c*` → `(a+b)`, then `((a+b)*c)`.
**Analogy:** Wrapping gifts: whenever you meet a bow (operator), you tie together the two most recently wrapped boxes into one parenthesized package.
**Complexity:** O(n) time, O(n) space.

### Infix to Prefix Conversion  🟡
**Links:** [Article](https://takeuforward.org/data-structure/infix-to-prefix/) · 🎥 [YouTube](https://youtu.be/4pIc9UBHJtk?si=0pWtyDC1GhbiYP3P)
**Intuition / Approach:** Reverse the infix string (swapping `(`↔`)`), run infix→postfix with `^` handled as strictly-greater precedence, then reverse the resulting postfix to get the prefix.
**Example:** `(a+b)*c` → reverse `c*)b+a(` → postfix of reversed → reverse back → `*+abc`.
**Analogy:** Reading a sentence in a mirror, translating it, then flipping the mirror back — a clever two-flip shortcut to reuse the postfix machinery.
**Complexity:** O(n) time, O(n) space.

---

## Monotonic Stack/Queue Problems [VVV. Imp]

### Next Greater Element  🟡
**Links:** [LeetCode](https://leetcode.com/problems/next-greater-element-i/) · 🎥 [YouTube](https://youtu.be/e7XQLtOQM3I?si=QdcHpTtx6gAHsext)
**Intuition / Approach:** Precompute next-greater for `nums2` with a monotonic (decreasing) stack scanning right→left, store answers in a hash map, then answer each `nums1` query in O(1).
**Example:** nums2=`[1,3,4,2]` → NGE `{1:3,3:4,4:-1,2:-1}`; nums1=`[4,1,2]` → `[-1,3,-1]`.
**Analogy:** Standing in a crowd and looking rightward for the first person taller than you — the stack remembers only the "still-unbeaten" tall people.
**Complexity:** O(n+m) time, O(n) space.

### Next Greater Element - 2  🟡
**Links:** [LeetCode](https://leetcode.com/problems/next-greater-element-ii/) · 🎥 [YouTube](https://youtu.be/7PrncD7v9YQ?si=UkBc7eVy9HGlBpeW)
**Intuition / Approach:** Circular array — the next greater may wrap around. Iterate `2n-1` down to `0` using index `i % n`, applying the same decreasing-stack rule; only record answers on the first pass.
**Example:** `[1,2,1]` → wrapping lets index 2 (value 1) find 2 → NGE `[2,-1,2]`.
**Analogy:** A round-table discussion — if no one to your right speaks louder, the conversation loops back to the start of the table to find the next louder voice.
**Complexity:** O(n) time, O(n) space.

### Next Smaller Element  🟡
**Links:** [Article](https://takeuforward.org/data-structure/next-smaller-element) 
**Intuition / Approach:** Mirror of NGE: scan right→left with an **increasing** stack, popping all elements `>=` the current, and the remaining top is the next smaller element.
**Example:** `[4,5,2,10,8]` → NSE `[2,2,-1,8,-1]`.
**Analogy:** Looking rightward for the first person *shorter* than you — you discard the taller people blocking your view.
**Complexity:** O(n) time, O(n) space.

### Number of Greater Elements to the Right  🟢
**Links:** [Article](https://takeuforward.org/data-structure/number-of-nges-to-the-right) 
**Intuition / Approach:** For each query index, count elements to its right strictly greater than it. Brute force is O(n·q); an offline/merge-sort or BIT approach gives better bounds, but the pattern lives with monotonic-stack style reasoning about "elements to the right".
**Example:** arr=`[3,4,2,7,5,8,10,6]`, query index 0 (value 3) → count of greater on right = 6.
**Analogy:** Counting how many people ahead of you in a queue are taller than you — a headcount, not just the first one.
**Complexity:** brute O(n·q); optimized O((n+q) log n).

### Trapping Rainwater  🔴
**Links:** [LeetCode](https://leetcode.com/problems/trapping-rain-water/) · 🎥 [YouTube](https://youtu.be/1_5VuquLbXg?si=NFG6df318_6OtGvg)
**Intuition / Approach:** Water above each bar = `min(maxLeft, maxRight) - height`. Solve with two pointers moving inward from the shorter side, or with a monotonic (decreasing) stack that resolves trapped "basins" when a taller bar arrives.
**Example:** `[0,1,0,2,1,0,1,3,2,1,2,1]` → traps 6 units of water.
**Analogy:** Rain filling the valleys of a city skyline — each dip holds water up to the shorter of its two flanking towers.
**Complexity:** O(n) time, O(1) (two-pointer) or O(n) (stack) space.

### Sum of Subarray Minimums  🟡
**Links:** [LeetCode](https://leetcode.com/problems/sum-of-subarray-minimums/) · 🎥 [YouTube](https://youtu.be/v0e8p9JCgRc?si=XAU7ekECgS5nboRw)
**Intuition / Approach:** Each element `a[i]` is the minimum of `(i - prevLessIndex) * (nextLessIndex - i)` subarrays; multiply by `a[i]` and sum. Use monotonic stacks for previous-less and next-less, breaking ties strictly on one side to avoid double counting.
**Example:** `[3,1,2,4]` → contributions sum to 17 (mod 1e9+7).
**Analogy:** Assigning credit: each team member gets paid for every project window in which they were the weakest link — count those windows exactly once.
**Complexity:** O(n) time, O(n) space.

### Asteroid Collision  🟡
**Links:** [LeetCode](https://leetcode.com/problems/asteroid-collision/) · 🎥 [YouTube](https://youtu.be/_eYGqw_VDR4?si=YyxibcHq800RqgIQ)
**Intuition / Approach:** Use a stack. A right-moving asteroid is always pushed. A left-moving one collides with right-movers on top: smaller ones explode (pop), equal ones both explode, and if it survives all it is pushed.
**Example:** `[5,10,-5]` → 5,10 pushed; -5 hits 10 (10>5) → -5 explodes → `[5,10]`.
**Analogy:** Bumper cars on a one-lane track — a car heading left only survives if it's heavier than every rightward car it meets.
**Complexity:** O(n) time, O(n) space.

### Sum of Subarray Ranges  🟡
**Links:** [LeetCode](https://leetcode.com/problems/sum-of-subarray-ranges/) · 🎥 [YouTube](https://youtu.be/gIrMptNPf5M?si=Q_GHuBvzZVs27X_U)
**Intuition / Approach:** Range = max − min. Sum over all subarrays = (sum of subarray maximums) − (sum of subarray minimums), each computed in O(n) with the monotonic-stack contribution technique.
**Example:** `[1,2,3]` → sum of ranges = 4 (subarrays' max−min: 0+0+0+1+1+2).
**Analogy:** Measuring temperature swings: for every time-window, the "range" is hottest minus coldest — total swing = total of highs minus total of lows.
**Complexity:** O(n) time, O(n) space.

### Remove K Digits  🟡
**Links:** [LeetCode](https://leetcode.com/problems/remove-k-digits/) · 🎥 [YouTube](https://youtu.be/jmbuRzYPGrg?si=WN387gwQ7aXWkUao)
**Intuition / Approach:** Build the smallest number greedily with a monotonic increasing stack: while the top digit is larger than the current and we still have removals left, pop it. Remove leftover from the end if `k>0`, strip leading zeros.
**Example:** `"1432219", k=3` → remove 4,3,2 → `"1219"`.
**Analogy:** Editing a price tag to look cheapest — erase any early big digit whenever a smaller one is coming up next.
**Complexity:** O(n) time, O(n) space.

### Largest rectangle in a histogram  🔴
**Links:** [LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/) · 🎥 [YouTube](https://youtu.be/Bzat9vgD0fs?si=DiBlLejXcr6EJoyB)
**Intuition / Approach:** For each bar, the widest rectangle at its height spans from previous-smaller to next-smaller. Use a monotonic increasing stack of indices; when a shorter bar appears, pop and compute `height * width`. Sentinels simplify draining.
**Example:** `[2,1,5,6,2,3]` → largest area = 10 (bars 5,6 over width 2 → 5×2, but 5-6 region gives 10).
**Analogy:** Fitting the biggest possible rectangular billboard flush against a city skyline — width limited by the first shorter building on each side.
**Complexity:** O(n) time, O(n) space.

### Maximum Rectangles  🔴
**Links:** [LeetCode](https://leetcode.com/problems/maximal-rectangle/) · 🎥 [YouTube](https://youtu.be/tOylVCugy9k)
**Intuition / Approach:** For a binary matrix, build a running histogram per row (heights of consecutive 1s ending at that row), then apply the largest-rectangle-in-histogram routine to each row; track the max.
**Example:** matrix rows building heights `[1,0,1,0,0]→[2,0,2,1,1]→...` → max rectangle of 1s (e.g., area 6).
**Analogy:** Snow accumulating column by column each day — every morning you measure the biggest flat rectangular slab you could carve from the current snow profile.
**Complexity:** O(n·m) time, O(m) space.

---

## Implementation Problems

### Sliding Window Maximum  🔴
**Links:** [LeetCode](https://leetcode.com/problems/sliding-window-maximum/) · 🎥 [YouTube](https://youtu.be/NwBvene4Imo?si=eU1PY-bcQfk5wdog)
**Intuition / Approach:** Maintain a decreasing deque of indices. Before adding `i`, pop smaller values from the back and drop the front if it left the window (`front <= i-k`). The front is always the current window maximum.
**Example:** `[1,3,-1,-3,5,3,6,7], k=3` → `[3,3,5,5,6,7]`.
**Analogy:** A moving spotlight over a crowd that always highlights the tallest person currently lit — shorter people behind the tallest are irrelevant.
**Complexity:** O(n) time, O(k) space.

### Stock span problem  🔴
**Links:** [LeetCode](https://leetcode.com/problems/online-stock-span/) · 🎥 [YouTube](https://youtu.be/eay-zoSRkVc?si=deNNe5i38BOAntha)
**Intuition / Approach:** Span = number of consecutive prior days with price ≤ today. Keep a monotonic stack of `(price, span)`; pop while top price ≤ today, accumulating their spans, then push the merged span. Amortized O(1) per query.
**Example:** prices `[100,80,60,70,60,75,85]` → spans `[1,1,1,2,1,4,6]`.
**Analogy:** A hiker counting how many days in a row they've climbed no higher than today's peak — collapse all the smaller hills you've already passed.
**Complexity:** amortized O(1) per query, O(n) space.

### Celebrity Problem  🔴
**Links:** [LeetCode](https://leetcode.com/accounts/login/?next=/problems/find-the-celebrity/) · 🎥 [YouTube](https://youtu.be/cEadsbTeze4?si=olXYfOs7l-SEn2zl)
**Intuition / Approach:** A celebrity is known by everyone but knows no one. Use two pointers: if `knows(a,b)`, `a` can't be celebrity → advance `a`; else `b` can't → advance `b`. Verify the single survivor knows nobody and is known by all.
**Example:** 3 people, matrix says everyone knows person 1 and 1 knows no one → celebrity = 1.
**Analogy:** Finding the one famous guest at a party — anyone who recognizes someone else is disqualified, quickly narrowing to the one person everybody recognizes.
**Complexity:** O(n) time, O(1) space.

### LRU Cache  🟡
**Links:** [Article](https://takeuforward.org/data-structure/program-for-least-recently-used-lru-page-replacement-algorithm) 
**Intuition / Approach:** Hash map (key→list node) + doubly linked list ordered by recency. On access, splice the node to the front (most recent). On insert past capacity, evict the tail (least recent). O(1) get/put.
**Example:** cap=2, put(1,1),put(2,2),get(1)→1, put(3,3) evicts key 2, get(2)→-1.
**Analogy:** A desk with limited space — the file you touch goes on top, and when you run out of room you toss whatever's been buried longest at the bottom.
**Complexity:** O(1) per op, O(capacity) space.

### LFU Cache  🔴
**Links:** [LeetCode](https://leetcode.com/problems/lfu-cache/) · 🎥 [YouTube](https://www.youtube.com/watch?v=0PSB9y8ehbk&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=79)
**Intuition / Approach:** Hash map (key→node), plus a map from frequency→doubly linked list of keys at that frequency, and a `minFreq` counter. On access, move the node to the next frequency bucket. Evict from the `minFreq` bucket's tail. O(1) get/put.
**Example:** cap=2, put(1,1),put(2,2),get(1) (freq1=2), put(3,3) evicts key 2 (least frequent), get(2)→-1.
**Analogy:** A vending machine restock policy — the least-*bought* product (not just the least-recently-bought) gets pulled from the shelf to make room.
**Complexity:** O(1) per op, O(capacity) space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Implement Stack using Arrays | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/implement-stack-using-array/) |
| 2 | Implement Queue using Arrays | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/implement-queue-using-array/) |
| 3 | Implement Stack using Queue | 🟢 Easy | Learning | [LeetCode](https://leetcode.com/problems/implement-stack-using-queues/) |
| 4 | Implement Queue using Stack | 🟢 Easy | Learning | [LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/) |
| 5 | Implement stack using Linkedlist | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/implement-stack-using-linked-list/) |
| 6 | Implement queue using Linkedlist | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/implement-queue-using-linked-list/) |
| 7 | Balanced Paranthesis | 🟢 Easy | Learning | [LeetCode](https://leetcode.com/problems/valid-parentheses/) |
| 8 | Implement Min Stack | 🔴 Hard | Learning | [LeetCode](https://leetcode.com/problems/min-stack/) |
| 9 | Infix to Postfix Conversion | 🟡 Medium | Conversion | [Article](https://takeuforward.org/data-structure/infix-to-postfix/) |
| 10 | Prefix to Infix Conversion | 🟡 Medium | Conversion | [Article](https://takeuforward.org/data-structure/prefix-to-infix-conversion) |
| 11 | Prefix to Postfix Conversion | 🟡 Medium | Conversion | [Article](https://takeuforward.org/data-structure/prefix-to-postfix-conversion) |
| 12 | Postfix to Prefix Conversion | 🟡 Medium | Conversion | [Article](https://takeuforward.org/data-structure/postfix-to-prefix-conversion) |
| 13 | Postfix to Infix Conversion | 🟢 Easy | Conversion | [Article](https://takeuforward.org/data-structure/postfix-to-infix) |
| 14 | Infix to Prefix Conversion | 🟡 Medium | Conversion | [Article](https://takeuforward.org/data-structure/infix-to-prefix/) |
| 15 | Next Greater Element | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/next-greater-element-i/) |
| 16 | Next Greater Element - 2 | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/next-greater-element-ii/) |
| 17 | Next Smaller Element | 🟡 Medium | Monotonic | [Article](https://takeuforward.org/data-structure/next-smaller-element) |
| 18 | Number of Greater Elements to the Right | 🟢 Easy | Monotonic | [Article](https://takeuforward.org/data-structure/number-of-nges-to-the-right) |
| 19 | Trapping Rainwater | 🔴 Hard | Monotonic | [LeetCode](https://leetcode.com/problems/trapping-rain-water/) |
| 20 | Sum of Subarray Minimums | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/sum-of-subarray-minimums/) |
| 21 | Asteroid Collision | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/asteroid-collision/) |
| 22 | Sum of Subarray Ranges | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/sum-of-subarray-ranges/) |
| 23 | Remove K Digits | 🟡 Medium | Monotonic | [LeetCode](https://leetcode.com/problems/remove-k-digits/) |
| 24 | Largest rectangle in a histogram | 🔴 Hard | Monotonic | [LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/) |
| 25 | Maximum Rectangles | 🔴 Hard | Monotonic | [LeetCode](https://leetcode.com/problems/maximal-rectangle/) |
| 26 | Sliding Window Maximum | 🔴 Hard | Implementation | [LeetCode](https://leetcode.com/problems/sliding-window-maximum/) |
| 27 | Stock span problem | 🔴 Hard | Implementation | [LeetCode](https://leetcode.com/problems/online-stock-span/) |
| 28 | Celebrity Problem | 🔴 Hard | Implementation | [LeetCode](https://leetcode.com/accounts/login/?next=/problems/find-the-celebrity/) |
| 29 | LRU Cache | 🟡 Medium | Implementation | [Article](https://takeuforward.org/data-structure/program-for-least-recently-used-lru-page-replacement-algorithm) |
| 30 | LFU Cache | 🔴 Hard | Implementation | [LeetCode](https://leetcode.com/problems/lfu-cache/) |
