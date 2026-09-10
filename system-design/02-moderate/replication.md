# Replication

> Difficulty: 🔵 Moderate

## TL;DR

Replication keeps copies of the same data on multiple machines so that a system can survive failures, serve reads from nearby nodes, and scale read throughput. The core design decisions are *where* writes are accepted (single leader, multiple leaders, or no leader) and *when* replicas are considered up to date (synchronous vs. asynchronous), and every choice trades consistency against availability and latency.

## Overview

A single database node is a single point of failure and a hard ceiling on throughput. Replication solves three distinct problems at once:

- **High availability / fault tolerance** — if one node dies, another already has the data and can take over.
- **Read scalability** — spread read traffic across many copies instead of hammering one machine.
- **Locality / latency** — put a copy geographically close to users to cut round-trip time.

The hard part is not copying data once; it is keeping copies consistent *while writes keep arriving* and while nodes and networks fail. That tension — consistency vs. availability vs. latency — is what interviewers probe. Replication is the mechanism behind read replicas, cross-region deployments, and most highly available data stores, so it shows up in almost every system design discussion.

## Key Concepts

- **Replica / node:** A machine holding a copy of the dataset.
- **Leader (primary/master):** The node that accepts writes and is the source of truth in leader-based schemes.
- **Follower (replica/secondary/standby):** A node that receives changes from a leader and typically serves reads.
- **Replication log:** The ordered stream of changes (statement-based, write-ahead log shipping, or logical/row-based) shipped from leader to followers.
- **Synchronous replication:** Leader waits for one or more followers to acknowledge a write before confirming to the client. Stronger durability, higher latency.
- **Asynchronous replication:** Leader confirms immediately and propagates changes in the background. Lower latency, risk of data loss on failover.
- **Semi-synchronous:** At least one follower must acknowledge; the rest are async. A common middle ground.
- **Replication lag:** The delay between a write committing on the leader and being visible on a follower.
- **Quorum (W, R, N):** In leaderless systems, `N` = replicas per item, `W` = replicas that must ack a write, `R` = replicas read from. `W + R > N` gives strong overlap.
- **Failover:** Promoting a follower to leader when the leader fails.
- **Split-brain:** Two nodes both believe they are leader and accept conflicting writes.
- **Read-your-writes / monotonic reads:** Consistency guarantees that mitigate the confusing effects of lag.

## How It Works

In the most common model, **leader-follower (primary-replica)**, all writes go to the leader. The leader appends the change to a replication log and streams it to followers, which apply the changes in the same order. Reads can be served by any node.

```mermaid
flowchart LR
    Client[Client Writes] --> Leader[(Leader)]
    ReadA[Client Reads] --> F1[(Follower 1)]
    ReadB[Client Reads] --> F2[(Follower 2)]
    Leader -- replication log --> F1
    Leader -- replication log --> F2
    Leader -- replication log --> F3[(Follower N)]
```

The synchronous vs. asynchronous decision determines *when the client hears "OK"* relative to follower acknowledgement:

```mermaid
sequenceDiagram
    participant C as Client
    participant L as Leader
    participant F as Follower
    Note over C,F: Synchronous
    C->>L: write(x=1)
    L->>F: replicate(x=1)
    F-->>L: ack
    L-->>C: OK (durable on 2 nodes)
    Note over C,F: Asynchronous
    C->>L: write(x=2)
    L-->>C: OK (may be lost if leader dies)
    L->>F: replicate(x=2)
```

On leader failure, a **failover** process runs: detect the failure (usually a timeout/heartbeat), choose the most up-to-date follower, and reroute clients. This is where async replication bites — any writes that hadn't reached the new leader are lost.

## Types / Patterns / Strategies

| Pattern | Where writes go | Conflict handling | Typical use |
| --- | --- | --- | --- |
| **Leader-follower (single-leader)** | One leader only | No conflicts (single write path) | Most relational DBs, default choice |
| **Multi-leader** | Multiple leaders (often per region) | Must resolve write conflicts | Multi-datacenter, offline-capable apps |
| **Leaderless (quorum)** | Any replica | Version vectors / read repair / hinted handoff | High-availability KV stores |

