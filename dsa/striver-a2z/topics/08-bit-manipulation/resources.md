# Bit Manipulation [Concepts & Problems] — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems (by Pattern)](./problems.md) · [Resources & References](./resources.md)

---

## 📺 Videos & Playlists

- [Striver — Bit Manipulation Introduction & Tricks (takeUforward)](https://youtu.be/nttpF8kwgd4?si=x9o8PsYaA2XVZ9rV) — core bit ops: check/set/clear/toggle, count set bits, power of two, swap.
- [Striver — Introduction to Bits and Tricks](https://youtu.be/qQd-ViW7bfk?si=QtdNaRhHmZb08Mr8) — foundational bit representation and operators.
- [Striver — Divide Two Integers without `*` `/` `%`](https://youtu.be/pBD4B1tzgVc?si=G9c5pEE-RrzeU6sz) — binary long division with sign & overflow handling.
- [Striver — Minimum Bit Flips / Count Bits to Flip](https://youtu.be/OOdrmcfZXd8?si=rnkRVz1UiVBKWC69) — `popcount(a ^ b)` intuition.
- [Striver — Single Number I (XOR)](https://youtu.be/bYWLJb3vCWY?t=1369) — cancel-the-pairs XOR pattern.
- [Striver — Power Set using Bit Manipulation](https://youtu.be/LqKaUv1G3_I?si=UXU_T5OsHiokPRvP) — mask enumeration of all subsets.
- [Striver — XOR of numbers from L to R](https://youtu.be/WqGb7159h7Q?si=uGUEbNUUaIN_6Vvr) — the `n % 4` prefix-XOR trick.
- [Striver — Single Number III (two unique numbers)](https://youtu.be/UA5JnV1J2sI?si=VFBRJyb3boZvx_r1) — split by a differing bit.
- [Striver — Prime Factorisation / Number Theory](https://youtu.be/LT7XhVdeRyg?si=6HkjQokJRPTFai21) — trial division & SPF.
- [Striver — All Divisors of a Number](https://youtu.be/1xNbjMdbjug?t=1580) — `O(√n)` divisor pairs.
- [Striver — Sieve of Eratosthenes / Count Primes](https://youtu.be/g5Fuxn_AvSk?si=fv6Q-Po7wrMW0a5n) — building and querying the sieve.
- [Striver — Pow(x, n) Binary Exponentiation](https://youtu.be/l0YC3876qxg) — square-and-multiply.

---

## 📝 Articles & Tutorials

- [takeUforward — Introduction to Bit Manipulation (theory)](https://takeuforward.org/data-structure/introduction-to-bit-manipulation-theory) — Striver's written companion to the intro video.
- [cp-algorithms — Bit Manipulation](https://cp-algorithms.com/algebra/bit-manipulation.html) — rigorous reference on bit tricks and built-ins.
- [cp-algorithms — Binary Exponentiation](https://cp-algorithms.com/algebra/binary-exp.html) — the canonical fast-power writeup with proofs and mod applications.
- [cp-algorithms — Linear Sieve](https://cp-algorithms.com/algebra/prime-sieve-linear.html) — `O(N)` sieve and SPF computation.
- [GeeksforGeeks — Bits Manipulation (Important Tactics)](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/) — XOR 1..n, power-of-two, MSB, swap, and more.
- [GeeksforGeeks — Bitwise Hacks for Competitive Programming](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/) — set/clear/toggle/count hacks reference.
- [GeeksforGeeks — Bit Tricks for Competitive Programming](https://www.geeksforgeeks.org/competitive-programming/bit-tricks-competitive-programming/) — `x & (x-1)`, lowest set bit, and friends.
- [GeeksforGeeks — Bit Manipulation for Competitive Programming](https://www.geeksforgeeks.org/dsa/bit-manipulation-for-competitive-programming/) — operator-by-operator walkthrough.
- [GeeksforGeeks — Sieve of Eratosthenes](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) — classic sieve explanation and code.
- [GeeksforGeeks — Prime Factorization using Sieve (SPF)](https://www.geeksforgeeks.org/dsa/prime-factorization-using-sieve-olog-n-multiple-queries/) — `O(log n)` factorisation for many queries.
- [GeeksforGeeks — Binary Exponentiation](https://www.geeksforgeeks.org/competitive-programming/binary-exponentiation-for-competitive-programming/) — fast power with modular variants.
- [LeetCode Discuss — Bit Manipulation Guide and Tricks](https://leetcode.com/discuss/study-guide/2960396/Bit-Manipulation-Guide-and-Tricks) — curated tricks + problem list.
- [LeetCode Discuss — All Number Theory Topics (Basic to Advanced)](https://leetcode.com/discuss/study-guide/3687666/All-Number-Theory-Topics-or-Basic-to-Advance-Lavel) — GCD/LCM, divisors, sieve, binary exp code snippets.
- [freeCodeCamp — Binary Exponentiation Explained](https://freecodecamp.org/news/binary-exponentiation-algorithm-explained-with-examples) — beginner-friendly derivation with examples.

---

## 🧮 Visualizers & Tools

- [VisuAlgo — Number Theory (Sieve, GCD, etc.)](https://visualgo.net/en/) — interactive visualizations for sieve and number-theory algorithms.
- [USFCA — Data Structure & Algorithm Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html) — step-through visualizers for core algorithms.
- [Wikipedia — Exponentiation by Squaring](https://en.wikipedia.org/wiki/Exponentiation_by_squaring) — formal treatment and variants of binary exponentiation.
- Quick mental tool: use `__builtin_popcount(x)` / `__builtin_popcountll(x)` and `__builtin_ctz(x)` (count trailing zeros) in GCC/Clang for instant bit counts.

---

## ❓ Most-Asked Interview Questions

1. **How do you check if the i-th bit is set?** — `(x >> i) & 1`; equivalently `x & (1 << i)` is non-zero.
2. **Set, clear, and toggle a bit?** — Set `x | (1<<i)`, clear `x & ~(1<<i)`, toggle `x ^ (1<<i)`.
3. **Check if a number is a power of two?** — `x > 0 && (x & (x-1)) == 0`; a power of two has exactly one set bit.
4. **Count set bits efficiently?** — Brian Kernighan: `while(x){ x &= x-1; count++; }` runs `popcount` times, `O(#set bits)`.
5. **Fastest way to swap two integers without a temp?** — XOR swap: `a^=b; b^=a; a^=b;` (careful when both alias the same variable).
6. **Why does XOR find the single element among duplicates?** — `a^a=0` and `a^0=a`, so all pairs cancel and only the odd-count value survives.
7. **Find the two unique numbers (rest twice)?** — XOR all to get `x^y`, isolate a differing bit `d = xy & -xy`, partition by that bit, XOR each group.
8. **XOR of all numbers from 1..n in O(1)?** — Depends on `n % 4`: pattern `{n, 1, n+1, 0}`; range `[L,R]` = `f(R) ^ f(L-1)`.
9. **Generate the power set with bits?** — For `n` items iterate masks `0..2^n-1`; bit `j` selects item `j` — `O(n·2^n)`.
10. **Divide without `/`, `*`, `%`?** — Binary long division: subtract the largest `divisor<<k` that fits, add `1<<k` to the quotient; special-case `INT_MIN/-1`.
11. **Compute pow(x, n) in O(log n)?** — Binary exponentiation: square the base, multiply into result when the current exponent bit is 1; invert for negative `n`.
12. **How does the Sieve of Eratosthenes work and its complexity?** — Mark multiples of each prime from `p*p`; `O(N log log N)` time, `O(N)` space.
13. **How to factorise many numbers fast?** — Precompute a Smallest-Prime-Factor sieve, then divide by `spf[x]` repeatedly — `O(log x)` per number.
14. **Find all divisors of n efficiently?** — Iterate `i` to `√n`; each hit yields the pair `(i, n/i)` — `O(√n)`.
15. **Common bit-manipulation pitfalls?** — Operator precedence (`&` below `==`), signed shift overflow (`1<<31`), missing `x>0` in the power-of-two check, and `p*p` overflow in the sieve.

---

## 📚 Books & Courses

- **Hacker's Delight** by Henry S. Warren — the definitive bit-manipulation reference (counting bits, tricks, rounding to powers of two).
- **CLRS — Introduction to Algorithms**, Chapter 31 (Number-Theoretic Algorithms) — GCD, modular arithmetic, primality.
- **Competitive Programmer's Handbook** by Antti Laaksonen — chapters on bit manipulation and number theory.
- **The Art of Computer Programming, Vol. 4A** by Knuth — bitwise tricks and combinatorial subset generation.
- Local library cross-link (if present): [../../../books/](../../../books/).

---

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Course/Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2/) — the source sheet for this step.
- [LeetCode Tag — Bit Manipulation](https://leetcode.com/tag/bit-manipulation/) — all tagged problems.
- [LeetCode Tag — Math](https://leetcode.com/tag/math/) — number-theory problems (primes, pow, divisors).
- [LeetCode Study Plan — Programming Skills](https://leetcode.com/studyplan/programming-skills/) — includes bit and math practice.
- [LeetCode Discuss — Complete Bit Manipulation Problems and Resources Guide](https://leetcode.com/discuss/post/7359165/complete-bit-manipulation-problems-and-r-ozfb/) — problem list grouped by technique.
- Direct problems: [Power of Two](https://leetcode.com/problems/power-of-two/) · [Single Number](https://leetcode.com/problems/single-number/) · [Subsets](https://leetcode.com/problems/subsets/) · [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/) · [Minimum Bit Flips](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/) · [Count Primes](https://leetcode.com/problems/count-primes/) · [Pow(x, n)](https://leetcode.com/problems/powx-n/).
