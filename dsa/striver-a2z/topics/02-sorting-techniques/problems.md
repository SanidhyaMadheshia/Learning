# Learn Important Sorting Techniques — Problems (by Pattern)

> **Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are **grouped by pattern (sub-step)** exactly as in the Striver A2Z data. Every problem includes an intuition, a worked example, and a memorable analogy. 7 problems total.

---

## Sorting-I — Simple Quadratic Sorts

### Selection Sort  🟢 Easy

**Links:** [Article](https://takeuforward.org/sorting/selection-sort-algorithm/) · 🎥 [YouTube](https://youtu.be/HGk_ypEuS24?t=167)

**Intuition / Approach:** For every position from left to right, scan the unsorted suffix to find the minimum element and swap it into place. After the `i`-th pass the prefix `[0..i]` holds the `i+1` smallest elements in final order. It always does `O(n²)` comparisons regardless of input.

**Example:** `[64, 25, 12, 22, 11]`
- Pass 0: min of whole array is `11` → swap with `64` → `[11, 25, 12, 22, 64]`
- Pass 1: min of `[25,12,22,64]` is `12` → swap with `25` → `[11, 12, 25, 22, 64]`
- Pass 2: min of `[25,22,64]` is `22` → swap → `[11, 12, 22, 25, 64]`
- Pass 3: min is `25`, already placed → `[11, 12, 22, 25, 64]` ✅

**Analogy:** Picking the *shortest kid* from a line-up and moving them to the front, then repeating with everyone left — you always hunt for the single smallest each round.

**Complexity:** O(n²) time, O(1) space, unstable.

---

### Bubble Sort  🟢 Easy

**Links:** [Article](https://takeuforward.org/data-structure/bubble-sort-algorithm/) · 🎥 [YouTube](https://youtu.be/HGk_ypEuS24?t=1061)

**Intuition / Approach:** Repeatedly walk the array comparing adjacent pairs and swapping any that are out of order. Each full pass "bubbles" the current largest element to the end. If a pass performs no swaps, the array is already sorted and you can stop early (adaptive, `O(n)` best case).

**Example:** `[5, 1, 4, 2, 8]`
- Pass 1: (5,1)→swap, (5,4)→swap, (5,2)→swap, (5,8)→ok ⇒ `[1,4,2,5,8]`
- Pass 2: (1,4)ok, (4,2)→swap, (4,5)ok ⇒ `[1,2,4,5,8]`
- Pass 3: no swaps ⇒ stop. Output `[1,2,4,5,8]` ✅

**Analogy:** Lighter air bubbles in water always float up past heavier ones — each sweep lets the biggest "bubble" rise to the top (end) of the array.

**Complexity:** O(n²) worst/avg, O(n) best, O(1) space, stable.

---

### Insertion Sorting  🟢 Easy

**Links:** [Article](https://takeuforward.org/data-structure/insertion-sort-algorithm/) · 🎥 [YouTube](https://youtu.be/HGk_ypEuS24?t=1900)

**Intuition / Approach:** Grow a sorted prefix one element at a time. Take the next element (`key`), shift all larger elements of the sorted prefix one slot right, and drop `key` into the opened gap. Extremely fast on nearly-sorted data.

**Example:** `[12, 11, 13, 5, 6]`
- key=11: shift 12 → `[11, 12, 13, 5, 6]`
- key=13: no shift → `[11, 12, 13, 5, 6]`
- key=5: shift 13,12,11 → `[5, 11, 12, 13, 6]`
- key=6: shift 13,12,11 → `[5, 6, 11, 12, 13]` ✅

**Analogy:** Sorting a hand of playing cards — you pick up each new card and slide it into the correct spot among the cards you're already holding.

**Complexity:** O(n²) worst/avg, O(n) best, O(1) space, stable, adaptive.

---

## Sorting-II — Divide & Conquer + Recursive Sorts

### Merge Sorting  🟡 Medium

**Links:** [Article](https://takeuforward.org/data-structure/merge-sort-algorithm/) · 🎥 [YouTube](https://youtu.be/ogjf7ORKfd8)

**Intuition / Approach:** Divide the array into halves recursively until single elements remain, then merge sorted halves back together using a temp buffer. The merge step compares fronts of both halves and appends the smaller (`<=` for stability). Guaranteed `O(n log n)` in all cases.

**Example:** `[38, 27, 43, 3]`
- Split → `[38,27]` and `[43,3]`
- Sort halves → `[27,38]` and `[3,43]`
- Merge: compare 27 vs 3 → 3; 27 vs 43 → 27; 38 vs 43 → 38; then 43 ⇒ `[3, 27, 38, 43]` ✅

**Analogy:** Merging two already-sorted stacks of graded exam papers — you repeatedly take the lower-numbered sheet off the top of whichever stack, forming one perfectly ordered pile.

**Complexity:** O(n log n) all cases, O(n) space, stable.

---

### Recursive Bubble Sort  🟢 Easy

**Links:** [Article](https://takeuforward.org/arrays/recursive-bubble-sort-algorithm/)

**Intuition / Approach:** Same as bubble sort, but the outer loop becomes recursion. One pass bubbles the max to the end of the current range `[0..n)`, then you recurse on the smaller range `[0..n-1)`. Base case is `n == 1`. A no-swap pass short-circuits (adaptive).

**Example:** `[4, 3, 2, 1]`, call `recBubble(a, 4)`
- Pass over size 4: → `[3,2,1,4]` (4 fixed)
- `recBubble(a,3)`: → `[2,1,3,4]`
- `recBubble(a,2)`: → `[1,2,3,4]`
- `recBubble(a,1)`: base case ⇒ `[1,2,3,4]` ✅

**Analogy:** Like clearing the heaviest rock from a riverbed each dive, then diving again into a slightly smaller stretch — each recursive call handles one fewer element.

**Complexity:** O(n²) worst/avg, O(n) best, O(n) recursion-stack space, stable.

---

### Recursive Insertion Sort  🟢 Easy

**Links:** [Article](https://takeuforward.org/arrays/recursive-insertion-sort-algorithm/)

**Intuition / Approach:** Recursive re-formulation of insertion sort. To sort the prefix of length `i+1`, first recursively ensure `[0..i)` is sorted, then insert `a[i]` into its correct place by shifting larger elements right. Base case: prefix of size 1 (index 0) is trivially sorted.

**Example:** `[3, 1, 2]`, sort via increasing index
- i=1: insert 1 into `[3]` → `[1, 3, 2]`
- i=2: insert 2 into `[1,3]` → shift 3 → `[1, 2, 3]` ✅

**Analogy:** Building a sorted bookshelf: assume the first `i` books are already ordered, then take the next book and slide it into its exact alphabetical slot — recursion just tracks "how far along the shelf" you are.

**Complexity:** O(n²) worst/avg, O(n) best, O(n) recursion-stack space, stable.

---

### Quick Sorting  🟢 Easy

**Links:** [Article](https://takeuforward.org/data-structure/quick-sort-algorithm/) · 🎥 [YouTube](https://youtu.be/WIrA4YexLRQ)

**Intuition / Approach:** Choose a pivot, then **partition** the array so everything smaller sits left and everything larger sits right, placing the pivot at its final index. Recurse on the two sides. No merge step. Average `O(n log n)`; worst `O(n²)` on sorted input with a poor pivot — mitigated with randomised / median-of-three pivots.

**Example:** `[10, 80, 30, 90, 40]`, pivot = 10 (first)
- Partition around 10: 10 is smallest → pivot lands at index 0 → `[10 | 80,30,90,40]`
- Recurse right `[80,30,90,40]`, pivot 80 → smaller {30,40}, larger {90} → `[30,40,80,90]`
- Combine ⇒ `[10, 30, 40, 80, 90]` ✅

**Analogy:** Splitting a class by a chosen "reference" height — shorter students shuffle to one side of the room, taller to the other, the reference stands exactly where they belong, then you repeat within each side.

**Complexity:** O(n log n) avg, O(n²) worst, O(log n) avg stack space, in-place, unstable.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|------------|---------|---------------|
| 1 | Selection Sort | 🟢 Easy | Sorting-I | [Article](https://takeuforward.org/sorting/selection-sort-algorithm/) |
| 2 | Bubble Sort | 🟢 Easy | Sorting-I | [Article](https://takeuforward.org/data-structure/bubble-sort-algorithm/) |
| 3 | Insertion Sorting | 🟢 Easy | Sorting-I | [Article](https://takeuforward.org/data-structure/insertion-sort-algorithm/) |
| 4 | Merge Sorting | 🟡 Medium | Sorting-II | [Article](https://takeuforward.org/data-structure/merge-sort-algorithm/) |
| 5 | Recursive Bubble Sort | 🟢 Easy | Sorting-II | [Article](https://takeuforward.org/arrays/recursive-bubble-sort-algorithm/) |
| 6 | Recursive Insertion Sort | 🟢 Easy | Sorting-II | [Article](https://takeuforward.org/arrays/recursive-insertion-sort-algorithm/) |
| 7 | Quick Sorting | 🟢 Easy | Sorting-II | [Article](https://takeuforward.org/data-structure/quick-sort-algorithm/) |