**Replication log formats:**
- *Statement-based:* ships the SQL; fragile with `NOW()`, `RAND()`, auto-increment.
- *Write-ahead log (WAL) shipping:* ships low-level byte changes; tightly couples storage versions.
- *Logical (row-based):* ships row changes; version-independent and the modern default (e.g., MySQL row-based binlog, Postgres logical replication).

**Conflict resolution (multi-leader / leaderless):** Last-Write-Wins (LWW, lossy), version vectors, CRDTs, or application-level merge (like Git).

## When to Use / When to Avoid

**Use single-leader replication when:**
- You need strong consistency and simple semantics.
- Read load dominates write load (add read replicas).
- One region is sufficient for write latency.

**Use multi-leader when:**
- You have multiple datacenters and need low write latency in each.
- You need offline writes (mobile apps, collaborative editors) that sync later.
- You can tolerate and resolve write conflicts.

**Use leaderless when:**
- Availability during node failures matters more than strict consistency.
- Writes must never block on a single node.
- The workload tolerates eventual consistency and tunable quorums.

**Avoid / be careful when:**
- You add replicas expecting *write* scaling — single-leader does not scale writes; you need sharding for that.
- The app reads immediately after writing and can't tolerate lag (needs read-your-writes routing).
- You enable full synchronous replication across regions — WAN latency will dominate every write.

## Trade-offs

| Pros | Cons |
| --- | --- |
| Fault tolerance — survive node/DC loss | Consistency is hard; lag causes stale reads |
| Read scalability via read replicas | Does not scale writes (except leaderless/sharding) |
| Lower read latency with geo-local replicas | Async replication risks data loss on failover |
| Enables zero/low-downtime maintenance | Failover is error-prone (split-brain, lost writes) |
| Sync replication gives strong durability | Sync adds write latency and reduces availability |
| Multi-leader enables offline & multi-region writes | Multi-leader/leaderless require conflict resolution |

## Real-World Examples

- **PostgreSQL** — streaming replication (WAL), synchronous and async modes, logical replication for selective/cross-version replication.
- **MySQL** — binlog replication (row/statement based); powers read-replica fleets everywhere; Group Replication for HA.
- **Amazon Aurora / RDS Read Replicas** — up to 15 low-lag read replicas sharing a distributed storage layer; multi-AZ failover.
- **Amazon DynamoDB & Apache Cassandra** — leaderless, quorum-based (tunable `W`/`R`), hinted handoff and read repair. DynamoDB Global Tables use multi-region multi-leader with LWW.
- **MongoDB** — replica sets with a single primary, automatic election-based failover (Raft-like).
- **Apache Kafka** — partition leaders + follower replicas with an in-sync-replica (ISR) set; `acks=all` is effectively synchronous durability.
- **Redis** — async primary-replica replication with Sentinel/Cluster for failover.
- **etcd / ZooKeeper / Consul** — consensus-based (Raft/Zab) replication for strongly consistent metadata.

## Common Pitfalls

- **Reading your own write from a lagging follower** and seeing stale data (e.g., user updates profile, refresh shows the old value). Fix with read-your-writes routing.
- **Assuming replicas scale writes.** They don't — all writes still funnel through the leader. Sharding scales writes.
- **Full synchronous replication everywhere**, which means one slow follower blocks all writes and reduces availability. Use semi-sync instead.
- **Ignoring split-brain during failover.** Without fencing (STONITH, leases, quorum), two leaders accept divergent writes.
- **Trusting Last-Write-Wins.** LWW silently discards concurrent writes; clock skew makes "last" ambiguous.
- **Unbounded replication lag** under write spikes or long-running follower queries, causing cascading staleness.
- **Not monitoring lag.** Lag is invisible until a customer complains; it must be a first-class metric with alerts.

## Interview Questions & Answers

