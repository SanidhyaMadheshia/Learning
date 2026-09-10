# Stack and Queues — Resources & References

**Navigation:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Stacks & Queues — Full Implementation (takeUforward)](https://youtu.be/tqQ5fTamIN4?si=ofLt8Zt1ZvhikZ6w) — Striver's one-shot on implementing stack/queue via arrays, linked lists, and each other.
- [Prefix / Infix / Postfix Conversions (takeUforward)](https://youtu.be/4pIc9UBHJtk?si=ryeVvQWpCgwbTQrh) — all six expression-conversion problems in one video.
- [Next Greater Element using Stack (takeUforward)](https://youtu.be/e7XQLtOQM3I?si=QdcHpTtx6gAHsext) — the canonical monotonic-stack introduction.
- [Next Greater Element II — circular array (takeUforward)](https://youtu.be/7PrncD7v9YQ?si=UkBc7eVy9HGlBpeW) — handling wrap-around.
- [Trapping Rain Water (takeUforward)](https://youtu.be/1_5VuquLbXg?si=NFG6df318_6OtGvg) — brute, prefix arrays, two-pointer, and stack.
- [Sum of Subarray Minimums (takeUforward)](https://youtu.be/v0e8p9JCgRc?si=XAU7ekECgS5nboRw) — contribution technique with monotonic stacks.
- [Sum of Subarray Ranges (takeUforward)](https://youtu.be/gIrMptNPf5M?si=Q_GHuBvzZVs27X_U) — max-sum minus min-sum.
- [Asteroid Collision (takeUforward)](https://youtu.be/_eYGqw_VDR4?si=YyxibcHq800RqgIQ) — stack simulation.
- [Remove K Digits (takeUforward)](https://youtu.be/jmbuRzYPGrg?si=WN387gwQ7aXWkUao) — greedy monotonic stack.
- [Largest Rectangle in Histogram (takeUforward)](https://youtu.be/Bzat9vgD0fs?si=DiBlLejXcr6EJoyB) — the histogram stack pattern.
- [Maximal Rectangle / Maximum Rectangles (takeUforward)](https://youtu.be/tOylVCugy9k) — histogram-per-row technique.
- [Sliding Window Maximum (takeUforward)](https://youtu.be/NwBvene4Imo?si=eU1PY-bcQfk5wdog) — monotonic deque.
- [Online Stock Span (takeUforward)](https://youtu.be/eay-zoSRkVc?si=deNNe5i38BOAntha) — monotonic stack of (price, span).
- [Celebrity Problem (takeUforward)](https://youtu.be/cEadsbTeze4?si=olXYfOs7l-SEn2zl) — two-pointer elimination.
- [Min Stack (takeUforward)](https://youtu.be/NdDIaH91P0g?si=4_Jbsq5trFvfSdUY) — O(1) getMin with the encoding trick.
- [LFU Cache (Striver playlist)](https://www.youtube.com/watch?v=0PSB9y8ehbk&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=79) — frequency-bucket design.

## 📝 Articles & Tutorials

- [Introduction to Monotonic Stack (GeeksforGeeks)](https://www.geeksforgeeks.org/introduction-to-monotonic-stack-data-structure-and-algorithm-tutorials/amp/) — what a monotonic stack is and why it's O(n).
- [How to Identify and Solve Monotonic Stack Problems (GeeksforGeeks)](https://www.geeksforgeeks.org/dsa/how-to-identify-and-solve-monotonic-stack-problems/) — recognition signals and a decision framework.
- [Introduction to Monotonic Queues (GeeksforGeeks)](https://www.geeksforgeeks.org/dsa/introduction-to-monotonic-queues/) — the deque variant behind sliding-window problems.
- [Next Greater Element in Array (GeeksforGeeks)](https://www.geeksforgeeks.org/dsa/next-greater-element/) — step-by-step NGE.
- [Monotonic Stack (Hello Interview)](https://www.hellointerview.com/learn/code/stack/monotonic-stack) — interview-focused walkthrough with templates.
- [Monotonic Stack Playbook — A Visual Guide (Medium)](https://medium.com/@megha_bh/monotonic-stack-playbook-a-visual-guide-with-mind-map-e07f24f14e17) — mind-map + visuals.
- [Monotonic Stack: The Matrix of Array Problems (dev.to)](https://dev.to/timevolt/monotonic-stack-the-matrix-of-array-problems-3ieo) — links many problems to one pattern.
- [Shunting-Yard Algorithm — infix to RPN (GitHub write-up)](https://github.com/brettshollenberger/shunting-yard-algorithm/blob/master/README.md) — Dijkstra's algorithm explained.
- [Shunting-Yard notes (Willamette University, PDF)](https://people.willamette.edu/~fruehr/353/archive/ShuntingYard.pdf) — academic treatment with worked examples.
- [RPN / Shunting Yard (US Naval Academy)](https://www.usna.edu/Users/cs/crabbe/SI312/current/project/rpn/rpn.html) — the railyard analogy and full algorithm.
- [The Shunting-yard Algorithm (Medium)](https://tylerpexton-70687.medium.com/the-shunting-yard-algorithm-b840844141b2) — PEMDAS-focused explanation.

## 🧮 Visualizers & Tools

- [VisuAlgo — Linked List / Stack / Queue / Deque](https://visualgo.net/en/list) — animated stack & queue operations.
- [USFCA Data Structure Visualizations (Stack — Array & LinkedList)](https://www.cs.usfca.edu/~galles/visualization/StackArray.html) — classic step-through visualizer.
- [USFCA — Queue (Array & LinkedList)](https://www.cs.usfca.edu/~galles/visualization/QueueArray.html) — enqueue/dequeue animation.
- [Stack Visualizer — Shunting-Yard & Postfix Evaluation](https://www.stackvisualizer.online/) — interactive expression evaluation using a stack.

## ❓ Most-Asked Interview Questions

1. **What's the difference between a stack and a queue?** Stack is LIFO (last in, first out); queue is FIFO (first in, first out). Stacks fit nesting/backtracking; queues fit scheduling/BFS.
2. **How do you implement a queue using two stacks (and its complexity)?** Push to `in`; when popping, if `out` is empty, transfer all of `in` to `out` (reversing), then pop from `out`. Amortized O(1) per operation.
3. **How do you get `getMin()` from a stack in O(1)?** Store `(value, minSoFar)` pairs, or use the `2*val - min` encoding trick to achieve O(1) time and O(1) extra space.
4. **Why is a monotonic-stack solution O(n) despite the inner while loop?** Amortization: every element is pushed once and popped at most once, so total push/pop work is bounded by 2n.
5. **When do you use a decreasing vs increasing monotonic stack?** Decreasing stack finds next/previous *greater*; increasing stack finds next/previous *smaller*.
6. **How do you find the next greater element in a circular array?** Iterate `2n` times using `i % n` with a decreasing stack, recording answers only on the first pass.
7. **Explain the Shunting-Yard algorithm.** Scan infix left→right; operands to output, `(` pushed, `)` pops to `(`, operators pop while top has ≥ precedence (strict for right-associative `^`), then push. Flush at the end.
8. **How is `^` (exponent) handled differently in conversions?** It is right-associative, so use strictly-greater precedence comparison so `2^3^2` = `2^(3^2)`.
9. **How does the monotonic deque solve Sliding Window Maximum in O(n)?** Keep a decreasing deque of indices; pop smaller values from the back, drop out-of-window indices from the front; the front is always the window max.
10. **Explain the histogram largest-rectangle stack approach.** Maintain increasing indices; when a shorter bar arrives, pop and compute `height * width` where width spans from previous-smaller to current index. Use sentinels to drain.
11. **How do you extend histogram logic to Maximal Rectangle in a binary matrix?** Build a running histogram of consecutive 1s per row, then apply largest-rectangle-in-histogram to each row and track the max.
12. **Design an LRU cache with O(1) operations.** Hash map (key→node) + doubly linked list ordered by recency; move-to-front on access, evict the tail on overflow.
13. **How does LFU differ from LRU?** LFU evicts the least *frequently* used item using frequency buckets and a `minFreq` pointer; LRU evicts the least *recently* used with a single recency-ordered list.
14. **Solve the Celebrity Problem in O(n) / O(1).** Two pointers: if `knows(a,b)` eliminate `a`, else eliminate `b`; verify the survivor knows nobody and is known by all.
15. **How do you validate balanced parentheses with multiple bracket types?** Push openers; on a closer, the stack top must be the exact matching opener; the string is valid iff the stack ends empty.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*, Ch. 10 (Elementary Data Structures)** — stacks, queues, and linked lists formal treatment. See [`../../../books/`](../../../books/) if a local copy is present.
- **Sedgewick & Wayne — *Algorithms* (4th ed.), Ch. 1.3 (Bags, Queues, and Stacks)** — implementation and API design.
- **takeUforward A2Z DSA Course** — the paired video course for this step (linked below).
- **LeetCode Explore — Queue & Stack Card** — guided problems with editorials.

## 🔗 Official Problem Sources

- [takeUforward — Striver A2Z DSA Sheet (Step 9: Stack and Queues)](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the source step for this package.
- [LeetCode — Stack tag](https://leetcode.com/tag/stack/) — all stack problems.
- [LeetCode — Queue tag](https://leetcode.com/tag/queue/) — all queue problems.
- [LeetCode — Monotonic Stack tag](https://leetcode.com/tag/monotonic-stack/) — the core pattern of this step.
- [LeetCode — Monotonic Queue tag](https://leetcode.com/tag/monotonic-queue/) — sliding-window family.
- [LeetCode Explore — Queue & Stack](https://leetcode.com/explore/learn/card/queue-stack/) — official study card.
