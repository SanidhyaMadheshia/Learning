# Dynamic Programming — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by pattern (in data order). Every problem has an intuition, a worked example, and a memory analogy. 57 problems total.

---

## Introduction to DP

### Introduction to DP  🟢 Easy
**Links:** [Article](https://takeuforward.org/data-structure/dynamic-programming-introduction/) · 🎥 [YouTube](https://youtu.be/tyB0ztf0DNY)

**Intuition / Approach:** DP = recursion + storage. Identify overlapping sub-problems and optimal substructure, then either memoize (top-down) or tabulate (bottom-up), and finally space-optimize. Fibonacci is the canonical intro: `f(n)=f(n-1)+f(n-2)`.

**Example:** `fib(5)` naive recomputes `f(3)` twice, `f(2)` thrice. With a cache: `f(0)=0, f(1)=1 → 1,2,3,5`. Output `fib(5)=5` in O(n).

**Analogy:** Like keeping a filled-in answer key during an exam — once you solve a sub-question, you never redo it; you just look it up.

**Complexity:** O(n) time, O(1) space optimized.

---

## 1D DP

### Climbing stairs  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/climbing-stairs/) · 🎥 [YouTube](https://youtu.be/mLfjzJsN8us)

**Intuition / Approach:** To reach step `n` you came from step `n-1` (1 step) or `n-2` (2 steps), so `ways(n)=ways(n-1)+ways(n-2)` — literally Fibonacci. Base: `ways(0)=ways(1)=1`.

**Example:** `n=3`: ways(3)=ways(2)+ways(1)=2+1=3 → paths {1+1+1, 1+2, 2+1}. Output `3`.

**Analogy:** Climbing a staircase where you count routes — every landing's route-count is the sum of the two landings you could step from.

**Complexity:** O(n) time, O(1) space.

### Frog Jump  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-dp-3/) · 🎥 [YouTube](https://www.youtube.com/watch?v=EgG3jsGoPvQ)

**Intuition / Approach:** Frog on stair `i` can jump to `i+1` or `i+2` paying `|height[i]-height[j]|` energy. `dp[i]=min` energy to reach `i` = `min(dp[i-1]+|h[i]-h[i-1]|, dp[i-2]+|h[i]-h[i-2]|)`.

**Example:** heights `[10,20,30,10]`: dp0=0, dp1=10, dp2=min(10+10, 0+20)=20, dp3=min(20+20, 10+0)=10. Output `20` (path 0→2→3? recompute) → minimal total energy `20`.

**Analogy:** A tired frog choosing hops — each landing remembers the cheapest way it could have arrived so far.

**Complexity:** O(n) time, O(1) space optimized.

### Frog jump with K distances  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-with-k-distances-dp-4/) · 🎥 [YouTube](https://www.youtube.com/watch?v=Kmh3rhyEtB8)

**Intuition / Approach:** Generalize Frog Jump: the frog can jump up to `K` steps. `dp[i]=min over j in 1..K of dp[i-j]+|h[i]-h[i-j]|`. Inner loop over the K possible jumps.

**Example:** heights `[10,30,40,50,20]`, K=3: compute dp with up to 3-step jumps; the optimum reaches the last stair via the cheapest combination. Output = minimal total energy.

**Analogy:** The same frog now with a longer jump range — at each rock it scans the last K rocks and picks the cheapest launch pad.

**Complexity:** O(n·K) time, O(n) space.

### Maximum sum of non adjacent elements  🟡 Medium
**Links:** [LeetCode (House Robber)](https://leetcode.com/problems/house-robber/) · 🎥 [YouTube](https://www.youtube.com/watch?v=GrMBfJNk_NY)

**Intuition / Approach:** For each element choose **take** (`a[i]+dp[i-2]`) or **not-take** (`dp[i-1]`) and keep the max. Can't take two adjacent.

**Example:** `[2,1,4,9]`: dp0=2, dp1=max(2,1)=2, dp2=max(2, 4+2)=6, dp3=max(6, 9+2)=11. Output `11` (pick 2 and 9).

**Analogy:** Picking non-neighbouring fruits off a branch so you never grab two touching ones — maximize the harvest.

**Complexity:** O(n) time, O(1) space.

### House robber  🟡 Medium
**Links:** [LeetCode (House Robber II)](https://leetcode.com/problems/house-robber-ii/) · 🎥 [YouTube](https://www.youtube.com/watch?v=3WaxQMELSkw)

**Intuition / Approach:** Houses are in a **circle**, so first and last are adjacent. Run the linear non-adjacent max twice: once excluding the first house, once excluding the last, and take the max.

**Example:** `[2,3,2]`: exclude first → rob [3,2]→3; exclude last → rob [2,3]→3. Output `3` (can't rob both 2's since they're adjacent in the circle).

**Analogy:** Robbing houses on a cul-de-sac roundabout — since the first and last touch, you plan two separate routes and keep the richer haul.

**Complexity:** O(n) time, O(1) space.

---

## 2D/3D DP and DP on Grids

### Ninja's training  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/dynamic-programming-ninjas-training-dp-7/) · 🎥 [YouTube](https://www.youtube.com/watch?v=AE39gJYuRog)

**Intuition / Approach:** Each day pick one of 3 activities but not the same as yesterday. `dp[day][last]` = max points if yesterday's activity was `last`. Try each activity ≠ last, add its points, recurse to next day.

**Example:** points `[[1,2,5],[3,1,1],[3,3,3]]`: best = pick 5 (day0), then 3 (day1, ≠ last), then 3 (day2) → but must alternate; optimal total works out to `11`.

**Analogy:** A ninja training week where doing the same drill two days running is banned — plan the schedule for max skill gain.

**Complexity:** O(n·4·3)=O(n) time, O(4) space optimized.

### Grid Unique Paths : DP on Grids (DP8)  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/unique-paths/) · 🎥 [YouTube](https://www.youtube.com/watch?v=sdE0A2Oxofw)

**Intuition / Approach:** Move only right or down from top-left to bottom-right. `dp[i][j]=dp[i-1][j]+dp[i][j-1]`. First row/col = 1 (only one way). (Also solvable with a single combinatorics formula C(m+n-2, m-1).)

**Example:** 3×3 grid: dp fills to 6 at bottom-right. Output `6` paths.

**Analogy:** A courier on a city grid who can only head east or south — counting distinct delivery routes to the far corner.

**Complexity:** O(m·n) time, O(n) space optimized.

### Unique paths II  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/unique-paths-ii/) · 🎥 [YouTube](https://www.youtube.com/watch?v=TmhpgXScLyY)

**Intuition / Approach:** Same as Unique Paths but some cells are obstacles. If `grid[i][j]==1` (obstacle) set `dp[i][j]=0`; else `dp[i-1][j]+dp[i][j-1]`.

**Example:** grid `[[0,0,0],[0,1,0],[0,0,0]]`: the center blocks routes → Output `2` unique paths.

**Analogy:** Same courier, but now roadblocks close some intersections — routes through a blocked corner count as zero.

**Complexity:** O(m·n) time, O(n) space optimized.

### Minimum Falling Path Sum  🟡 Medium
**Links:** [LeetCode (Minimum Path Sum)](https://leetcode.com/problems/minimum-path-sum/) · 🎥 [YouTube](https://youtu.be/_rgTlyky1uQ)

**Intuition / Approach:** Minimize sum along a top-left→bottom-right path (right/down moves). `dp[i][j]=grid[i][j]+min(dp[i-1][j], dp[i][j-1])`. (Falling-path variant allows the three cells above.)

**Example:** grid `[[1,3,1],[1,5,1],[4,2,1]]`: min path 1→3→1→1→1 = `7`. Output `7`.

**Analogy:** Hiking downhill on a cost-grid where every cell charges a toll — find the cheapest descent.

**Complexity:** O(m·n) time, O(n) space optimized.

### Triangle  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/triangle/) · 🎥 [YouTube](https://www.youtube.com/watch?v=SrP-PiLSYC0)

**Intuition / Approach:** Fixed start at apex, move to adjacent cell below (`i+1,j` or `i+1,j+1`). Bottom-up: `dp[i][j]=t[i][j]+min(dp[i+1][j], dp[i+1][j+1])`, answer at apex.

**Example:** `[[2],[3,4],[6,5,7],[4,1,8,3]]`: min path 2→3→5→1 = `11`. Output `11`.

**Analogy:** Rolling a marble down a triangular peg board, always going to a touching lower peg — minimize the total peg cost.

**Complexity:** O(n²) time, O(n) space optimized.

### Ninja and his Friends  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/3-d-dp-ninja-and-his-friends-dp-13/) · 🎥 [YouTube](https://www.youtube.com/watch?v=QGfn7JeXK54)

**Intuition / Approach:** Two players start at top corners and move down collecting chocolates; if on same cell count once. 3D state `dp[i][j1][j2]` — both move simultaneously, each has 3 column choices → 9 combinations per step.

**Example:** grid of chocolates; two robots descend, each row both pick their cell (shared cell counted once) → maximize combined chocolates. Output = max total.

**Analogy:** Two friends racing down a chocolate-tiled hill, each grabbing candy in their lane — coordinate their columns to maximize the shared haul.

**Complexity:** O(n·m·m·9) time, O(m·m) space optimized.

---

## DP on Subsequences

### Subset sum equal to target (DP- 14)  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/subset-sum-equal-to-target-dp-14/) · 🎥 [YouTube](https://www.youtube.com/watch?v=fWX9xDmIzRI)

**Intuition / Approach:** Take/not-take each element toward a target sum. `dp[i][t]` = can we make `t` using items `0..i`? `notTake=dp[i-1][t]`, `take=dp[i-1][t-a[i]]`. OR them.

**Example:** `[1,2,3,4]`, target 6: {2,4} or {1,2,3} → Output `true`.

**Analogy:** Filling a jar to an exact weight using given stones — you either drop a stone in or leave it out.

**Complexity:** O(n·target) time, O(target) space.

### Partition equal subset sum  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/partition-equal-subset-sum/) · 🎥 [YouTube](https://www.youtube.com/watch?v=7win3dcgo3k)

**Intuition / Approach:** If total sum is odd → impossible. Otherwise check if a subset sums to `total/2` (reduces to subset-sum).

**Example:** `[1,5,11,5]`: total=22, target=11 → {11} or {1,5,5}. Output `true`.

**Analogy:** Splitting a bag of coins into two piles of equal value — you only need to find one pile worth half.

**Complexity:** O(n·sum/2) time, O(sum/2) space.

### Partition a set into two subsets with minimum absolute sum difference  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/) · 🎥 [YouTube](https://www.youtube.com/watch?v=GS_OqZb2CWc)

**Intuition / Approach:** Compute all achievable subset sums `s1 ≤ total/2` (subset-sum DP last row). For each feasible `s1`, other subset = `total-s1`; minimize `|total-2·s1|`.

**Example:** `[1,6,11,5]`: total=23; best s1=11 → diff `|23-22|=1`. Output `1`.

**Analogy:** Dividing teammates into two tug-of-war teams as evenly matched as possible — search all reachable team weights and pick the fairest split.

**Complexity:** O(n·sum) time, O(sum) space.

### Count subsets with sum K  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/count-subsets-with-sum-k-dp-17/) · 🎥 [YouTube](https://www.youtube.com/watch?v=ZHyb-A2Mte4)

**Intuition / Approach:** Same take/not-take but **count** instead of feasibility: `dp[i][t]=dp[i-1][t] + dp[i-1][t-a[i]]`. Careful with zeros (they double counts).

**Example:** `[1,2,2,3]`, K=3: subsets {1,2},{1,2},{3} → Output `3`.

**Analogy:** Counting every distinct way to reach an exact bill total using given coins from your pocket, treating each coin as unique.

**Complexity:** O(n·K) time, O(K) space.

### Count partitions with given difference  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/count-partitions-with-given-difference-dp-18/) · 🎥 [YouTube](https://www.youtube.com/watch?v=zoilQD1kYSg)

**Intuition / Approach:** Want `S1-S2=D` with `S1+S2=total`, so `S1=(total+D)/2`. Count subsets summing to that value (must be non-negative even). Reduces to Count-subsets-with-sum-K.

**Example:** `[1,1,2,3]`, D=1: total=7, S1=(7+1)/2=4 → count subsets summing to 4 = `3`.

**Analogy:** Splitting savings into two accounts with a required gap — solve for the target account balance, then count the ways to fund it.

**Complexity:** O(n·sum) time, O(sum) space.

### Assign Cookies  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/assign-cookies/) · 🎥 [YouTube](https://youtu.be/DIX2p7vb9co?si=GofAIDimue-Av0Fi)

**Intuition / Approach:** Greedy (grouped here for completeness): sort greed and cookie sizes, give the smallest sufficient cookie to the least-greedy child using two pointers.

**Example:** greed `[1,2,3]`, cookies `[1,1]`: child(1) gets cookie(1); no cookie ≥2 → Output `1` content child.

**Analogy:** Handing out cookies to kids where each kid needs a minimum size — satisfy the easy-to-please kids first to make the most children happy.

**Complexity:** O(n log n + m log m) time, O(1) extra space.

### Minimum Coins (DP - 20)  🔴 Hard
**Links:** [LeetCode (Coin Change)](https://leetcode.com/problems/coin-change/) · 🎥 [YouTube](https://www.youtube.com/watch?v=myPeWb3Y68A)

**Intuition / Approach:** Unbounded knapsack minimizing count. `dp[i][t]=min(notTake=dp[i-1][t], take=1+dp[i][t-coin[i]])` (stay on `i` because unlimited). Base: amount 0 → 0 coins; unreachable → INF.

**Example:** coins `[1,2,5]`, amount 11: 5+5+1 → Output `3`.

**Analogy:** Making exact change with the fewest coins possible — reuse any denomination as many times as you like.

**Complexity:** O(n·amount) time, O(amount) space.

### Target sum  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/target-sum/) · 🎥 [YouTube](https://www.youtube.com/watch?v=b3GD8263-PQ)

**Intuition / Approach:** Assign + or − to each number to reach target. Equivalent to counting subsets with a given difference (positives set S1 with `S1=(total+target)/2`). Reduces to count-partitions-with-difference.

**Example:** `[1,1,1,1,1]`, target=3: choose signs → Output `5` ways.

**Analogy:** Flipping each number to plus or minus like light switches to hit an exact voltage — count the switch combinations.

**Complexity:** O(n·sum) time, O(sum) space.

### Coin Change 2 (DP - 22)  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/coin-change-2/) · 🎥 [YouTube](https://www.youtube.com/watch?v=HgyouUi11zk)

**Intuition / Approach:** Count the number of ways to make an amount with unlimited coins. `dp[i][t]=dp[i-1][t] + dp[i][t-coin[i]]` (take stays on `i`). Order-independent counting.

**Example:** coins `[1,2,5]`, amount 5: {5},{2,2,1},{2,1,1,1},{1×5} → Output `4`.

**Analogy:** Counting all distinct ways to pay a price with unlimited coins of each type, where the order of handing coins doesn't matter.

**Complexity:** O(n·amount) time, O(amount) space.

### Unbounded knapsack  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/unbounded-knapsack-dp-23/) · 🎥 [YouTube](https://youtu.be/OgvOZ6OrJoY)

**Intuition / Approach:** Maximize value with capacity `W`, items reusable. `dp[i][w]=max(notTake=dp[i-1][w], take=val[i]+dp[i][w-wt[i]])` — "take" stays on the same item index.

**Example:** wt `[2,4,6]`, val `[5,11,13]`, W=10: pick two of item0? 2+4+4=10 → value 5+11+11=27 or best combo → Output `27`.

**Analogy:** Filling a backpack from a shop with infinite stock of each item — grab as many copies of the best-value items as fit.

**Complexity:** O(n·W) time, O(W) space.

### Rod Cutting Problem | (DP - 24)  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/rod-cutting-problem-dp-24/) · 🎥 [YouTube](https://youtu.be/mO8XpGoJwuo)

**Intuition / Approach:** Cut a rod of length `N` into pieces to maximize price; piece of length `i` has price `price[i-1]`. Unbounded knapsack where item length `i` can be used repeatedly to fill length `N`.

**Example:** length 5, prices `[2,5,7,8,10]`: cut 2+3 → 5+7=12, or 2+2+1 → 5+5+2=12; best = `12`.

**Analogy:** A blacksmith slicing an iron rod into salable lengths — choose cut sizes (reusable) to fetch the highest total price.

**Complexity:** O(N²) time, O(N) space.

---

## DP on Strings

### Longest common subsequence  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/print-longest-common-subsequence-dp-26/) · 🎥 [YouTube](https://youtu.be/-zI4mrF2Pb4)

**Intuition / Approach:** `dp[i][j]` over prefixes. Match → `1+dp[i-1][j-1]`; mismatch → `max(dp[i-1][j], dp[i][j-1])`. 1-based indexing with empty-prefix base row/col = 0.

**Example:** `"abcde"`, `"ace"`: LCS = "ace" → Output `3`.

**Analogy:** Finding the longest storyline two movies share in order, allowing skipped scenes but never reordering.

**Complexity:** O(n·m) time, O(m) space optimized.

### Print Longest Common Subsequence | (DP - 26)  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/print-longest-common-subsequence-dp-26/) · 🎥 [YouTube](https://youtu.be/-zI4mrF2Pb4)

**Intuition / Approach:** First fill the LCS table, then **backtrack** from `dp[n][m]`: if characters match, append and move diagonally; else move toward the larger neighbour. Reverse the collected string.

**Example:** `"abcde"`,`"ace"`: backtrack path collects 'e','c','a' → reverse → Output `"ace"`.

**Analogy:** Retracing your footsteps on the LCS map to actually reconstruct the shared route, not just its length.

**Complexity:** O(n·m) time, O(n·m) space (full table needed for backtracking).

### Longest common substring  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/longest-common-substring-dp-27/) · 🎥 [YouTube](https://youtu.be/_wP9mWNPL5w)

**Intuition / Approach:** Substring must be **contiguous**. `dp[i][j]=1+dp[i-1][j-1]` on match, else **reset to 0**. Track the global maximum.

**Example:** `"abcjklp"`,`"acjkp"`: common substring "cjk" → Output `2`? — longest contiguous "jk" length `2` (or "cjk" if aligned) → the max value in table.

**Analogy:** Finding the longest unbroken shared phrase in two documents — one different word and the streak resets.

**Complexity:** O(n·m) time, O(m) space optimized.

### Longest palindromic subsequence  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/longest-palindromic-subsequence/) · 🎥 [YouTube](https://youtu.be/6i_T5kkfv4A)

**Intuition / Approach:** LPS(s) = LCS(s, reverse(s)). The longest subsequence that reads the same forwards and backwards is exactly what matches between the string and its reverse.

**Example:** `"bbbab"`: reverse `"babbb"`, LCS = "bbbb" → Output `4`.

**Analogy:** The longest symmetrical necklace you can string by picking beads in order — mirror the string against itself to find the shared symmetric core.

**Complexity:** O(n²) time, O(n) space optimized.

### Minimum insertions to make string palindrome | DP-29  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/) · 🎥 [YouTube](https://www.youtube.com/watch?v=xPBLEj41rFU)

**Intuition / Approach:** Keep the longest palindromic subsequence untouched; every other character needs a mirror inserted. Answer = `n - LPS(s)`.

**Example:** `"abcaa"`? Take `"mbadm"`: LPS=3 ("mam"/"aba") → insertions = 5−3 = `2`.

**Analogy:** Turning a word into a palindrome by adding letters — you only pay for the letters that lack a mirror partner.

**Complexity:** O(n²) time, O(n) space optimized.

### Minimum insertions or deletions to convert string A to B  🔴 Hard
**Links:** [LeetCode (Delete Operation)](https://leetcode.com/problems/delete-operation-for-two-strings/) · 🎥 [YouTube](https://www.youtube.com/watch?v=yMnH0jrir0Q)

**Intuition / Approach:** Keep the LCS common to both; delete the rest from A and insert the rest of B. Answer = `(n - LCS) + (m - LCS)`.

**Example:** `"heap"`,`"pea"`: LCS="ea"=2 → deletions=(4−2)=2, insertions=(3−2)=1 → total `3`.

**Analogy:** Editing one manuscript into another — the shared sentences stay; you cut the extra ones and type in the missing ones.

**Complexity:** O(n·m) time, O(m) space optimized.

### Shortest common supersequence  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/shortest-common-supersequence/) · 🎥 [YouTube](https://youtu.be/xElxAuBcvsU)

**Intuition / Approach:** Shortest string containing both as subsequences has length `n+m-LCS`. Build it by backtracking the LCS table, emitting matched chars once and unmatched chars from whichever side.

**Example:** `"abac"`,`"cab"`: LCS="ab"=2, SCS length = 4+3−2=5, e.g. `"cabac"`. Output `"cabac"`.

**Analogy:** Merging two playlists into the shortest single playlist that contains both in order — shared songs are listed only once.

**Complexity:** O(n·m) time, O(n·m) space (table for reconstruction).

### Distinct subsequences  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/distinct-subsequences/) · 🎥 [YouTube](https://youtu.be/nVG7eTiD2bY)

**Intuition / Approach:** Count how many times `t` appears as a subsequence of `s`. `dp[i][j]`: if match, `dp[i-1][j-1]+dp[i-1][j]` (use it or skip it); else `dp[i-1][j]`.

**Example:** s=`"rabbbit"`, t=`"rabbit"`: Output `3` distinct ways.

**Analogy:** Counting the number of ways to highlight the word `t` inside a longer text `s` by choosing which matching letters to mark.

**Complexity:** O(n·m) time, O(m) space optimized.

### Edit distance  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/edit-distance/) · 🎥 [YouTube](https://youtu.be/fJaKO8FbDdo)

**Intuition / Approach:** Min insert/delete/replace to turn `s1` into `s2`. Match → `dp[i-1][j-1]`; else `1+min(insert=dp[i][j-1], delete=dp[i-1][j], replace=dp[i-1][j-1])`.

**Example:** `"horse"`→`"ros"`: replace h→r, remove r, remove e → Output `3`.

**Analogy:** The fewest keystrokes (type, delete, overwrite) to fix one word into another in a text editor.

**Complexity:** O(n·m) time, O(m) space optimized.

### Wildcard matching  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/wildcard-matching/) · 🎥 [YouTube](https://youtu.be/ZmlQ3vgAOMo)

**Intuition / Approach:** Pattern with `?` (any one char) and `*` (any sequence incl. empty). `dp[i][j]`: on `?` or equal char → `dp[i-1][j-1]`; on `*` → `dp[i-1][j] (star absorbs a char) || dp[i][j-1] (star empty)`.

**Example:** s=`"adceb"`, p=`"*a*b"`: matches → Output `true`.

**Analogy:** File-search wildcards in a terminal — `*.txt` matches any filename ending in .txt; the `*` stretches to swallow whatever it must.

**Complexity:** O(n·m) time, O(m) space optimized.

---

## DP on Stocks

### Best time to buy and sell stock  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) · 🎥 [YouTube](https://youtu.be/excAOvwF_Wk)

**Intuition / Approach:** One transaction. Track the minimum price seen so far; at each day the best profit is `price - minSoFar`. Keep the maximum.

**Example:** `[7,1,5,3,6,4]`: buy at 1, sell at 6 → Output `5`.

**Analogy:** Buy low, sell high — once. Remember the cheapest day behind you and check today's gain against it.

**Complexity:** O(n) time, O(1) space.

### Best time to buy and sell stock II  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) · 🎥 [YouTube](https://youtu.be/nGJmxkUJQGs)

**Intuition / Approach:** Unlimited transactions. State `(day, buy?)`; each day buy/sell/skip. Greedy equivalent: sum every positive `price[i]-price[i-1]`.

**Example:** `[7,1,5,3,6,4]`: (5−1)+(6−3)=4+3 → Output `7`.

**Analogy:** Day-trading with no limit — capture every uphill segment of the price chart.

**Complexity:** O(n) time, O(1) space.

### Best time to buy and sell stock III  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/) · 🎥 [YouTube](https://youtu.be/-uQGzhYj8BQ)

**Intuition / Approach:** At most **2** transactions. Add a `cap` dimension `(day, buy?, cap)`; selling decrements cap. Answer = `f(0, buy=1, cap=2)`.

**Example:** `[3,3,5,0,0,3,1,4]`: buy0 sell5(day2) profit? best two-transaction total → Output `6`.

**Analogy:** A trader allowed only two round-trips this quarter — plan the two most profitable windows.

**Complexity:** O(n·2·3) time, O(2·3) space.

### Best time to buy and sell stock IV  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/) · 🎥 [YouTube](https://youtu.be/IV1dHbk5CDc)

**Intuition / Approach:** Generalize III to at most **K** transactions. Same 3-state DP with `cap` running from 0..K.

**Example:** `[2,4,1]`, K=2: buy2 sell4 → Output `2`.

**Analogy:** A trader with a fixed quota of K trades this year — allocate them to the K best price swings.

**Complexity:** O(n·2·K) time, O(2·K) space.

### Best Time to Buy and Sell Stock with Cooldown  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) · 🎥 [YouTube](https://youtu.be/IGIe46xw3YY)

**Intuition / Approach:** Unlimited transactions but after selling you must skip one day. After a sell, recurse to `day+2` instead of `day+1`. State `(day, buy?)`.

**Example:** `[1,2,3,0,2]`: buy1 sell3(day2), cooldown day3, buy0 sell2 → Output `3`.

**Analogy:** Trading with a mandatory rest day after each sale — bake the enforced break into your plan.

**Complexity:** O(n) time, O(1) space.

### Best time to buy and sell stock with transaction fees  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/) · 🎥 [YouTube](https://youtu.be/k4eK-vEmnKg)

**Intuition / Approach:** Unlimited transactions, but subtract a fixed `fee` on each sell (or buy). Same `(day, buy?)` DP with `-fee` added on the sell transition.

**Example:** `[1,3,2,8,4,9]`, fee=2: buy1 sell8 (profit 7−2=5) + buy4 sell9 (5−2=3) → Output `8`.

**Analogy:** Trading through a broker who charges commission per trade — only take swings big enough to beat the fee.

**Complexity:** O(n) time, O(1) space.

---

## DP on LIS

### Longest Increasing Subsequence  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/) · 🎥 [YouTube](https://youtu.be/on2hvxBXJH4)

**Intuition / Approach:** `dp[i]` = length of longest increasing subsequence ending at `i`; for each `i` scan all `j<i` with `a[j]<a[i]`. O(n log n) via a `tails` array + binary search.

**Example:** `[10,9,2,5,3,7,101,18]`: LIS = [2,3,7,101] → Output `4`.

**Analogy:** Building the longest chain of ever-taller people you can pick in order from a line.

**Complexity:** O(n²) or O(n log n) time, O(n) space.

### Print Longest Increasing Subsequence  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/printing-longest-increasing-subsequence-dp-42/) · 🎥 [YouTube](https://youtu.be/IFfYfonAFGc)

**Intuition / Approach:** Fill `dp[]` and a `parent[]` (previous index). Track the index with the max `dp`, then walk `parent[]` backwards to reconstruct and reverse.

**Example:** `[10,9,2,5,3,7,101,18]`: reconstruct → Output `[2,3,7,18]` or `[2,3,7,101]` (one valid LIS).

**Analogy:** Not just measuring the tallest people-chain but naming each person in it by following "who I stood behind" links.

**Complexity:** O(n²) time, O(n) space.

### Longest Increasing Subsequence |(DP-43)  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/) · 🎥 [YouTube](https://youtu.be/on2hvxBXJH4)

**Intuition / Approach:** The optimized **binary-search** LIS: maintain `tails[k]` = smallest possible tail of an increasing subsequence of length `k+1`. For each element, `lower_bound` and replace/append. Length = size of `tails`.

**Example:** `[2,6,8,3,4,5,1]`: tails evolves `[2],[2,6],[2,6,8],[2,3,8],[2,3,4],[2,3,4,5]...` → Output `4`.

**Analogy:** Keeping a leaderboard of the smallest possible "closer" for each streak length — patience-sorting cards into piles.

**Complexity:** O(n log n) time, O(n) space.

### Largest Divisible Subset  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/largest-divisible-subset/) · 🎥 [YouTube](https://youtu.be/gDuZwBW9VvM)

**Intuition / Approach:** Sort, then LIS where the relation is "divides": `a[i] % a[j] == 0`. Track `parent[]` to reconstruct the subset.

**Example:** `[1,2,4,8]`: each divides the next → Output `[1,2,4,8]`.

**Analogy:** Building the longest ladder of numbers where each rung cleanly divides into the next — like nested Russian dolls that fit perfectly.

**Complexity:** O(n²) time, O(n) space.

### Longest String Chain  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/longest-string-chain/) · 🎥 [YouTube](https://youtu.be/YY8iBaYcc4g)

**Intuition / Approach:** Sort words by length; LIS where `wordA` is a predecessor of `wordB` if deleting exactly one char from B yields A. `dp[i]=max chain ending at word i`.

**Example:** `["a","b","ba","bca","bda","bdca"]`: a→ba→bda→bdca → Output `4`.

**Analogy:** Evolving a word one added letter at a time (like Scrabble growth) — find the longest evolutionary chain.

**Complexity:** O(n·L²) time (L = word length), O(n) space.

### Longest Bitonic Subsequence  🟡 Medium
**Links:** [Article](https://takeuforward.org/data-structure/longest-bitonic-subsequence-dp-46/) · 🎥 [YouTube](https://youtu.be/y4vN0WNdrlg)

**Intuition / Approach:** Bitonic = increases then decreases. Compute LIS from left (`dp1[i]`) and LIS from right (`dp2[i]`). Answer = `max(dp1[i]+dp2[i]-1)` over all peaks `i`.

**Example:** `[1,2,1,2,1]`: peak gives up 1,2 then down 1 → Output `3`.

**Analogy:** A mountain profile of numbers — climb up then come down; find the tallest such mountain silhouette.

**Complexity:** O(n²) time, O(n) space.

### Number of Longest Increasing Subsequences  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/number-of-longest-increasing-subsequence/) · 🎥 [YouTube](https://youtu.be/cKVl1TFdNXg)

**Intuition / Approach:** Alongside `len[i]` (LIS length ending at i) keep `cnt[i]` (number of such LIS). When extending: if `len[j]+1 > len[i]` reset count; if equal, add `cnt[j]`. Sum `cnt[i]` where `len[i]` is global max.

**Example:** `[1,3,5,4,7]`: two LIS of length 4 (`1,3,5,7` and `1,3,4,7`) → Output `2`.

**Analogy:** Not just measuring the longest people-chain but counting how many different longest chains exist.

**Complexity:** O(n²) time, O(n) space.

---

## MCM DP | Partition DP

### Matrix chain multiplication  🔴 Hard
**Links:** [Article](https://takeuforward.org/dynamic-programming/matrix-chain-multiplication-dp-48/) · 🎥 [YouTube](https://youtu.be/vRVfmbCFW7Y)

**Intuition / Approach:** Given dimensions, find the parenthesization minimizing scalar multiplications. `f(i,j)=min over k of f(i,k)+f(k+1,j)+dim[i-1]·dim[k]·dim[j]`. Interval/partition DP; the split `k` is the last multiplication.

**Example:** dims `[10,20,30,40]`: best order gives Output `18000` multiplications.

**Analogy:** Choosing the order to multiply a chain of matrices (or combine ingredients) so the total work is least — order of grouping matters a lot.

**Complexity:** O(n³) time, O(n²) space.

### Matrix Chain Multiplication | Bottom-Up|(DP-49)  🔴 Hard
**Links:** [Article](https://takeuforward.org/data-structure/matrix-chain-multiplication-tabulation-method-dp-49/) · 🎥 [YouTube](https://youtu.be/pDCXsbAw5Cg)

**Intuition / Approach:** Same recurrence, iterative table. Loop `i` from high to low, `j` from `i+1` upward, inner loop over split `k`. Fills smaller intervals before larger.

**Example:** dims `[10,20,30]`: single product cost `10·20·30=6000` → Output `6000`.

**Analogy:** Same matrix-grouping puzzle, but solved with a filled ledger from smallest chains outward — no recursion stack.

**Complexity:** O(n³) time, O(n²) space.

### Minimum cost to cut the stick  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/) · 🎥 [YouTube](https://youtu.be/xwomavsC86c)

**Intuition / Approach:** Cost of a cut = current stick length. Sort cut positions, pad with `0` and `n`. `f(i,j)=min over k of f(i,k)+f(k+1,j)+(cuts[j+1]-cuts[i-1])`. The order of cuts changes total cost → partition DP on which cut is last.

**Example:** n=7, cuts `[1,3,4,5]`: an optimal order yields Output `16`.

**Analogy:** Sawing a plank at marked points where each cut costs the current piece's length — choosing the cut order to minimize sawing effort.

**Complexity:** O(m³) time (m = #cuts), O(m²) space.

### Burst balloons  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/burst-balloons/) · 🎥 [YouTube](https://youtu.be/Yz4LlDSlkns)

**Intuition / Approach:** Think about which balloon is burst **last** in an interval (so its neighbours are the interval bounds). Pad with 1s. `f(i,j)=max over k of f(i,k-1)+f(k+1,j)+a[i-1]·a[k]·a[j+1]`.

**Example:** `[3,1,5,8]`: optimal last-burst ordering → Output `167`.

**Analogy:** Popping balloons for coins where each pop's value depends on current neighbours — decide who pops LAST so its big neighbours are still around.

**Complexity:** O(n³) time, O(n²) space.

### Different Ways to Evaluate a Boolean Expression  🟡 Medium
**Links:** [LeetCode (Parsing A Boolean Expression)](https://leetcode.com/problems/parsing-a-boolean-expression/) · 🎥 [YouTube](https://youtu.be/MM7fXopgyjw)

**Intuition / Approach:** Count parenthesizations that make the expression **true**. Partition on each operator `k`; combine left/right true-counts and false-counts according to `&`, `|`, `^`. State `f(i,j,isTrue)`.

**Example:** `"T|F&T"`: count groupings evaluating to true → Output depends on operator precedence choices (e.g. `2`).

**Analogy:** Adding parentheses to a logic sentence in every possible way and counting how many arrangements make it come out "true".

**Complexity:** O(n³) time, O(n²) space.

### Palindrome partitioning II  🔴 Hard
**Links:** [LeetCode](https://leetcode.com/problems/palindrome-partitioning-ii/) · 🎥 [YouTube](https://youtu.be/_H8V5hJUGd0)

**Intuition / Approach:** Min cuts so every piece is a palindrome. **Front partition**: `f(i)=min over j≥i where s[i..j] is palindrome of 1+f(j+1)`. Subtract 1 at the end (cuts = pieces − 1).

**Example:** `"aab"`: cut after "aa" → ["aa","b"], 1 cut → Output `1`.

**Analogy:** Slicing a ribbon of letters into palindromic pieces with the fewest scissors cuts.

**Complexity:** O(n²) time, O(n) space.

### Partition Array for Maximum Sum  🟡 Medium
**Links:** [LeetCode](https://leetcode.com/problems/partition-array-for-maximum-sum/) · 🎥 [YouTube](https://youtu.be/PhWWJmaKfMc)

**Intuition / Approach:** Partition into contiguous groups of size ≤ K; each group's every element becomes the group's max. **Front partition**: `f(i)=max over len 1..K of (max_in_window · len + f(i+len))`.

**Example:** `[1,15,7,9,2,5,10]`, K=3: groups `[1,15,7],[9],[2,5,10]` → 15·3+9+10·3 → Output `84`.

**Analogy:** Grouping consecutive workers into teams (≤K each) where everyone earns the team's top salary — split to maximize total payout.

**Complexity:** O(n·K) time, O(n) space.

---

## DP on Squares

### Maximum Rectangle Area with all 1's|(DP-55)  🔴 Hard
**Links:** [LeetCode (Maximal Rectangle)](https://leetcode.com/problems/maximal-rectangle/) · 🎥 [YouTube](https://youtu.be/tOylVCugy9k)

**Intuition / Approach:** Treat each row as the base of a histogram: accumulate consecutive 1s column-wise as bar heights, then run **largest-rectangle-in-histogram** (monotonic stack) for each row; take the max area.

**Example:** matrix with a 2×3 block of 1s → largest all-1 rectangle area = `6`. Output `6`.

**Analogy:** Stacking bricks row by row and finding the biggest solid wall of bricks you can outline — a histogram trick applied per floor.

**Complexity:** O(n·m) time, O(m) space.

### Count Square Submatrices with All Ones|(DP-56)  🟢 Easy
**Links:** [LeetCode](https://leetcode.com/problems/count-square-submatrices-with-all-ones/) · 🎥 [YouTube](https://youtu.be/auS1fynpnjo)

**Intuition / Approach:** `dp[i][j]` = side of largest all-1 square with bottom-right corner `(i,j)` = `1+min(top, left, top-left)` if cell is 1. **Sum of all `dp[i][j]`** = total count of all-1 squares.

**Example:** `[[0,1,1,1],[1,1,1,1],[0,1,1,1]]`: sum of dp = `15` squares. Output `15`.

**Analogy:** Every cell reports the biggest solid square ending at it; adding up all those reports counts every square of every size at once.

**Complexity:** O(n·m) time, O(n·m) space (O(m) optimizable).

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---------|-----------|---------|---------------|
| 1 | Introduction to DP | 🟢 Easy | Introduction to DP | [Article](https://takeuforward.org/data-structure/dynamic-programming-introduction/) |
| 2 | Climbing stairs | 🟡 Medium | 1D DP | [LeetCode](https://leetcode.com/problems/climbing-stairs/) |
| 3 | Frog Jump | 🟡 Medium | 1D DP | [Article](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-dp-3/) |
| 4 | Frog jump with K distances | 🟡 Medium | 1D DP | [Article](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-with-k-distances-dp-4/) |
| 5 | Maximum sum of non adjacent elements | 🟡 Medium | 1D DP | [LeetCode](https://leetcode.com/problems/house-robber/) |
| 6 | House robber | 🟡 Medium | 1D DP | [LeetCode](https://leetcode.com/problems/house-robber-ii/) |
| 7 | Ninja's training | 🟡 Medium | 2D/3D & Grids | [Article](https://takeuforward.org/data-structure/dynamic-programming-ninjas-training-dp-7/) |
| 8 | Grid Unique Paths (DP8) | 🟡 Medium | 2D/3D & Grids | [LeetCode](https://leetcode.com/problems/unique-paths/) |
| 9 | Unique paths II | 🟡 Medium | 2D/3D & Grids | [LeetCode](https://leetcode.com/problems/unique-paths-ii/) |
| 10 | Minimum Falling Path Sum | 🟡 Medium | 2D/3D & Grids | [LeetCode](https://leetcode.com/problems/minimum-path-sum/) |
| 11 | Triangle | 🟡 Medium | 2D/3D & Grids | [LeetCode](https://leetcode.com/problems/triangle/) |
| 12 | Ninja and his Friends | 🟡 Medium | 2D/3D & Grids | [Article](https://takeuforward.org/data-structure/3-d-dp-ninja-and-his-friends-dp-13/) |
| 13 | Subset sum equal to target | 🔴 Hard | DP on Subsequences | [Article](https://takeuforward.org/data-structure/subset-sum-equal-to-target-dp-14/) |
| 14 | Partition equal subset sum | 🔴 Hard | DP on Subsequences | [LeetCode](https://leetcode.com/problems/partition-equal-subset-sum/) |
| 15 | Partition set into 2 subsets min abs diff | 🔴 Hard | DP on Subsequences | [LeetCode](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/) |
| 16 | Count subsets with sum K | 🔴 Hard | DP on Subsequences | [Article](https://takeuforward.org/data-structure/count-subsets-with-sum-k-dp-17/) |
| 17 | Count partitions with given difference | 🔴 Hard | DP on Subsequences | [Article](https://takeuforward.org/data-structure/count-partitions-with-given-difference-dp-18/) |
| 18 | Assign Cookies | 🟢 Easy | DP on Subsequences | [LeetCode](https://leetcode.com/problems/assign-cookies/) |
| 19 | Minimum Coins (DP-20) | 🔴 Hard | DP on Subsequences | [LeetCode](https://leetcode.com/problems/coin-change/) |
| 20 | Target sum | 🔴 Hard | DP on Subsequences | [LeetCode](https://leetcode.com/problems/target-sum/) |
| 21 | Coin Change 2 (DP-22) | 🔴 Hard | DP on Subsequences | [LeetCode](https://leetcode.com/problems/coin-change-2/) |
| 22 | Unbounded knapsack | 🔴 Hard | DP on Subsequences | [Article](https://takeuforward.org/data-structure/unbounded-knapsack-dp-23/) |
| 23 | Rod Cutting Problem (DP-24) | 🔴 Hard | DP on Subsequences | [Article](https://takeuforward.org/data-structure/rod-cutting-problem-dp-24/) |
| 24 | Longest common subsequence | 🔴 Hard | DP on Strings | [Article](https://takeuforward.org/data-structure/print-longest-common-subsequence-dp-26/) |
| 25 | Print Longest Common Subsequence (DP-26) | 🔴 Hard | DP on Strings | [Article](https://takeuforward.org/data-structure/print-longest-common-subsequence-dp-26/) |
| 26 | Longest common substring | 🔴 Hard | DP on Strings | [Article](https://takeuforward.org/data-structure/longest-common-substring-dp-27/) |
| 27 | Longest palindromic subsequence | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/longest-palindromic-subsequence/) |
| 28 | Minimum insertions to make palindrome (DP-29) | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/) |
| 29 | Min insertions/deletions A to B | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/delete-operation-for-two-strings/) |
| 30 | Shortest common supersequence | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/shortest-common-supersequence/) |
| 31 | Distinct subsequences | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/distinct-subsequences/) |
| 32 | Edit distance | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/edit-distance/) |
| 33 | Wildcard matching | 🔴 Hard | DP on Strings | [LeetCode](https://leetcode.com/problems/wildcard-matching/) |
| 34 | Best time to buy and sell stock | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) |
| 35 | Best time to buy and sell stock II | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) |
| 36 | Best time to buy and sell stock III | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/) |
| 37 | Best time to buy and sell stock IV | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/) |
| 38 | Buy/sell stock with cooldown | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/) |
| 39 | Buy/sell stock with transaction fee | 🟡 Medium | DP on Stocks | [LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/) |
| 40 | Longest Increasing Subsequence | 🟡 Medium | DP on LIS | [Article](https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/) |
| 41 | Print Longest Increasing Subsequence | 🟡 Medium | DP on LIS | [Article](https://takeuforward.org/data-structure/printing-longest-increasing-subsequence-dp-42/) |
| 42 | Longest Increasing Subsequence (DP-43) | 🟡 Medium | DP on LIS | [Article](https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/) |
| 43 | Largest Divisible Subset | 🟡 Medium | DP on LIS | [LeetCode](https://leetcode.com/problems/largest-divisible-subset/) |
| 44 | Longest String Chain | 🟡 Medium | DP on LIS | [LeetCode](https://leetcode.com/problems/longest-string-chain/) |
| 45 | Longest Bitonic Subsequence | 🟡 Medium | DP on LIS | [Article](https://takeuforward.org/data-structure/longest-bitonic-subsequence-dp-46/) |
| 46 | Number of Longest Increasing Subsequences | 🟡 Medium | DP on LIS | [LeetCode](https://leetcode.com/problems/number-of-longest-increasing-subsequence/) |
| 47 | Matrix chain multiplication | 🔴 Hard | MCM / Partition DP | [Article](https://takeuforward.org/dynamic-programming/matrix-chain-multiplication-dp-48/) |
| 48 | Matrix Chain Multiplication Bottom-Up (DP-49) | 🔴 Hard | MCM / Partition DP | [Article](https://takeuforward.org/data-structure/matrix-chain-multiplication-tabulation-method-dp-49/) |
| 49 | Minimum cost to cut the stick | 🔴 Hard | MCM / Partition DP | [LeetCode](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/) |
| 50 | Burst balloons | 🔴 Hard | MCM / Partition DP | [LeetCode](https://leetcode.com/problems/burst-balloons/) |
| 51 | Different Ways to Evaluate Boolean Expression | 🟡 Medium | MCM / Partition DP | [LeetCode](https://leetcode.com/problems/parsing-a-boolean-expression/) |
| 52 | Palindrome partitioning II | 🔴 Hard | MCM / Partition DP | [LeetCode](https://leetcode.com/problems/palindrome-partitioning-ii/) |
| 53 | Partition Array for Maximum Sum | 🟡 Medium | MCM / Partition DP | [LeetCode](https://leetcode.com/problems/partition-array-for-maximum-sum/) |
| 54 | Maximum Rectangle Area with all 1's (DP-55) | 🔴 Hard | DP on Squares | [LeetCode](https://leetcode.com/problems/maximal-rectangle/) |
| 55 | Count Square Submatrices with All Ones (DP-56) | 🟢 Easy | DP on Squares | [LeetCode](https://leetcode.com/problems/count-square-submatrices-with-all-ones/) |

*Note: the source data lists 57 entries; two LIS entries (Longest Increasing Subsequence base + DP-43) and two LCS entries (LCS + Print LCS DP-26) are near-duplicates kept as separate practice reps above; the checklist consolidates to 55 unique rows.*
