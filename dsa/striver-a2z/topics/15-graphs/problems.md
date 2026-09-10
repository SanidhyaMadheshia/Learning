# Graphs — Problems (by Pattern)

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

> Problems are grouped by pattern (in sheet order). Every problem includes intuition, a worked example, and a memory-hook analogy. Difficulty: 🟢 Easy · 🟡 Medium · 🔴 Hard.

---

## Learning

### Introduction to Graph  🟢
**Links:** [Article](https://takeuforward.org/data-structure/graph-representation-in-java) · 🎥 [YouTube](https://youtu.be/3oI-34aPMWM)
**Intuition / Approach:** Learn the vocabulary — vertices, edges, directed/undirected, weighted/unweighted, degree, paths, cycles, components. Understand that graphs generalise trees and grids.
**Example:** Vertices `{0,1,2}`, edges `{0-1, 1-2}` → a path graph; degree of node 1 is 2.
**Analogy:** A graph is a **city map**: intersections are vertices, roads are edges; one-way streets are directed edges, toll costs are weights.

### Graph Representation | C++  🟢
**Links:** [Article](https://takeuforward.org/graph/graph-representation-in-c/) · 🎥 [YouTube](https://youtu.be/3oI-34aPMWM)
**Intuition / Approach:** Store the graph as an adjacency matrix (`O(V²)`, O(1) edge lookup) or adjacency list (`O(V+E)`, ideal for sparse graphs). Build the list by pushing `v` into `adj[u]` (and `u` into `adj[v]` if undirected).
**Example:** Edges `{0-1,0-2}` → adjacency list `0:[1,2], 1:[0], 2:[0]`.
**Analogy:** An adjacency **matrix** is a full seating chart marking who-sits-next-to-whom for every pair; an adjacency **list** is each person's personal contact list — far more compact when most people barely know each other.

### Graph Representation | Java  🟢
**Links:** [Article](https://takeuforward.org/data-structure/graph-representation-in-java) · 🎥 [YouTube](https://youtu.be/3oI-34aPMWM)
**Intuition / Approach:** Same concept in Java: use `ArrayList<ArrayList<Integer>>` for the list, or an `int[][]` matrix. For weighted graphs store pairs `(neighbor, weight)`.
**Example:** `V=3`, edges `{0-1,1-2}` → `adj.get(0)=[1]`, `adj.get(1)=[0,2]`, `adj.get(2)=[1]`.
**Analogy:** Same city map, just a different notebook (language) to jot down which roads leave each intersection.

### Connected Components  🟡
**Links:** [Article](https://takeuforward.org/data-structure/connected-components) · Editorial available
**Intuition / Approach:** A graph may be split into several disconnected pieces. Loop over all vertices; every time you find an unvisited one, run a full DFS/BFS from it — that traversal marks one whole component. Count how many launches you make.
**Example:** Nodes `{0,1,2,3,4}`, edges `{0-1, 2-3}`. Launch from 0 (covers 0,1), from 2 (covers 2,3), from 4 (covers 4) → **3 components**.
**Analogy:** Islands in an archipelago — you can walk anywhere within one island, but need a new boat trip (new traversal) to reach the next.

### Traversal Techniques  🟡
**Links:** [Article](https://takeuforward.org/data-structure/depth-first-search-dfs/) · 🎥 [YouTube](https://youtu.be/Qzf1a--rhp8)
**Intuition / Approach:** Two canonical walks: **BFS** (queue, explores level by level → shortest unweighted distance) and **DFS** (stack/recursion, dives deep then backtracks). Both are `O(V+E)` and need a `visited[]`.
**Example:** From node 0 in `0:[1,2], 1:[3], 2:[3]`: BFS order `0,1,2,3`; DFS order `0,1,3,2`.
**Analogy:** BFS is **ripples spreading** from a stone dropped in a pond (all points at radius 1, then radius 2…); DFS is a **maze explorer** who follows one corridor to its dead end before trying another.

### DFS  🟡
**Links:** [Article](https://takeuforward.org/data-structure/depth-first-search-dfs/) · 🎥 [YouTube](https://youtu.be/Qzf1a--rhp8)
**Intuition / Approach:** Recursively visit a node, mark it, then recurse into each unvisited neighbour. Backtrack when stuck. Foundation for cycle detection, topo sort, connectivity, bridges.
**Example:** Graph `0:[1,2], 1:[2], 2:[0,3], 3:[3]` from 0 → visit 0→1→2→3 (self-loop skipped since visited).
**Analogy:** Exploring a **cave system** — you go as deep as the passage allows, then retrace your steps to the last fork and try an unexplored branch.

---

## Problems on BFS/DFS

### Number of provinces  🟡
**Links:** [LeetCode](https://leetcode.com/problems/number-of-provinces/) · 🎥 [YouTube](https://youtu.be/ACzkVtewUYA)
**Intuition / Approach:** The `isConnected` matrix is an adjacency matrix. Count connected components: DFS/BFS from each unvisited city, marking all reachable cities; each launch is one province.
**Example:** `[[1,1,0],[1,1,0],[0,0,1]]` → cities {0,1} connected, city 2 alone → **2 provinces**.
**Analogy:** Grouping friends into **friend circles** — if A knows B and B knows C, all three are one circle even if A never met C directly.

### Connected Components Problem in Matrix  🟡
**Links:** [Article](https://takeuforward.org/data-structure/connected-components) · Editorial available
**Intuition / Approach:** Treat each filled cell as a node connected to its 4 (or 8) neighbours. Sweep the grid; each unvisited filled cell launches a DFS/BFS covering one component.
**Example:** Grid `[[1,0],[0,1]]` (4-connectivity) → two separate 1-cells → **2 components**.
**Analogy:** Counting separate **puddles** on pavement — cells touching form one puddle; a gap starts a new one.

### Rotten Oranges  🟡
**Links:** [LeetCode](https://leetcode.com/problems/rotting-oranges/) · 🎥 [YouTube](https://www.youtube.com/watch?v=yf3oUhkvqA0)
**Intuition / Approach:** Multi-source BFS. Push all rotten oranges as level-0 sources; each BFS level = one minute; a fresh orange rots when a rotten neighbour reaches it. Answer = last level; if any fresh remains, return -1.
**Example:** `[[2,1,1],[1,1,0],[0,1,1]]` → minute-by-minute rot spreads outward → **4 minutes**.
**Analogy:** Rot spreading in a **fruit basket** — every rotten fruit infects its touching neighbours simultaneously each minute; the clock stops when nothing fresh is left.

### Flood fill algorithm  🟡
**Links:** [LeetCode](https://leetcode.com/problems/flood-fill/) · Editorial available
**Intuition / Approach:** DFS/BFS from the start pixel, recoloring every 4-connected pixel that shares the original color. Guard against infinite recursion when the new color equals the old one.
**Example:** Image `[[1,1,1],[1,1,0],[1,0,1]]`, start `(1,1)`, color 2 → all connected 1s around center become 2.
**Analogy:** The **paint-bucket tool** in an image editor — click a region and it floods contiguous same-colored pixels with the new color.

### Cycle Detection in Undirected Graph (bfs)  🔴
**Links:** [Article](https://takeuforward.org/data-structure/detect-cycle-in-an-undirected-graph-using-bfs/) · 🎥 [YouTube](https://youtu.be/BPlrALf1LDU)
**Intuition / Approach:** BFS carrying each node's `parent`. If you reach an already-visited neighbour that is **not** the parent, a cycle exists.
**Example:** Edges `{0-1,1-2,2-0}` → BFS from 0 visits 1,2; from 2, neighbour 0 is visited and isn't parent → **cycle**.
**Analogy:** Walking a **circular hiking trail** — if you bump into a spot you already passed (and didn't just come from), the trail loops.

### Detect a cycle in an undirected graph  🔴
**Links:** [LeetCode](https://leetcode.com/problems/course-schedule/) · 🎥 [YouTube](https://youtu.be/zQ3zgFypzX4)
**Intuition / Approach:** DFS variant — recurse with the current node's parent; a visited neighbour other than the parent means a back-edge, i.e. a cycle. Check all components.
**Example:** Edges `{0-1,1-2,2-3,3-1}` → DFS reaches 1 again from 3 (parent is 2) → **cycle**.
**Analogy:** Following string in a **ball of yarn** — if a strand loops back to a knot you already tied (not the one you just left), it forms a loop.

### Distance of nearest cell having one  🟡
**Links:** [LeetCode](https://leetcode.com/problems/01-matrix/) · 🎥 [YouTube](https://youtu.be/edXdVwkYHF8)
**Intuition / Approach:** Multi-source BFS from all `1` cells at once. Each `0` cell's BFS level is its distance to the nearest `1`.
**Example:** `[[0,0,0],[0,1,0],[0,0,0]]` → the center is 0, its 4 neighbours are 1, corners are 2.
**Analogy:** Nearest **fire station** distance — start clocks at every station simultaneously; each block records when the first responders reach it.

### Surrounded Regions  🟡
**Links:** [LeetCode](https://leetcode.com/problems/surrounded-regions/) · 🎥 [YouTube](https://youtu.be/BtdgAys4yMk)
**Intuition / Approach:** An `O` survives only if connected to a border `O`. DFS/BFS from all border `O`s marking them safe; flip every unmarked `O` to `X`.
**Example:** `[[X,X,X],[X,O,X],[X,X,X]]` → center `O` isn't border-connected → becomes `X`.
**Analogy:** A **fenced field** — any patch of grass touching the outer fence stays; grass fully enclosed by walls gets paved over.

### Number of enclaves  🟡
**Links:** [LeetCode](https://leetcode.com/problems/number-of-enclaves/) · 🎥 [YouTube](https://youtu.be/rxKcepXQgU4)
**Intuition / Approach:** Land cells that can walk off the boundary escape. DFS/BFS from all border land cells to mark escapable land; count remaining trapped land cells.
**Example:** `[[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]` → the inner cluster can't reach the edge → count of enclaved 1s.
**Analogy:** Counting **castaways** — anyone who can reach the coastline is rescued; the tally is the ones stuck inland with no path out.

### Word ladder I  🔴
**Links:** [LeetCode](https://leetcode.com/problems/word-ladder/) · 🎥 [YouTube](https://youtu.be/tRPda0rcf8E)
**Intuition / Approach:** Model each word as a node; edges connect words differing by one letter. BFS from `beginWord` gives the shortest transformation length. Use a hash set for the dictionary.
**Example:** `hit → hot → dot → dog → cog` → length **5**.
**Analogy:** A **word-change puzzle** — change one letter at a time, each intermediate must be a real word; BFS finds the fewest moves.

### Word ladder II  🔴
**Links:** [LeetCode](https://leetcode.com/problems/word-ladder-ii/) · 🎥 [YouTube](https://youtu.be/AD4SFl7tu7I?si=EpcJQTWm2YeURvEG)
**Intuition / Approach:** Return **all** shortest transformation sequences. BFS level by level building predecessor info (or storing full paths), then reconstruct every shortest path. Erase used words per level to avoid longer paths.
**Example:** `hit → cog` may yield `[hit,hot,dot,dog,cog]` and `[hit,hot,lot,log,cog]`.
**Analogy:** Listing **every equally-shortest route** on a GPS — not just one, but all paths that tie for the minimum number of turns.

### Number of islands  🟡
**Links:** [LeetCode](https://leetcode.com/problems/number-of-islands/) · 🎥 [YouTube](https://www.youtube.com/watch?v=muncqlKJrH0&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=8)
**Intuition / Approach:** Grid components again. Each unvisited land cell launches a DFS/BFS that sinks the whole island (marks all connected land); count launches.
**Example:** `[[1,1,0],[0,0,0],[0,0,1]]` → top-left blob + bottom-right cell → **2 islands**.
**Analogy:** Counting **islands from a plane** — touch-connected land is one island; open water between them separates the count.

### Bipartite Graph (DFS)  🔴
**Links:** [LeetCode](https://leetcode.com/problems/is-graph-bipartite/) · 🎥 [YouTube](https://youtu.be/KG5YFfR0j8A)
**Intuition / Approach:** Try to 2-color the graph so adjacent nodes differ. DFS/BFS assigning alternating colors; a conflict (adjacent same color) means not bipartite. Odd-length cycles break bipartiteness.
**Example:** Square `0-1-2-3-0` (even cycle) is bipartite {0,2}/{1,3}; a triangle `0-1-2-0` is not.
**Analogy:** Splitting people into **two teams** where every rivalry crosses teams — impossible if three people all mutually dislike each other (odd cycle).

### Cycle Detection in Directed Graph (DFS)  🔴
**Links:** [LeetCode](https://leetcode.com/problems/course-schedule-ii/) · 🎥 [YouTube](https://youtu.be/9twcmtQj4DU)
**Intuition / Approach:** DFS with two markers: `visited` and `pathVisited` (recursion stack). Reaching a node already on the current stack is a back-edge ⇒ directed cycle. Reset `pathVisited` on backtrack.
**Example:** Edges `0→1, 1→2, 2→0` → DFS from 0 revisits 0 on the same stack → **cycle**.
**Analogy:** Chasing **circular dependencies** — task A waits on B, B on C, C on A: nobody can start; the wait-chain loops back on itself.

---

## Topo Sort and Problems

### Topo Sort  🔴
**Links:** [Article](https://takeuforward.org/data-structure/topological-sort-algorithm-dfs-g-21/) · 🎥 [YouTube](https://youtu.be/5lZ0iJMrUMk)
**Intuition / Approach:** A linear ordering of DAG vertices so every edge `u→v` puts `u` before `v`. DFS variant: push a node onto a stack after all its descendants finish; reverse the stack.
**Example:** Edges `5→0, 5→2, 4→0, 4→1, 2→3, 3→1` → valid order `5 4 2 3 1 0`.
**Analogy:** **Getting dressed** — socks before shoes, shirt before jacket; topo sort lists a valid order respecting all "before" rules.

### Topological sort or Kahn's algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/topological-sort-algorithm-dfs-g-21/) · 🎥 [YouTube](https://youtu.be/5lZ0iJMrUMk)
**Intuition / Approach:** BFS-based topo sort. Compute in-degrees; enqueue all zero-in-degree nodes; repeatedly pop one, append it, and decrement neighbours' in-degrees, enqueuing new zeros. Output smaller than `V` ⇒ cycle.
**Example:** Same DAG; nodes with in-degree 0 (`4,5`) go first, then unlock the rest in order.
**Analogy:** A **buffet line** — you can only take a dish once all its prerequisite dishes are served; in-degree 0 means "nothing blocks me, serve me now."

### Detect a cycle in a directed graph  🔴
**Links:** [LeetCode](https://leetcode.com/problems/course-schedule/) · 🎥 [YouTube](https://www.youtube.com/watch?v=uzVUw90ZFIg&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=12)
**Intuition / Approach:** Run Kahn's algorithm; if fewer than `V` nodes are output, some nodes were never freed (in-degree never hit 0) → a cycle exists. Equivalent to DFS recursion-stack detection.
**Example:** Edges `0→1,1→2,2→0` → no node ever reaches in-degree 0 → output size 0 < 3 → **cycle**.
**Analogy:** A **deadlock detector** — if some processes are still waiting after you've cleared everyone who could proceed, they're stuck in a wait-cycle.

### Course Schedule I  🔴
**Links:** [LeetCode](https://leetcode.com/problems/course-schedule/) · 🎥 [YouTube](https://youtu.be/WAOfKpxYHR8)
**Intuition / Approach:** "Can you finish all courses?" = "is the prerequisite graph a DAG?" Build edges `pre→course`, run Kahn's; feasible iff no cycle (all nodes processed).
**Example:** `numCourses=2, prerequisites=[[1,0]]` → 0 then 1 → **true**; `[[1,0],[0,1]]` → cycle → **false**.
**Analogy:** Checking if a **degree plan** is completable — impossible if two courses each list the other as a prerequisite.

### Course Schedule II  🟡
**Links:** [LeetCode](https://leetcode.com/problems/course-schedule-ii/) · 🎥 [YouTube](https://youtu.be/WAOfKpxYHR8)
**Intuition / Approach:** Return an actual valid order (or empty if impossible). Kahn's algorithm output is that order; if its size `< numCourses`, return `[]`.
**Example:** `numCourses=4, prerequisites=[[1,0],[2,0],[3,1],[3,2]]` → order `0,1,2,3` (or `0,2,1,3`).
**Analogy:** Producing the actual **semester-by-semester study plan**, not just confirming one exists.

### Find eventual safe states  🔴
**Links:** [LeetCode](https://leetcode.com/problems/find-eventual-safe-states/) · 🎥 [YouTube](https://youtu.be/2gtg3VsDGyc)
**Intuition / Approach:** A node is safe if every path from it ends at a terminal node (never enters a cycle). Reverse the graph and run Kahn's from out-degree-0 (terminal) nodes; every node freed is safe. Return them sorted.
**Example:** Graph with a cycle `1→2→1` and terminal `0` → nodes leading only to 0 are safe; those trapped in the cycle are not.
**Analogy:** Roads that **always lead home** — a spot is safe only if every route from it eventually reaches a dead-end you want, never circling forever.

### Alien Dictionary  🔴
**Links:** [LeetCode](https://leetcode.com/problems/alien-dictionary/) · 🎥 [YouTube](https://youtu.be/U3N_je7tWAs)
**Intuition / Approach:** Compare adjacent sorted words; the first differing character gives an ordering edge `c1→c2`. Topologically sort the characters. Invalid (cycle, or prefix-after-longer-word) ⇒ no valid order.
**Example:** Words `["wrt","wrf","er","ett","rftt"]` → edges `t→f, w→e, r→t, e→r` → order `wertf`.
**Analogy:** Reconstructing an **unknown alphabet** from a sorted phonebook — each pair of neighbours reveals one "this letter comes before that" clue.

---

## Shortest Path Algorithms and Problems

### Shortest path in undirected graph with unit weights  🔴
**Links:** [Article](https://takeuforward.org/data-structure/shortest-path-in-undirected-graph-with-unit-distance-g-28/) · 🎥 [YouTube](https://www.youtube.com/watch?v=C4gxoTaI71U&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=28)
**Intuition / Approach:** All edges cost 1, so plain **BFS** from the source gives shortest distances. Initialise `dist` to ∞, `dist[src]=0`, relax on first visit.
**Example:** Chain `0-1-2-3` from 0 → distances `0,1,2,3`.
**Analogy:** Counting **subway stops** to a destination when every hop costs the same — just count the fewest hops.

### Shortest path in DAG  🔴
**Links:** [Article](https://takeuforward.org/data-structure/shortest-path-in-directed-acyclic-graph-topological-sort-g-27/) · 🎥 [YouTube](https://www.youtube.com/watch?v=ZUFQfFaU-8U&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=27)
**Intuition / Approach:** In a weighted DAG, topologically sort, then relax edges in topo order — each node is finalised once all its predecessors are processed. Linear time, works with negative weights (no cycles).
**Example:** DAG `0→1(2), 0→4(1), 4→2(2), 1→2(3)` → shortest to 2 is via `0→4→2` = 3.
**Analogy:** A **factory assembly line** — process stations in dependency order; each part's minimum cost is known once all feeder stations are done.

### Djisktra's Algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/dijkstras-algorithm-using-set-g-33/) · 🎥 [YouTube](https://www.youtube.com/watch?v=rp1SMw7HSO8&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=35)
**Intuition / Approach:** Greedy shortest path for **non-negative** weights. Maintain a min-heap (or set) keyed on tentative distance; always finalise the closest unfinalised node and relax its edges.
**Example:** `S→A(2), S→B(5), A→B(1), B→T(3)` → shortest `S→A→B→T` = 6.
**Analogy:** **Water flowing downhill** filling the nearest low point first — the closest reachable node is settled before farther ones.

### Why priority Queue is used in Djisktra's Algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/dijkstras-algorithm-using-priority-queue-g-32/) · 🎥 [YouTube](https://www.youtube.com/watch?v=rp1SMw7HSO8&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=35)
**Intuition / Approach:** A min-priority-queue always yields the currently closest node in `O(log V)`, so we never waste time re-scanning all nodes for the minimum (which a plain array would). This drops the complexity from `O(V²)` to `O(E log V)`.
**Example:** With many nodes, the heap pops `dist=2` before `dist=5` automatically, guiding correct greedy order.
**Analogy:** A **triage nurse** who always calls the most urgent patient next — the priority queue keeps the "closest/cheapest" always at the front.

### Shortest Distance in a Binary Maze  🔴
**Links:** [LeetCode](https://leetcode.com/problems/shortest-path-in-binary-matrix/) · 🎥 [YouTube](https://www.youtube.com/watch?v=U5Mw4eyUmw4&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=36)
**Intuition / Approach:** Grid with 0/1 cells; move through open cells to reach the target. Unit costs → **BFS** gives the shortest number of steps (8-directional for LeetCode 1091). Track distance per cell.
**Example:** `[[0,1],[1,0]]` from `(0,0)` to `(1,1)` diagonally → **2** cells path.
**Analogy:** A **robot vacuum** finding the fewest tile-moves across an open floor while dodging furniture (walls).

### Path with minimum effort  🔴
**Links:** [LeetCode](https://leetcode.com/problems/path-with-minimum-effort/) · 🎥 [YouTube](https://youtu.be/0ytpZyiZFhA)
**Intuition / Approach:** Minimise the **maximum** absolute height difference along a path — a modified Dijkstra where a path's "cost" is the largest edge climb, and we relax with `max(effortSoFar, |diff|)`.
**Example:** `[[1,2,2],[3,8,2],[5,3,5]]` → best path keeps max jump = **2**.
**Analogy:** Choosing a **hiking trail** that minimises the steepest single climb, not total distance — you dread the worst step, not the sum.

### Cheapest flight within K stops  🔴
**Links:** [LeetCode](https://leetcode.com/problems/cheapest-flights-within-k-stops/) · 🎥 [YouTube](https://youtu.be/9XybHVqTHcQ)
**Intuition / Approach:** Shortest path with a stop constraint. Use **level-limited BFS / Bellman-Ford**: relax edges exactly `K+1` times so paths use at most `K` intermediate stops. Track `(stops, node, cost)`.
**Example:** `n=3, flights=[[0,1,100],[1,2,100],[0,2,500]], K=1` → cheapest within 1 stop = `0→1→2` = **200**.
**Analogy:** Booking the **cheapest flight allowed at most one layover** — you accept a longer route only if it's within the layover budget.

### Network Delay Time  🟡
**Links:** [LeetCode](https://leetcode.com/problems/network-delay-time/) · [Article](https://takeuforward.org/data-structure/network-delay-time)
**Intuition / Approach:** Time for a signal from source `k` to reach all nodes = the **maximum** of Dijkstra shortest distances. If any node is unreachable, return -1.
**Example:** `times=[[2,1,1],[2,3,1],[3,4,1]], n=4, k=2` → distances `{1:1,3:1,4:2}` → answer **2**.
**Analogy:** A **rumor spreading** through an office — total time until everyone knows equals when the last (farthest) person hears it.

### Number of ways to arrive at destination  🔴
**Links:** [LeetCode](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/) · 🎥 [YouTube](https://youtu.be/_-0mx0SmYxA)
**Intuition / Approach:** Dijkstra while also counting shortest paths. Keep `ways[]`; when a strictly shorter path is found, reset `ways[v]=ways[u]`; when an equal-length path is found, add `ways[v]+=ways[u]` (mod 1e9+7).
**Example:** Multiple equal-length shortest routes to node `n-1` are summed to give the count.
**Analogy:** Counting how many **equally-fastest commutes** exist between home and office — several distinct routes may all tie for the minimum time.

### Minimum multiplications to reach end  🔴
**Links:** [Article](https://takeuforward.org/graph/g-39-minimum-multiplications-to-reach-end/) · 🎥 [YouTube](https://www.youtube.com/watch?v=_BvEJ3VIDWw&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=39)
**Intuition / Approach:** State-space BFS. Each reachable number (mod 100000) is a node; multiplying by an array element is an edge of weight 1. BFS from `start` gives the fewest multiplications to reach `end`.
**Example:** `arr=[2,5,7], start=3, end=30` → `3*2=6, 6*5=30` → **2** steps.
**Analogy:** A **combination lock of multiplications** — each allowed multiplier is a dial move; find the fewest moves to hit the target number.

### Bellman Ford Algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/bellman-ford-algorithm-g-41/) · 🎥 [YouTube](https://youtu.be/0vVofAhAYjc)
**Intuition / Approach:** Single-source shortest path allowing **negative edges**. Relax all edges `V-1` times; a further relaxation on pass `V` proves a **negative cycle**. Works on directed graphs.
**Example:** `0→1(5), 1→2(-2), 0→2(4)` → dist to 2 = `min(4, 5-2)=3`.
**Analogy:** Repeatedly **smoothing wrinkles in a tablecloth** — after enough passes (V-1) it's flat; if a wrinkle keeps reappearing, there's a self-feeding loop (negative cycle).

### Floyd warshall algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/floyd-warshall-algorithm-g-42/) · 🎥 [YouTube](https://www.youtube.com/watch?v=YbY8cVwWAvw&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=42)
**Intuition / Approach:** All-pairs shortest paths via DP. For each intermediate `k`, try improving every `(i,j)` with `dist[i][k]+dist[k][j]`. `O(V³)`. A negative value on the diagonal signals a negative cycle.
**Example:** 3-node graph → after considering each node as intermediate, `dist[i][j]` holds every pair's shortest distance.
**Analogy:** Filling a **mileage chart** between all city pairs by asking, "could routing through city k be shorter?" for every k.

### Find the city with the smallest number of neighbors  🔴
**Links:** [LeetCode](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/) · 🎥 [YouTube](https://youtu.be/9XybHVqTHcQ)
**Intuition / Approach:** Run **Floyd-Warshall** to get all-pairs distances, then for each city count how many others are within `distanceThreshold`. Return the city with the fewest such neighbours (largest index on ties).
**Example:** `n=4, threshold=4` → compute distance matrix, count reachable cities per node, pick the minimum.
**Analogy:** Finding the **most isolated town** — the one with the fewest other towns within a reasonable driving distance.

---

## MinimumSpanningTree / Disjoint Set and Problems

### MST theory  🟢
**Links:** [Article](https://takeuforward.org/data-structure/minimum-spanning-tree-theory-g-44/) · 🎥 [YouTube](https://youtu.be/ZSPjZuZWCME)
**Intuition / Approach:** An MST connects all `V` vertices with `V-1` edges at minimum total weight and no cycle. Two greedy builders: **Prim** (grow one tree) and **Kruskal** (add cheapest safe edges via DSU).
**Example:** Weighted square with a diagonal → pick the 3 lightest edges that keep it connected and acyclic.
**Analogy:** Laying **minimum cable** to connect every house in a neighbourhood without wasteful loops.

### Prim's Algorithm  🔴
**Links:** [Article](https://takeuforward.org/data-structure/prims-algorithm-minimum-spanning-tree-c-and-java-g-45/) · 🎥 [YouTube](https://youtu.be/mJcZjjKzeqk)
**Intuition / Approach:** Start from any node; use a min-heap of frontier edges. Repeatedly add the cheapest edge that reaches a new node, expanding the tree until all nodes are in. `O(E log V)`.
**Example:** From node 0, pick cheapest incident edge, then cheapest edge leaving the growing tree, etc., until all connected.
**Analogy:** **Growing a crystal** — it accretes the nearest cheapest atom to its surface at each step, expanding outward.

### Disjoint Set  🔴
**Links:** [Article](https://takeuforward.org/data-structure/disjoint-set-union-by-rank-union-by-size-path-compression-g-46/) · 🎥 [YouTube](https://youtu.be/aBxjDBC4M1U)
**Intuition / Approach:** Maintain sets with `find` (representative) and `union` (merge). Optimise with **path compression** (flatten `find` chains) and **union by rank/size** (attach smaller tree under larger). Near-`O(1)` amortised (`α(N)`).
**Example:** After `union(1,2), union(2,3)` → `find(1)==find(3)` are the same root.
**Analogy:** Merging **social clubs** — asking "are we in the same club?" and "merge our two clubs" — with a president (root) representing each club.

### Find the MST weight  🔴
**Links:** [Article](https://takeuforward.org/data-structure/prims-algorithm-minimum-spanning-tree-c-and-java-g-45/) · 🎥 [YouTube](https://youtu.be/mJcZjjKzeqk)
**Intuition / Approach:** Just return the summed weight of the MST — run Prim or Kruskal and accumulate the chosen edge weights. Both give the same total.
**Example:** Edges chosen with weights `1,2,3` for a 4-node graph → MST weight `6`.
**Analogy:** The **final bill** for the minimum cabling project — the total cost of the cheapest connecting plan.

### Number of operations to make network connected  🔴
**Links:** [LeetCode](https://leetcode.com/problems/number-of-operations-to-make-network-connected/) · 🎥 [YouTube](https://youtu.be/FYrl7iz9_ZU)
**Intuition / Approach:** With DSU, count connected components `c` and count **extra (redundant) edges** (an edge joining two already-connected nodes). You need `c-1` moves to link components; feasible iff `extra >= c-1`.
**Example:** `n=4, connections=[[0,1],[0,2],[1,2]]` → components {0,1,2} and {3}; one extra edge, need 1 → answer **1**.
**Analogy:** Re-plugging **spare network cables** — you can only rewire the redundant ones, and you need enough spares to bridge every separate island of computers.

### Most stones removed with same row or column  🟡
**Links:** [LeetCode](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/) · 🎥 [YouTube](https://youtu.be/OwMNX8SPavM)
**Intuition / Approach:** Union stones sharing a row or column (map rows/cols to DSU nodes). From each connected component you can remove all but one stone → answer = `total stones − number of components`.
**Example:** 6 stones forming 1 component → remove `6-1 = 5`.
**Analogy:** Clearing a **connected pile of magnets** — you can pluck them one by one as long as each touches the group, leaving just one anchor per separate cluster.

### Accounts merge  🔴
**Links:** [LeetCode](https://leetcode.com/problems/accounts-merge/) · 🎥 [YouTube](https://youtu.be/FMwpt_aQOGw)
**Intuition / Approach:** Emails are nodes; union accounts sharing any email. Map each email to an account index, DSU-merge on shared emails, then group emails by root, sort, and prepend the owner name.
**Example:** Two "John" accounts sharing `johnsmith@mail` merge into one; a different John stays separate.
**Analogy:** Merging **duplicate contact cards** — if two cards share a phone or email, they're the same person; combine them.

### Number of islands II  🔴
**Links:** [LeetCode](https://leetcode.com/problems/number-of-islands-ii/) · 🎥 [YouTube](https://youtu.be/Rn6B-Q4SNyA)
**Intuition / Approach:** Online queries add land cells one at a time; report island count after each. Use DSU: each new land cell starts as its own island (`count++`), then union with any adjacent land, decrementing `count` per successful merge.
**Example:** Adding cells `(0,0),(0,1),(1,1)` → counts become `1,1,1` as they connect.
**Analogy:** **Reclaiming land from the sea** — each dumped patch is a new islet, but if it touches existing land the islets fuse into fewer islands.

### Making a large island  🔴
**Links:** [LeetCode](https://leetcode.com/problems/making-a-large-island/) · 🎥 [YouTube](https://youtu.be/lgiz0Oup6gM)
**Intuition / Approach:** DSU-label every island with its size. For each `0` cell, sum the sizes of distinct neighbouring islands `+1`; the maximum over all flips (or the whole grid if no 0) is the answer.
**Example:** `[[1,0],[0,1]]` → flipping the center-ish 0 joins two size-1 islands → size **3**.
**Analogy:** Building **one land bridge** to merge the biggest possible combined island from adjacent land masses.

### Swim in Rising Water  🟡
**Links:** [LeetCode](https://leetcode.com/problems/swim-in-rising-water/) · [Article](https://takeuforward.org/data-structure/swim-in-rising-water)
**Intuition / Approach:** Find the minimum time `t` such that a path from top-left to bottom-right uses only cells with elevation `≤ t`. Solve with a Dijkstra-like min-heap minimising the path maximum, or DSU adding cells in elevation order until start and end connect.
**Example:** `[[0,2],[1,3]]` → the path max elevation to reach the corner is **3**.
**Analogy:** Waiting for a **flood to rise** just enough that you can swim across submerged cells from corner to corner — you want the earliest safe moment.

---

## Other Algorithms

### Bridges in graph  🔴
**Links:** [LeetCode](https://leetcode.com/problems/critical-connections-in-a-network/) · 🎥 [YouTube](https://youtu.be/qrAub5z8FeA)
**Intuition / Approach:** A **bridge** is an edge whose removal increases the number of components. Tarjan's DFS assigns discovery time `tin[]` and low-link `low[]`; edge `(u,v)` is a bridge when `low[v] > tin[u]` (no back-edge from v's subtree bypasses u).
**Example:** In `1-2-3` with also `1-3`, the middle edges aren't bridges (cycle), but a lone edge `3-4` is a bridge.
**Analogy:** The **only bridge to an island** — remove it and the island is cut off; a road with an alternate route is not critical.

### Articulation point in graph  🔴
**Links:** [Article](https://takeuforward.org/data-structure/articulation-point-in-graph-g-56/) · 🎥 [YouTube](https://youtu.be/j1QDfU21iZk)
**Intuition / Approach:** An **articulation point** is a vertex whose removal increases components. Tarjan's DFS: non-root `u` is one if some child `v` has `low[v] >= tin[u]`; the root is one if it has more than one DFS child.
**Example:** In a "bowtie" graph, the shared center vertex is an articulation point — cutting it splits the two loops.
**Analogy:** A **single-point-of-failure server** — if that one machine goes down, the network splits into disconnected halves.

### Kosaraju's algorithm  🔴
**Links:** [Article](https://takeuforward.org/graph/strongly-connected-components-kosarajus-algorithm-g-54/) · 🎥 [YouTube](https://www.youtube.com/watch?v=V8qIqJxCioo&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=27)
**Intuition / Approach:** Count **strongly connected components** (SCCs) in a directed graph. (1) DFS pushing nodes by finish time; (2) transpose the graph; (3) pop the stack and DFS on the transpose — each new tree is one SCC.
**Example:** `1→2→3→1` and `3→4` → `{1,2,3}` is one SCC, `{4}` another → **2 SCCs**.
**Analogy:** Finding **cliques of mutual reachability** — groups where everyone can reach everyone else and come back, like tightly-knit friend groups in a directed follow network.

---

## Problem Checklist

| # | Problem | Difficulty | Pattern | Practice link |
|---|---|---|---|---|
| 1 | Introduction to Graph | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/graph-representation-in-java) |
| 2 | Graph Representation \| C++ | 🟢 Easy | Learning | [Article](https://takeuforward.org/graph/graph-representation-in-c/) |
| 3 | Graph Representation \| Java | 🟢 Easy | Learning | [Article](https://takeuforward.org/data-structure/graph-representation-in-java) |
| 4 | Connected Components | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/connected-components) |
| 5 | Traversal Techniques | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/depth-first-search-dfs/) |
| 6 | DFS | 🟡 Medium | Learning | [Article](https://takeuforward.org/data-structure/depth-first-search-dfs/) |
| 7 | Number of provinces | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/number-of-provinces/) |
| 8 | Connected Components Problem in Matrix | 🟡 Medium | BFS/DFS | [Article](https://takeuforward.org/data-structure/connected-components) |
| 9 | Rotten Oranges | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/rotting-oranges/) |
| 10 | Flood fill algorithm | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/flood-fill/) |
| 11 | Cycle Detection in Undirected Graph (bfs) | 🔴 Hard | BFS/DFS | [Article](https://takeuforward.org/data-structure/detect-cycle-in-an-undirected-graph-using-bfs/) |
| 12 | Detect a cycle in an undirected graph | 🔴 Hard | BFS/DFS | [LeetCode](https://leetcode.com/problems/course-schedule/) |
| 13 | Distance of nearest cell having one | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/01-matrix/) |
| 14 | Surrounded Regions | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/surrounded-regions/) |
| 15 | Number of enclaves | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/number-of-enclaves/) |
| 16 | Word ladder I | 🔴 Hard | BFS/DFS | [LeetCode](https://leetcode.com/problems/word-ladder/) |
| 17 | Word ladder II | 🔴 Hard | BFS/DFS | [LeetCode](https://leetcode.com/problems/word-ladder-ii/) |
| 18 | Number of islands | 🟡 Medium | BFS/DFS | [LeetCode](https://leetcode.com/problems/number-of-islands/) |
| 19 | Bipartite Graph (DFS) | 🔴 Hard | BFS/DFS | [LeetCode](https://leetcode.com/problems/is-graph-bipartite/) |
| 20 | Cycle Detection in Directed Graph (DFS) | 🔴 Hard | BFS/DFS | [LeetCode](https://leetcode.com/problems/course-schedule-ii/) |
| 21 | Topo Sort | 🔴 Hard | Topo Sort | [Article](https://takeuforward.org/data-structure/topological-sort-algorithm-dfs-g-21/) |
| 22 | Topological sort or Kahn's algorithm | 🔴 Hard | Topo Sort | [Article](https://takeuforward.org/data-structure/topological-sort-algorithm-dfs-g-21/) |
| 23 | Detect a cycle in a directed graph | 🔴 Hard | Topo Sort | [LeetCode](https://leetcode.com/problems/course-schedule/) |
| 24 | Course Schedule I | 🔴 Hard | Topo Sort | [LeetCode](https://leetcode.com/problems/course-schedule/) |
| 25 | Course Schedule II | 🟡 Medium | Topo Sort | [LeetCode](https://leetcode.com/problems/course-schedule-ii/) |
| 26 | Find eventual safe states | 🔴 Hard | Topo Sort | [LeetCode](https://leetcode.com/problems/find-eventual-safe-states/) |
| 27 | Alien Dictionary | 🔴 Hard | Topo Sort | [LeetCode](https://leetcode.com/problems/alien-dictionary/) |
| 28 | Shortest path in undirected graph with unit weights | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/shortest-path-in-undirected-graph-with-unit-distance-g-28/) |
| 29 | Shortest path in DAG | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/shortest-path-in-directed-acyclic-graph-topological-sort-g-27/) |
| 30 | Djisktra's Algorithm | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/dijkstras-algorithm-using-set-g-33/) |
| 31 | Why priority Queue is used in Djisktra's Algorithm | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/dijkstras-algorithm-using-priority-queue-g-32/) |
| 32 | Shortest Distance in a Binary Maze | 🔴 Hard | Shortest Path | [LeetCode](https://leetcode.com/problems/shortest-path-in-binary-matrix/) |
| 33 | Path with minimum effort | 🔴 Hard | Shortest Path | [LeetCode](https://leetcode.com/problems/path-with-minimum-effort/) |
| 34 | Cheapest flight within K stops | 🔴 Hard | Shortest Path | [LeetCode](https://leetcode.com/problems/cheapest-flights-within-k-stops/) |
| 35 | Network Delay Time | 🟡 Medium | Shortest Path | [LeetCode](https://leetcode.com/problems/network-delay-time/) |
| 36 | Number of ways to arrive at destination | 🔴 Hard | Shortest Path | [LeetCode](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/) |
| 37 | Minimum multiplications to reach end | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/graph/g-39-minimum-multiplications-to-reach-end/) |
| 38 | Bellman Ford Algorithm | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/bellman-ford-algorithm-g-41/) |
| 39 | Floyd warshall algorithm | 🔴 Hard | Shortest Path | [Article](https://takeuforward.org/data-structure/floyd-warshall-algorithm-g-42/) |
| 40 | Find the city with the smallest number of neighbors | 🔴 Hard | Shortest Path | [LeetCode](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/) |
| 41 | MST theory | 🟢 Easy | MST/DSU | [Article](https://takeuforward.org/data-structure/minimum-spanning-tree-theory-g-44/) |
| 42 | Prim's Algorithm | 🔴 Hard | MST/DSU | [Article](https://takeuforward.org/data-structure/prims-algorithm-minimum-spanning-tree-c-and-java-g-45/) |
| 43 | Disjoint Set | 🔴 Hard | MST/DSU | [Article](https://takeuforward.org/data-structure/disjoint-set-union-by-rank-union-by-size-path-compression-g-46/) |
| 44 | Find the MST weight | 🔴 Hard | MST/DSU | [Article](https://takeuforward.org/data-structure/prims-algorithm-minimum-spanning-tree-c-and-java-g-45/) |
| 45 | Number of operations to make network connected | 🔴 Hard | MST/DSU | [LeetCode](https://leetcode.com/problems/number-of-operations-to-make-network-connected/) |
| 46 | Most stones removed with same row or column | 🟡 Medium | MST/DSU | [LeetCode](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/) |
| 47 | Accounts merge | 🔴 Hard | MST/DSU | [LeetCode](https://leetcode.com/problems/accounts-merge/) |
| 48 | Number of islands II | 🔴 Hard | MST/DSU | [LeetCode](https://leetcode.com/problems/number-of-islands-ii/) |
| 49 | Making a large island | 🔴 Hard | MST/DSU | [LeetCode](https://leetcode.com/problems/making-a-large-island/) |
| 50 | Swim in Rising Water | 🟡 Medium | MST/DSU | [LeetCode](https://leetcode.com/problems/swim-in-rising-water/) |
| 51 | Bridges in graph | 🔴 Hard | Other | [LeetCode](https://leetcode.com/problems/critical-connections-in-a-network/) |
| 52 | Articulation point in graph | 🔴 Hard | Other | [Article](https://takeuforward.org/data-structure/articulation-point-in-graph-g-56/) |
| 53 | Kosaraju's algorithm | 🔴 Hard | Other | [Article](https://takeuforward.org/graph/strongly-connected-components-kosarajus-algorithm-g-54/) |
