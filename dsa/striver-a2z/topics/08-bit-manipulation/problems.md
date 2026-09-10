# Bit Manipulation [Concepts & Problems] — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems (by Pattern)](./problems.md) · [Resources & References](./resources.md)

> Problems are **grouped by pattern** (the data's sub-steps). Every problem appears exactly once, with intuition, a worked example, and a memory analogy.

---

## Learn Bit Manipulation

### Introduction to Bits and Tricks  🟢
**Links:** [Article](https://takeuforward.org/data-structure/introduction-to-bit-manipulation-theory) · 🎥 [YouTube](https://youtu.be/qQd-ViW7bfk?si=QtdNaRhHmZb08Mr8)

**Intuition / Approach:** Understand that an integer is a sum of powers of two and that each of the six operators (`& | ^ ~ << >>`) acts bit-by-bit. Master the four core mask operations — test `(x>>i)&1`, set `x|(1<<i)`, clear `x&~(1<<i)`, toggle `x^(1<<i)` — and the shift identities `x<<k = x·2^k`, `x>>k = x/2^k`.

**Example:** `x = 13 = 1101₂`. Test bit 1 → `(13>>1)&1 = 0`. Set bit 1 → `13 | (1<<1) = 1111₂ = 15`. Clear bit 0 → `13 & ~1 = 1100₂ = 12`.

**Analogy:** Think of a bit as a **row of light switches**; each switch controls a lamp of wattage `2^i`. AND/OR/XOR are just wiring rules for flipping the switches.

---

### Check if the i-th bit is Set or Not  🟢
**Links:** [Article](https://takeuforward.org/data-structure/check-if-the-i-th-bit-is-set-or-not) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** Shift the number right by `i` so the target bit lands at position 0, then mask with `1`: `(x >> i) & 1`. Equivalently, AND with `(1 << i)` and check non-zero. `O(1)`.

**Example:** `x = 5 = 101₂`, `i = 2` → `(5 >> 2) & 1 = 1` → bit is set.

**Analogy:** Like **sliding a specific book to the front of a shelf** so you only have to look at one spot to see if it's there.

---

### Check if a Number is Odd or Not  🟢
**Links:** [Article](https://takeuforward.org/data-structure/check-if-a-number-is-odd-or-not) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** The parity of a number lives entirely in bit 0 (worth `2^0 = 1`). If bit 0 is set the number is odd. So `x & 1` is 1 for odd, 0 for even — no modulo needed.

**Example:** `7 = 111₂` → `7 & 1 = 1` → odd. `10 = 1010₂` → `10 & 1 = 0` → even.

**Analogy:** The **ones digit in binary is the "odd/even coin"** — heads (1) means odd, tails (0) means even; the rest of the bits are all even amounts.

---

### Check if a Number is Power of 2 or Not  🟢
**Links:** [LeetCode](https://leetcode.com/problems/power-of-two/) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** A power of two has exactly **one** set bit. Subtracting 1 flips that bit to 0 and turns all lower bits to 1, so `x & (x-1) == 0`. Guard with `x > 0` to reject 0 and negatives.

**Example:** `8 = 1000₂`, `8-1 = 0111₂`, `8 & 7 = 0` → power of two. `6 = 110₂`, `6 & 5 = 100₂ ≠ 0` → not.

**Analogy:** A power of two is a **lone tower**: knock the base out (`-1`) and the whole tower collapses to rubble that shares no floor with the original.

---

### Count the Number of Set Bits  🟢
**Links:** [Article](https://takeuforward.org/data-structure/count-the-number-of-set-bits) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** Brian Kernighan's trick: `n & (n-1)` removes the lowest set bit. Repeat until `n == 0`, counting iterations — the loop runs exactly `popcount(n)` times instead of 32. `O(#set bits)`.

**Example:** `n = 13 = 1101₂` → `13&12=1100` (c=1) → `12&11=1000` (c=2) → `8&7=0` (c=3). Answer 3.

**Analogy:** Like **plucking petals off a flower one at a time** — each pluck removes exactly one petal, so counts equal petals, not the whole stem length.

---

### Set/Unset the rightmost unset bit  🟢
**Links:** [Article](https://takeuforward.org/data-structure/set-the-rightmost-bit) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** Adding 1 to `x` turns its trailing block of 1s into 0s and sets the next-higher 0 — i.e. the rightmost **unset** bit. So `x | (x + 1)` sets that rightmost unset bit. (If all bits are already set, the value is unchanged after masking to width.)

**Example:** `x = 11 = 1011₂`. Rightmost unset bit is position 2. `x+1 = 1100₂`, `x | (x+1) = 1111₂ = 15`.

**Analogy:** Filling the **first empty parking spot from the right** — you scan from the near end and drop the car in the first open slot.

---

### Swap Two Numbers  🟢
**Links:** [Article](https://takeuforward.org/data-structure/swap-two-numbers) · 🎥 [YouTube](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV)

**Intuition / Approach:** Using XOR's self-inverse property you can swap without a temporary: `a ^= b; b ^= a; a ^= b;`. After step 1 `a` holds `a^b`; step 2 makes `b = a^b^b = a`; step 3 makes `a = a^b^a = b`.

**Example:** `a=5(101), b=3(011)` → `a=110` → `b=110^011=101=5` → `a=110^101=011=3`. Now `a=3, b=5`.

**Analogy:** Two people **swapping seats through a revolving door** — no third empty chair is ever needed; the door does the shuffling.

---

### Divide two numbers without multiplication and division  🟡
**Links:** [LeetCode](https://leetcode.com/problems/divide-two-integers/) · 🎥 [YouTube](https://youtu.be/pBD4B1tzgVc?si=G9c5pEE-RrzeU6sz)

**Intuition / Approach:** Long division in binary: from the highest bit down, if `divisor << k` fits into the remaining dividend, subtract it and add `1 << k` to the quotient. Work in `long long` on absolute values, apply the sign at the end, and special-case `INT_MIN / -1 → INT_MAX`.

**Example:** `22 / 3`. `3<<2=12 ≤ 22` → sub, q+=4, rem=10. `3<<1=6 ≤ 10` → sub, q+=2, rem=4. `3<<0=3 ≤ 4` → sub, q+=1, rem=1. Quotient = 7.

**Analogy:** Paying a bill with the **largest denomination bills first** (16, 8, 4, 2, 1) — you subtract the biggest note that still fits, then move to smaller ones.

**Complexity:** `O(log n)` time, `O(1)` space.

---

## Interview Problems

### Minimum Bit Flips to Convert Number  🟡
**Links:** [LeetCode](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/) · 🎥 [YouTube](https://youtu.be/OOdrmcfZXd8?si=rnkRVz1UiVBKWC69)

**Intuition / Approach:** A flip changes one bit. The number of positions where `a` and `b` differ is exactly `popcount(a ^ b)`, because XOR marks differing bits as 1. Count those set bits.

**Example:** `start=10=1010₂`, `goal=7=0111₂`. `10^7 = 1101₂`, popcount = 3 → 3 flips.

**Analogy:** Comparing two **rows of light switches**; the number of switches you must toggle equals the number of positions where the two rows disagree.

**Complexity:** `O(#differing bits)` time, `O(1)` space.

---

### Single Number - I  🟡
**Links:** [LeetCode](https://leetcode.com/problems/single-number/) · 🎥 [YouTube](https://youtu.be/bYWLJb3vCWY?t=1369)

**Intuition / Approach:** Every element appears twice except one. XOR all elements: equal values cancel (`a^a=0`), leaving the unique element (`a^0=a`). Order doesn't matter thanks to commutativity/associativity. `O(n)` time, `O(1)` space.

**Example:** `[4,1,2,1,2]` → `4^1^2^1^2 = 4^(1^1)^(2^2) = 4^0^0 = 4`.

**Analogy:** At a **buddy check where everyone has a twin**, XOR pairs them off; the one camper without a twin is left standing.

---

### Power Set Bit Manipulation  🟡
**Links:** [LeetCode](https://leetcode.com/problems/subsets/) · 🎥 [YouTube](https://youtu.be/LqKaUv1G3_I?si=UXU_T5OsHiokPRvP)

**Intuition / Approach:** For `n` elements there are `2^n` subsets. Let a mask range over `[0, 2^n)`; include element `j` when bit `j` of the mask is set. Iterate all masks to enumerate every subset. `O(n · 2^n)`.

**Example:** `s=[1,2,3]`. mask=0→{}, 1(001)→{1}, 2(010)→{2}, 3(011)→{1,2}, 4(100)→{3}, ... 7(111)→{1,2,3}.

**Analogy:** A **buffet with n dishes** — every possible plate is a yes/no choice per dish, and the binary counter enumerates all plates from empty to full.

**Complexity:** `O(n · 2^n)` time, `O(2^n)` output space.

---

### XOR of numbers in a given range  🟡
**Links:** [Article](https://takeuforward.org/data-structure/find-xor-of-numbers-from-l-to-r) · 🎥 [YouTube](https://youtu.be/WqGb7159h7Q?si=uGUEbNUUaIN_6Vvr)

**Intuition / Approach:** Define `f(n) = XOR of 0..n`, which cycles with `n % 4`: `{n, 1, n+1, 0}`. Then `XOR(L..R) = f(R) ^ f(L-1)` because the prefix `0..L-1` cancels itself out. `O(1)`.

**Example:** `L=4, R=7`. `f(7)=0` (7%4=3), `f(3)=0` (3%4=3) → wait, use `f(L-1)=f(3)=0`, so `4^5^6^7 = f(7)^f(3) = 0^0 = 0`. Check: `4^5=1, ^6=7, ^7=0`. ✓

**Analogy:** A **repeating traffic-light cycle** — you don't watch every second; you just read where you are in the 4-phase pattern.

**Complexity:** `O(1)` time and space.

---

### Single Number - III  🟡
**Links:** [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) · 🎥 [YouTube](https://youtu.be/UA5JnV1J2sI?si=VFBRJyb3boZvx_r1)

**Intuition / Approach:** Two elements are unique; the rest appear twice. XOR all → `xy = x ^ y`. Since `x ≠ y`, `xy` has at least one set bit; take the lowest with `d = xy & (-xy)`. That bit differs between `x` and `y`, so partition the array by it and XOR each group separately to recover `x` and `y`.

**Example:** `[1,2,1,3,2,5]` → `xy = 3^5 = 6 = 110₂`. `d = 6 & -6 = 2`. Group with bit1 set: `2,3,2` → `3`; group without: `1,1,5` → `5`. Answer `{3,5}`.

**Analogy:** Two mismatched socks in a pile of pairs — first XOR removes all matched pairs, then a **distinguishing feature** (a differing bit) lets you sort the two odd socks into separate bins.

**Complexity:** `O(n)` time, `O(1)` space.

---

## Advanced Maths

### Print Prime Factors of a Number  🔴
**Links:** [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) · 🎥 [YouTube](https://youtu.be/LT7XhVdeRyg?si=6HkjQokJRPTFai21)

**Intuition / Approach:** Trial-divide by each `i` from 2 while `i·i ≤ n`. Whenever `i | n`, record `i` and keep dividing it out. After the loop, if `n > 1` it is a prime factor itself (a leftover large prime). `O(√n)`.

**Example:** `n = 60`. `2` divides → 30 → 15, record 2. `3` divides 15 → 5, record 3. loop ends (`4·4>5`); `n=5>1` → record 5. Factors: 2, 3, 5.

**Analogy:** **Peeling an onion from the smallest layer out** — you strip each smallest prime layer completely before moving to the next larger one.

**Complexity:** `O(√n)` time, `O(log n)` factors.

---

### Divisors of a Number  🟢
**Links:** [Article](https://takeuforward.org/data-structure/print-all-divisors-of-a-given-number/) · 🎥 [YouTube](https://youtu.be/1xNbjMdbjug?t=1580)

**Intuition / Approach:** Divisors come in pairs `(i, n/i)` straddling `√n`. Iterate `i` from 1 to `√n`; on each hit push `i` and (if different) `n/i`. This finds all divisors in `O(√n)` instead of `O(n)`.

**Example:** `n = 36`. `1&36, 2&18, 3&12, 4&9, 6&6`. Divisors: 1,2,3,4,6,9,12,18,36.

**Analogy:** Arranging `n` tiles into **all possible rectangles** — each rectangle `i × (n/i)` gives a divisor pair, and you only need to try widths up to the square.

**Complexity:** `O(√n)` time.

---

### Count primes in range L to R  🔴
**Links:** [LeetCode](https://leetcode.com/problems/count-primes/) · 🎥 [YouTube](https://youtu.be/g5Fuxn_AvSk?si=fv6Q-Po7wrMW0a5n)

**Intuition / Approach:** Build a Sieve of Eratosthenes up to `R`, marking multiples of each prime from `p*p`. Then count primes in `[L, R]` (or use a prefix-count array for many queries: `cnt[R] - cnt[L-1]`). `O(R log log R)`.

**Example:** `L=10, R=20`. Sieve marks composites; primes in range are 11, 13, 17, 19 → count = 4.

**Analogy:** A **stadium roll-call** where you cross off every seat that's a multiple of an announced number; the seats never crossed are the primes, and you tally the ones in your section.

**Complexity:** `O(R log log R)` build, `O(R)` space.

---

### Prime factorisation of a Number  🔴
**Links:** [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) · 🎥 [YouTube](https://youtu.be/LT7XhVdeRyg?si=6HkjQokJRPTFai21)

**Intuition / Approach:** For a single number, `O(√n)` trial division suffices. For many queries, precompute a **Smallest Prime Factor (SPF)** sieve: `spf[x]` = smallest prime dividing `x`. Then factor any `x ≤ N` by repeatedly dividing by `spf[x]` in `O(log x)`.

**Example (SPF):** `n=84`. `spf[84]=2`→42, `spf[42]=2`→21, `spf[21]=3`→7, `spf[7]=7`→1. Factors: 2², 3, 7.

**Analogy:** A **precomputed "who's the boss" chart** — you always ask the smallest prime in charge of the current number, divide, and repeat until you reach 1.

**Complexity:** SPF build `O(N log log N)`; per-number factorisation `O(log n)`.

---

### Pow(x,n)  🟡
**Links:** [LeetCode](https://leetcode.com/problems/powx-n/) · 🎥 [YouTube](https://youtu.be/l0YC3876qxg)

**Intuition / Approach:** Binary exponentiation: read `n`'s bits from LSB. Keep squaring the base (`x, x², x⁴, ...`); whenever the current bit is 1, multiply it into the result. Handle negative `n` by inverting `x` and negating `n`. `O(log n)`.

**Example:** `x=2, n=10 (1010₂)`. bits: 0→square(4), 1→res=4 square(16), 0→square(256), 1→res=4·256=1024. Answer 1024.

**Analogy:** Doubling a **folded paper**: each fold squares the thickness, and you only "keep" the layers whose bit is set — reaching huge powers in a handful of folds instead of one multiply at a time.

**Complexity:** `O(log n)` time, `O(1)` space.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---|---|---|---|
| 1 | Introduction to Bits and Tricks | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/introduction-to-bit-manipulation-theory) |
| 2 | Check if the i-th bit is Set or Not | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/check-if-the-i-th-bit-is-set-or-not) |
| 3 | Check if a Number is Odd or Not | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/check-if-a-number-is-odd-or-not) |
| 4 | Check if a Number is Power of 2 or Not | 🟢 Easy | Learn Bit Manipulation | [LeetCode](https://leetcode.com/problems/power-of-two/) |
| 5 | Count the Number of Set Bits | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/count-the-number-of-set-bits) |
| 6 | Set/Unset the rightmost unset bit | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/set-the-rightmost-bit) |
| 7 | Swap Two Numbers | 🟢 Easy | Learn Bit Manipulation | [Article](https://takeuforward.org/data-structure/swap-two-numbers) |
| 8 | Divide two numbers without mult/div | 🟡 Medium | Learn Bit Manipulation | [LeetCode](https://leetcode.com/problems/divide-two-integers/) |
| 9 | Minimum Bit Flips to Convert Number | 🟡 Medium | Interview Problems | [LeetCode](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/) |
| 10 | Single Number - I | 🟡 Medium | Interview Problems | [LeetCode](https://leetcode.com/problems/single-number/) |
| 11 | Power Set Bit Manipulation | 🟡 Medium | Interview Problems | [LeetCode](https://leetcode.com/problems/subsets/) |
| 12 | XOR of numbers in a given range | 🟡 Medium | Interview Problems | [Article](https://takeuforward.org/data-structure/find-xor-of-numbers-from-l-to-r) |
| 13 | Single Number - III | 🟡 Medium | Interview Problems | [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) |
| 14 | Print Prime Factors of a Number | 🔴 Hard | Advanced Maths | [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) |
| 15 | Divisors of a Number | 🟢 Easy | Advanced Maths | [Article](https://takeuforward.org/data-structure/print-all-divisors-of-a-given-number/) |
| 16 | Count primes in range L to R | 🔴 Hard | Advanced Maths | [LeetCode](https://leetcode.com/problems/count-primes/) |
| 17 | Prime factorisation of a Number | 🔴 Hard | Advanced Maths | [Article](https://takeuforward.org/data-structure/find-the-two-numbers-appearing-odd-number-of-times) |
| 18 | Pow(x,n) | 🟡 Medium | Advanced Maths | [LeetCode](https://leetcode.com/problems/powx-n/) |
