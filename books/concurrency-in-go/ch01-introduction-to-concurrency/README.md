# Chapter 1 — An Introduction to Concurrency

> Book: *Concurrency in Go* (Katherine Cox-Buday, O'Reilly 2017) · Chapter 1
> 🏠 [Book index](../README.md) · ➡️ Next chapter: [Ch 2 — Modeling Your Code: CSP](../ch02-modeling-your-code-csp/README.md)

## Overview

Chapter 1 answers three questions: *why* did concurrency become unavoidable, *why* is it so hard to get right, and *why* does Go make it better anyway. The historical arc runs from **Moore's Law** stalling (~2012) → **multicore** CPUs → **Amdahl's Law** capping parallel gains → **cloud computing** making **horizontal scaling** cheap → **web scale** software and its new complexity, with Herb Sutter's 2005 "The Free Lunch Is Over" as the turning point. The chapter then catalogs the canonical ways concurrent code goes wrong, split into two classes. **Correctness problems** (never give a wrong answer): **race conditions / data races**, **atomicity**, and **memory access synchronization** (critical sections guarded by mutexes). **Liveness problems** (always have useful work to do): **deadlock** (and the four **Coffman Conditions**), **livelock** (the busy-but-stuck hallway shuffle), and **starvation** (greedy vs polite workers). Beneath all of them is the hardest factor — **people**: communicating who owns concurrency and synchronization, via verbose comments or (better) signatures. The chapter closes on hope: Go's **low-latency concurrent GC**, **automatic goroutine-to-thread multiplexing**, and **composable channels** make the clear path also the correct and performant one — you write a function and prepend `go`.

## Chapter mind map

```mermaid
mindmap
  root(("Ch 1: Intro to Concurrency"))
    Why it matters
      Moore's Law stalls ~2012
      Multicore CPUs
      Amdahl's Law (serial fraction caps speedup)
      Cloud + horizontal scaling
      Web scale
      Free Lunch Is Over (Sutter 2005)
    Correctness problems
      Race conditions / data races
      Atomicity (context, i++ is 3 steps)
      Memory access synchronization (critical sections, mutex)
    Liveness problems
      Deadlock (Coffman conditions)
      Livelock (hallway shuffle)
      Starvation (greedy vs polite)
    The human factor
      Who owns concurrency
      How mapped to primitives
      Who owns synchronization
    Go's hope
      Low-latency concurrent GC
      Goroutines multiplexed onto threads
      Composable channels
```

## How the problems relate

```mermaid
flowchart TD
    H["Concurrency is hard"] --> C["Correctness class"]
    H --> L["Liveness class"]
    C --> RC["Race conditions"]
    C --> AT["Atomicity"]
    C --> MS["Memory access synchronization"]
    RC --> AT
    AT --> MS
    L --> DL["Deadlock"]
    L --> LL["Livelock"]
    L --> ST["Starvation"]
    LL -->|"special case of"| ST
    MS -->|"coarse vs fine lock<br/>tradeoff"| ST
    H --> P["People: concurrency safety"]
    P --> GO["Go's primitives make it tractable"]
    classDef corr fill:#e8f0ff,stroke:#3366cc
    classDef live fill:#fff0e6,stroke:#e67300
    class RC,AT,MS corr
    class DL,LL,ST live
```

## Mini-chapters

| # | Mini-chapter | One-line summary |
|---|---|---|
| 1 | [Moore's Law, Web Scale, and the Mess](01-moores-law-web-scale-and-the-mess.md) | Why multicore + Amdahl's Law + cloud/web scale made concurrency mandatory (Sutter's "free lunch is over"). |
| 2 | [Race Conditions](02-race-conditions.md) | Missing ordering guarantees → data races; why `time.Sleep` never fixes them; target logical correctness. |
| 3 | [Atomicity](03-atomicity.md) | Atomic = indivisible + uninterruptible *within a context*; `i++` is three steps; combining atomics isn't atomic. |
| 4 | [Memory Access Synchronization](04-memory-access-synchronization.md) | Critical sections and mutexes remove data races but not race conditions; granularity and convention costs. |
| 5 | [Deadlocks & the Coffman Conditions](05-deadlocks-and-coffman-conditions.md) | All processes wait forever; the four Coffman Conditions; break one (lock ordering) to prevent it. |
| 6 | [Livelocks](06-livelocks.md) | Busy but stuck — the hallway shuffle; caused by uncoordinated deadlock avoidance; cure with coordination/jitter. |
| 7 | [Starvation](07-starvation.md) | Can't get needed resources; greedy vs polite workers; detect with a work-rate metric; fine vs coarse locking. |
| 8 | [Determining Concurrency Safety](08-determining-concurrency-safety.md) | The people problem: communicate who owns concurrency/sync via verbose comments or clearer signatures. |
| 9 | [Simplicity in the Face of Complexity](09-simplicity-in-the-face-of-complexity.md) | Go's GC, goroutine-to-thread multiplexing, and channels make the clear path correct and fast — just prepend `go`. |

## Verified Go programs

All programs for this chapter were written to `/tmp/cig/verify/ch1/` and run with `go run` (Go 1.27). The race detector (`-race`) requires cgo and a C compiler that were unavailable in the verification sandbox, so race-demonstrating programs were verified with plain `go run`; where a program *intentionally* races or deadlocks, that is stated in the notes.

| Program | Demonstrates | Result |
|---|---|---|
| `amdahl/` | Amdahl's Law speedup ceiling | speedup flattens/regresses past core count ✅ |
| `race/` | unsynchronized data race | runs; one of three legal outcomes printed ✅ |
| `atomic/` | lost updates vs `atomic.Int64` | unsafe=84475 vs expected/atomic=100000 ✅ |
| `memsync/` | mutex-guarded critical sections | runs clean; ordering still nondeterministic ✅ |
| `deadlock/` | classic lock-order deadlock | `fatal error: all goroutines are asleep - deadlock!` (expected) ✅ |
| `deadlockfix/` | breaking Circular Wait via lock ordering | prints `sum=7` twice ✅ |
| `livelock/` | hallway-shuffle livelock | both "toss their hands up" — no progress ✅ |
| `starvation/` | greedy vs polite workers | greedy ≈2.2× polite loops ✅ |
| `safety/` | channel-returning API contract | prints `01234567` ✅ |
| `simplicity/` | one goroutine per connection | all clients handled; clean shutdown ✅ |
