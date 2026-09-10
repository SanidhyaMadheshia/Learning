# Graphs — Resources & References

**Nav:** [Theory & Patterns](./theory-and-patterns.md) · [Problems](./problems.md) · [Resources](./resources.md)

---

## 📺 Videos & Playlists

- [Striver's Graph Series — takeUforward (full playlist)](https://www.youtube.com/playlist?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn) — the definitive A2Z graph playlist covering every problem in this sheet, in order.
- [Introduction to Graphs & Representation — Striver](https://youtu.be/3oI-34aPMWM) — vertices, edges, directed/undirected, adjacency list vs matrix.
- [BFS & DFS traversal — Striver](https://youtu.be/Qzf1a--rhp8) — the two core traversals with dry runs.
- [Topological Sort (DFS & Kahn's) — Striver](https://youtu.be/5lZ0iJMrUMk) — ordering DAGs and detecting cycles.
- [Dijkstra's Algorithm — Striver](https://www.youtube.com/watch?v=rp1SMw7HSO8&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=35) — priority-queue and set implementations.
- [Bellman-Ford Algorithm — Striver](https://youtu.be/0vVofAhAYjc) — negative edges and negative-cycle detection.
- [Floyd-Warshall Algorithm — Striver](https://www.youtube.com/watch?v=YbY8cVwWAvw&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=42) — all-pairs shortest paths.
- [Disjoint Set (Union by Rank/Size + Path Compression) — Striver](https://youtu.be/aBxjDBC4M1U) — the DSU data structure from scratch.
- [Minimum Spanning Tree theory & Prim's — Striver](https://youtu.be/ZSPjZuZWCME) — MST fundamentals and Prim's implementation.
- [Kosaraju's Algorithm (SCC) — Striver](https://www.youtube.com/watch?v=V8qIqJxCioo&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=27) — strongly connected components.
- [Bridges in a Graph (Tarjan) — Striver](https://youtu.be/qrAub5z8FeA) — tin/low discovery-time technique.

## 📝 Articles & Tutorials

- [Striver Graph Series — Top Graph Interview Questions (index)](https://takeuforward.org/graph/striver-graph-series-top-graph-interview-questions) — the master article linking every graph topic.
- [Strivers A2Z DSA Course/Sheet](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the full structured sheet this package follows.
- [cp-algorithms: Dijkstra (dense & sparse)](https://cp-algorithms.com/graph/dijkstra.html) — rigorous treatment with proofs; see also [Dijkstra on sparse graphs](https://cp-algorithms.com/graph/dijkstra_sparse.html).
- [cp-algorithms: Bellman-Ford](https://cp-algorithms.com/graph/bellman_ford.html) — negative weights and cycle detection.
- [cp-algorithms: Floyd-Warshall (all-pairs)](https://cp-algorithms.com/graph/all-pair-shortest-path-floyd-warshall.html) — DP formulation and edge cases.
- [cp-algorithms: Disjoint Set Union](https://cp-algorithms.com/data_structures/disjoint_set_union.html) — DSU with every optimisation and applications.
- [cp-algorithms: Kruskal's MST with DSU](https://cp-algorithms.com/graph/mst_kruskal_with_dsu.html) — Kruskal built on union-find; also [plain Kruskal](https://cp-algorithms.com/graph/mst_kruskal.html).
- [GeeksforGeeks: Shortest Path Algorithms — Complete Guide](https://www.geeksforgeeks.org/dsa/shortest-path-algorithms-a-complete-guide/) — side-by-side BFS/Dijkstra/Bellman-Ford/Floyd-Warshall.
- [Tech Interview Handbook: Graph cheatsheet](https://www.techinterviewhandbook.org/algorithms/graph/) — concise interview-focused patterns (matrix-as-graph, pitfalls).
- [LeetCode Discuss: Graph algorithms + problems to practice](https://leetcode.com/discuss/study-guide/1326900/Graph-algorithms-+-problems-to-practice) — curated study guide grouping graph problems by technique.

## 🧮 Visualizers & Tools

- [VisuAlgo — Graph Traversal (DFS/BFS)](https://visualgo.net/en/dfsbfs) — animate DFS/BFS, bipartite check, and cut vertices/bridges on your own graphs.
- [VisuAlgo — Single-Source Shortest Paths](https://visualgo.net/en/sssp) — step through BFS, Dijkstra, Bellman-Ford, and DAG shortest paths.
- [VisuAlgo — main page (MST, SSSP, Max Flow, etc.)](https://www.visualgo.net/) — the full suite of graph visualizations with custom input.
- [see-algorithms: Dijkstra's Algorithm Visualizer](https://see-algorithms.com/graph/Dijkstras) — interactive priority-queue-driven shortest path animation.

## ❓ Most-Asked Interview Questions

1. **When do you use BFS vs DFS?** BFS for shortest paths in unweighted graphs and level-order/multi-source spread; DFS for reachability, cycle detection, topological sort, and connectivity. Both are O(V+E).
2. **How do you detect a cycle in an undirected graph vs a directed graph?** Undirected: DFS/BFS tracking the `parent` — a visited non-parent neighbour is a cycle. Directed: DFS with a recursion-stack `pathVisited[]` — revisiting a node currently on the stack is a cycle (or use Kahn's and check output size < V).
3. **Why can't Dijkstra handle negative edge weights?** Its greedy invariant "the popped minimum is finalised" breaks when a later negative edge could reduce an already-finalised distance. Use Bellman-Ford instead.
4. **How does Bellman-Ford detect a negative cycle?** After relaxing all edges V-1 times (enough for any simple shortest path), a V-th relaxation that still improves a distance proves a reachable negative cycle.
5. **When would you choose Floyd-Warshall over running Dijkstra from each node?** For small, dense graphs needing all-pairs distances: Floyd-Warshall is a simple O(V³) with tiny constants and handles negative edges (no negative cycles). V Dijkstras cost O(V·E log V).
6. **What is a topological sort and when does it exist?** A linear ordering of a DAG where every edge points forward. It exists iff the directed graph has no cycle; Kahn's algorithm produces one and detects cycles simultaneously.
7. **Explain the Disjoint Set Union optimisations.** Path compression flattens the tree during `find`; union by rank/size attaches the smaller tree under the larger. Together they give near-constant O(α(N)) amortised per operation.
8. **Difference between Prim's and Kruskal's MST algorithms?** Prim grows a single tree from a start node using a min-heap of frontier edges (O(E log V)), better for dense graphs. Kruskal sorts all edges and adds the cheapest that doesn't form a cycle using DSU (O(E log E)), better for sparse/edge-list input.
9. **How do you find shortest path with at most K stops?** Level-bounded relaxation: a Bellman-Ford-style loop run K+1 times, or a BFS carrying `(node, stops, cost)` — do not finalise nodes greedily because a longer-in-stops path may be cheaper.
10. **What is a bridge and an articulation point?** A bridge is an edge whose removal disconnects the graph; an articulation point is such a vertex. Both are found with Tarjan's DFS using `tin[]` (discovery time) and `low[]` (lowest reachable time): bridge iff `low[v] > tin[u]`; articulation iff `low[v] >= tin[u]` for a child (root special case: >1 child).
11. **What are strongly connected components and how do you find them?** Maximal subsets of a directed graph where every vertex reaches every other. Kosaraju: DFS by finish time, transpose the graph, DFS again popping the finish-order stack — each new tree is one SCC. O(V+E).
12. **How is a grid treated as a graph?** Each cell is a node; edges connect the 4 (or 8) adjacent in-bounds cells. Use direction arrays and BFS/DFS. Islands, rotten oranges, flood fill, and 0/1 matrix are all grid-graph problems.
13. **How do you count/return shortest paths, not just the distance?** Run Dijkstra/BFS while maintaining a `ways[]` count: on a strictly shorter path reset the count, on an equal-length path add the predecessor's count (usually modulo 1e9+7).
14. **What makes a graph bipartite and how do you test it?** A graph is bipartite iff it has no odd-length cycle. Test by 2-coloring via BFS/DFS; a conflict (adjacent nodes sharing a color) means it is not bipartite.
15. **Adjacency list vs adjacency matrix — trade-offs?** List: O(V+E) space, O(deg) neighbour iteration — ideal for sparse graphs (most problems). Matrix: O(V²) space, O(1) edge lookup — good for dense graphs and Floyd-Warshall.

## 📚 Books & Courses

- **CLRS — *Introduction to Algorithms*** (Cormen, Leiserson, Rivest, Stein): Ch. 20 Elementary Graph Algorithms (BFS/DFS/topo sort/SCC), Ch. 21 Minimum Spanning Trees (Kruskal/Prim), Ch. 22 Single-Source Shortest Paths (Bellman-Ford/Dijkstra/DAG), Ch. 23 All-Pairs Shortest Paths (Floyd-Warshall). *(Chapter numbers per the 4th edition.)*
- **Sedgewick & Wayne — *Algorithms* (4th ed.)**: Chapter 4 "Graphs" (undirected/directed graphs, MST, shortest paths) with clear Java implementations.
- [USACO Guide — Graph section](https://usaco.guide/CPH.pdf) (Competitive Programmer's Handbook by Antti Laaksonen, free PDF): graph theory chapters with contest-oriented explanations.
- Local library cross-link: [`../../../books/`](../../../books/) — check for CLRS / algorithm texts stored in this repo.

## 🔗 Official Problem Sources

- [takeUforward — Strivers A2Z DSA Sheet (Step 15: Graphs)](https://takeuforward.org/dsa/strivers-a2z-sheet-learn-dsa-a-to-z) — the official sheet page.
- [takeUforward — Striver Graph Series (topic index)](https://takeuforward.org/graph/striver-graph-series-top-graph-interview-questions) — per-problem articles.
- [LeetCode — Graph tag](https://leetcode.com/tag/graph/) — all graph-tagged problems.
- [LeetCode — Breadth-First Search tag](https://leetcode.com/tag/breadth-first-search/) · [Depth-First Search tag](https://leetcode.com/tag/depth-first-search/)
- [LeetCode — Union Find tag](https://leetcode.com/tag/union-find/) · [Shortest Path tag](https://leetcode.com/tag/shortest-path/) · [Topological Sort tag](https://leetcode.com/tag/topological-sort/) · [Minimum Spanning Tree tag](https://leetcode.com/tag/minimum-spanning-tree/)
- [LeetCode — Graph Theory I study plan](https://leetcode.com/studyplan/graph-theory/) — guided practice covering traversal, DSU, and shortest paths.