**Q: What's the difference between synchronous and asynchronous replication, and which would you choose?**
**A:** Synchronous means the leader waits for follower acknowledgement before confirming the write, guaranteeing the data exists on ≥2 nodes but adding latency and reducing availability (a down follower blocks writes). Asynchronous confirms immediately and replicates in the background — fast and highly available, but writes can be lost if the leader fails before propagating. In practice most systems use **semi-synchronous**: one follower is synchronous (durability guarantee) and the rest are async (performance). I'd choose based on the cost of losing a recent write vs. the latency budget.

**Q: How do read replicas help scaling, and what's their key limitation?**
**A:** They offload read traffic from the leader, so a read-heavy workload can scale horizontally by adding followers. The key limitation is that they **don't scale writes** — every write still goes through the single leader — and they introduce **replication lag**, so reads may be stale. For write scaling you need sharding/partitioning.

**Q: What is replication lag and how do you deal with the "read-your-own-writes" problem?**
**A:** Lag is the delay between a write committing on the leader and appearing on a follower. To guarantee read-your-writes: route a user's reads to the leader for a short window after they write, track a per-user timestamp/log-sequence-number and only read from replicas that have caught up to it, or pin the user's session to the leader. Related guarantees are monotonic reads (never go backwards in time) and consistent-prefix reads.

**Q: Compare single-leader, multi-leader, and leaderless replication.**
**A:** Single-leader has one write node — simple, no write conflicts, strong consistency, but a write bottleneck and failover complexity. Multi-leader allows writes in multiple locations (great for multi-region/offline) but requires conflict resolution because two leaders can accept conflicting writes. Leaderless (Dynamo-style) lets any replica take writes and uses quorums (`W + R > N`) plus read repair and hinted handoff for consistency — maximizes availability but pushes conflict handling (version vectors) to the system/app.

**Q: In a quorum system with N=3, what W and R give strong consistency, and what's the trade-off?**
**A:** Strong consistency requires `W + R > N`, so the read and write quorums overlap on at least one up-to-date replica. With N=3, common choices are W=2, R=2 (balanced), or W=3,R=1 (fast reads, slow/less-available writes), or W=1,R=3 (fast writes, slow reads). Lower W or R improves latency and availability but risks reading stale data; you tune per workload.

**Q: What is split-brain and how do you prevent it during failover?**
**A:** Split-brain is when two nodes both believe they're the leader and accept conflicting writes — usually after a network partition where the old leader wasn't truly dead. Prevention: require a **quorum/majority** to elect a leader (so a minority partition can't self-promote), use **fencing tokens** or leases so the old leader is rejected when it returns, and STONITH ("shoot the other node in the head") to forcibly isolate the suspected-dead node. Consensus protocols like Raft build this in.

**Q: A user updates their profile picture but still sees the old one after refresh. What's happening and how do you fix it?**
**A:** Classic replication-lag / stale-read issue: the write hit the leader, but the refresh read hit a follower that hasn't applied it yet. Fixes: route reads to the leader briefly after a write, track the write's log position and only serve the read from a caught-up replica, or use sticky sessions. It's a read-your-writes consistency problem, not a bug in the write path.

**Q: How does Kafka's ISR (in-sync replicas) model relate to sync vs. async replication?**
**A:** Each Kafka partition has a leader and follower replicas; the ISR set is the followers currently caught up. With `acks=all`, a produce request is acknowledged only after all ISR members replicate it — effectively synchronous durability scoped to the ISR. `min.insync.replicas` sets the floor, so you balance durability (more replicas must ack) against availability (fewer available replicas can stall writes). It's a tunable semi-synchronous design.

## Further Reading

- Martin Kleppmann, *Designing Data-Intensive Applications* — Chapter 5 (Replication) is the canonical treatment.
- DeCandia et al., *"Dynamo: Amazon's Highly Available Key-value Store"* (2007) — foundational leaderless/quorum paper.
- Ongaro & Ousterhout, *"In Search of an Understandable Consensus Algorithm (Raft)"* (2014) — leader election and consistent replication.
- PostgreSQL documentation — *"High Availability, Load Balancing, and Replication"*.
- Apache Kafka documentation — *"Replication"* and *"Designing for Durability"*.
