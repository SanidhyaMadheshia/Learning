# vLLM & llm-d — Complete Event Prep Guide

*A zero-to-medium learning doc for the "Engine Room of vLLM and llm-d AI Inferencing" meetup.*
*Written for someone who currently knows nothing about LLMs but is technically comfortable (infra / backend background).*

---

## How to use this doc

Read it top to bottom **once** the night before. Each part builds on the previous one:

1. **Part 0** — the 5-minute "walk in confident" summary.
2. **Parts 1–3** — the actual learning: foundations → vLLM (the engine) → llm-d (scaling it).
3. **Part 4** — summary of the YouTube video you shared.
4. **Part 5** — every talk on the agenda decoded, with smart questions to ask.
5. **Part 6** — the full open-source stack list (what's "going in").
6. **Part 7** — glossary. **Part 8** — logistics + questions.

If you only have 10 minutes: read Part 0, the glossary (Part 7), and Part 5.

---

## Part 0 — The 5-Minute Version (read this first)

**The one-sentence mental model:**
> An **LLM** is a huge math function that predicts the next word. Running it to answer a request is called **inference**. **vLLM** is the open-source software that runs one model *fast on a GPU*. **llm-d** is the open-source software that runs *many copies of vLLM across a whole GPU cluster on Kubernetes* so you can serve millions of users.

**The stack, bottom to top:**

```
Your prompt
   │
   ▼
[ llm-d ]      ← Kubernetes-native "traffic director" across the whole GPU fleet
   │             (smart routing, autoscaling, splitting work across machines)
   ▼
[ vLLM ]       ← the inference ENGINE running on each GPU node
   │             (makes a single model fast & memory-efficient)
   ▼
[ GPU(s) ]     ← NVIDIA (CUDA) or AMD (ROCm) hardware that does the math
```

**The 6 words that will be said 100 times — know these cold:**

| Term | Plain meaning |
|---|---|
| **Inference** | Running an already-trained model to get an answer (not training it). |
| **Token** | A chunk of text (~¾ of a word). Models read and write tokens, not letters. |
| **KV cache** | The model's "short-term memory" of the conversation so far, stored in GPU memory. Grows with every token. The #1 thing everyone fights over. |
| **Prefill vs Decode** | Two phases of a request: **prefill** = read your whole prompt at once (fast, compute-heavy); **decode** = generate the answer one token at a time (slow, memory-heavy). |
| **Throughput vs Latency** | Throughput = total tokens/sec across all users. Latency = how fast *one* user gets a reply. Serving is the art of trading these off. |
| **MoE** | "Mixture of Experts" — a giant model that only turns on a few of its parts ("experts") per token. Cheaper to run than its size suggests (e.g. DeepSeek). |

**Why this event exists:** GPUs are extremely expensive and often sit idle because of bad memory management and dumb request routing. vLLM + llm-d are the leading *open-source* answer to "squeeze every token out of your GPUs." That's the whole theme.

---

## Part 1 — Foundations (for absolute beginners)

### 1.1 What is an LLM, really?

A **Large Language Model** (LLM) is a neural network trained on enormous amounts of text. Under the hood it does one thing: given some text, **predict the next token**. Repeat that in a loop and you get sentences, code, answers.

- **Token** — text is chopped into tokens (roughly ¾ of a word, or a few characters). "Kubernetes" might be 3–4 tokens. The model's input and output are both sequences of tokens.
- **Weights / parameters** — the billions of numbers learned during training. A "7B" model has 7 billion parameters; "70B" has 70 billion. More parameters = smarter but heavier. These weights must be loaded into GPU memory to run.
- **Context window** — the max number of tokens the model can "see" at once (e.g. 8K, 128K, 1M). Longer context = more memory needed.

### 1.2 Training vs Inference (this event is 100% about inference)

- **Training** — teaching the model by showing it text and adjusting weights. Done once, extremely expensive, by the model's creators.
- **Inference** — *using* the trained model to answer requests. Done millions of times a day. **This is what vLLM and llm-d optimize.** Nobody at this event is training models; they're *serving* them.

### 1.3 Why GPUs?

A GPU (Graphics Processing Unit) can do thousands of math operations in parallel. LLM inference is basically giant matrix multiplications, so GPUs are ~orders of magnitude faster than CPUs for it.

- **VRAM (GPU memory)** — the scarce resource. It must hold (a) the model weights and (b) the KV cache for every active request. A 70B model in FP16 needs ~140 GB just for weights — more than one GPU has, which is why models get split across GPUs.
- **The two GPU vendors you'll hear about:**
  - **NVIDIA** — programmed with **CUDA** (the dominant, proprietary GPU software platform). GPUs: A100, H100, H200, B200/GB200 (Blackwell).
  - **AMD** — programmed with **ROCm** (AMD's *open-source* CUDA alternative). GPUs: **Instinct MI300X / MI325X / MI350X**. Two talks + the workshop are about running vLLM on AMD ROCm.

### 1.4 The two phases of every request: Prefill and Decode

This distinction is the backbone of the whole event. Understand it and half the talks make sense.

```
PROMPT: "Explain Kubernetes to me"          ANSWER: "Kubernetes is an open ..."
        └──────── PREFILL ────────┘                 └──────── DECODE ───────┘
   Read ALL prompt tokens in one big pass.     Generate ONE token at a time,
   Compute-bound (GPU crunching hard).         each needs the whole model again.
   Produces the first token → TTFT.            Memory-bandwidth-bound. Slow & steady.
```

- **Prefill** — the model ingests your entire prompt in parallel. It's **compute-bound** (the GPU's math units are the bottleneck). Ends when the first output token appears.
- **Decode** — the model produces the answer token by token, each step feeding on the previous. It's **memory-bandwidth-bound** (moving weights/cache around is the bottleneck, not raw math). This is why long answers feel like they "type out."

Because these two phases stress *different* parts of the hardware, a key advanced trick (Part 3) is to run them on **separate** pools of GPUs — that's **prefill/decode disaggregation**.

### 1.5 The KV cache (the single most important concept)

When generating token #500, the model needs to "attend to" all 499 previous tokens. Recomputing them every step would be insane. So the engine **caches** the intermediate results (the "Key" and "Value" tensors) for every past token. That's the **KV cache**.

- It lives in **GPU memory** and **grows with every token** in the conversation.
- Long prompts + long answers + many concurrent users = KV cache explosion → you run out of VRAM → you can't serve more users.
- **Nearly every optimization in this event is about using the KV cache more cleverly:** packing it efficiently (PagedAttention), reusing it (prefix caching), routing to the machine that already has it (KV-cache-aware routing), or moving it off the GPU when idle (KV offload).

### 1.6 The metrics everyone quotes

| Metric | Meaning | Whose pain |
|---|---|---|
| **TTFT** (Time To First Token) | How long until you see the *first* word. Dominated by prefill. | User-perceived snappiness. |
| **TPOT / ITL** (Time Per Output Token / Inter-Token Latency) | Delay *between* each generated word. Dominated by decode. | How fast the answer "streams." |
| **Throughput** | Total tokens/sec served across *all* users. | Cost efficiency. |
| **Latency** | End-to-end time for one request. | Individual UX. |
| **SLO** | Service Level Objective — e.g. "p95 TTFT < 500 ms." The target platform teams must hit. | Ops teams. |

The eternal tradeoff: **batching more users together raises throughput (cheaper) but can hurt individual latency.** Good serving software hits SLOs while keeping GPUs busy.

---

## Part 2 — vLLM: the inference engine

### 2.1 What it is + where it came from

**vLLM** is a fast, memory-efficient open-source library for **LLM inference and serving**. Origin story worth knowing:

- Born at **UC Berkeley's Sky Computing Lab**; introduced the **PagedAttention** technique (paper *arXiv:2309.06180*, 2023).
- Now one of the most active open-source AI projects: **2,000+ contributors**, **200+ supported model architectures**, governed broadly (it sits under the **PyTorch Foundation**).
- It's the **default open-source model server** and the **engine llm-d is built on**. When people say "the vLLM ecosystem," they mean vLLM plus a constellation of companion libraries (Part 6).

You run it either as a Python library (offline batch jobs) or, more commonly, as an **OpenAI-compatible HTTP server** — meaning any tool that talks to OpenAI's API can point at your self-hosted vLLM instead. (Note: the server ships with **no authentication by default** — teams must put a gateway/auth in front, which is one thing llm-d helps with.)

### 2.2 PagedAttention — the founding trick

**Problem:** Naively, each request reserves one big contiguous block of GPU memory for its KV cache, sized for the *maximum* possible length. Most requests are shorter, so **60–80% of that memory is wasted** (internal fragmentation). Waste = fewer concurrent users = idle expensive GPU.

**Insight:** This is the exact problem operating systems solved decades ago with **virtual memory and paging**.

**Solution:** PagedAttention chops the KV cache into small **fixed-size blocks ("pages")** and hands them out on demand, with a "page table" mapping logical positions to physical blocks. Memory waste drops from ~60–80% to **under ~4%**. That directly means **more users per GPU** and higher throughput. It also makes it trivial to *share* identical pages between requests (see prefix caching).

*Analogy:* Instead of giving every diner a reserved 10-seat table whether they need it or not, you seat people at small shared tables as they arrive. Same restaurant, far more customers served.

### 2.3 Continuous (in-flight) batching

**Static batching** (the old way): collect N requests, run them together, and *wait for all N to finish* before starting the next batch. But requests finish at different times, so the GPU idles waiting for the slowest one.

**Continuous batching** (vLLM's way): requests **join and leave the batch mid-flight**, on every generation step. The moment one request finishes, a new one takes its slot. The GPU stays saturated. This is the single biggest throughput win over a naive loop and is now standard in every serious serving stack.

### 2.4 Two more memory tricks you'll hear

- **Chunked prefill** — a long prompt's prefill is broken into chunks and *interleaved* with ongoing decode work, so one giant prompt doesn't freeze everyone else's token stream. Smooths latency.
- **Prefix caching** — if many requests share the same beginning (e.g. a long system prompt, a RAG document, a few-shot template), vLLM computes that prefix's KV cache **once** and reuses it. Huge win for chatbots and agents that resend the same context. (This is also the hook llm-d's routing exploits — Part 3.)

### 2.5 Parallelism — splitting a model across GPUs

When a model is too big for one GPU, or you want more speed, you split it. Four kinds (know what each splits):

| Type | What it splits | One-liner |
|---|---|---|
| **Tensor Parallelism (TP)** | Individual layers (the matrices) across GPUs | Every GPU does part of *each* layer's math; needs fast interconnect (NVLink). |
| **Pipeline Parallelism (PP)** | Different layers onto different GPUs | GPU 1 does layers 1–10, GPU 2 does 11–20, like an assembly line. |
| **Data Parallelism (DP)** | Whole replicas of the model | Each GPU runs a full copy; more copies = more throughput. |
| **Expert Parallelism (EP)** | The "experts" of an MoE model across GPUs | Only relevant for MoE; central to **WideEP** (Part 3.5). |

### 2.6 Quantization — shrinking the numbers

Model weights are numbers. Storing them in fewer bits = less memory + faster, at some accuracy cost. The ladder you'll hear:

- **FP16 / BF16** (16-bit) — the standard "full" precision for serving.
- **FP8** (8-bit) — half the memory, now common on H100/MI300X; small quality loss.
- **INT4 / 4-bit** (AWQ, GPTQ) — quarter the memory; lets big models fit on small GPUs; more quality loss.

More concurrency and bigger models on the same hardware — but always a precision/quality tradeoff.

### 2.7 Speculative decoding (bonus speed trick)

A small, fast "draft" model guesses the next several tokens; the big model then **verifies them all in one parallel pass**. Correct guesses are kept, wrong ones discarded. Net effect: the answer streams faster **with no loss in quality** (the big model still has the final say).

### 2.8 vLLM "V1" architecture (high level)

The modern vLLM ("V1") engine uses a **multi-process** design that separates the API/scheduling loop from the GPU execution workers, reducing overhead and improving GPU utilization. You don't need internals — just know "V1" = the rearchitected, faster core, and it exposes the OpenAI-compatible server on top.

---

## Part 3 — llm-d: distributed inference on Kubernetes

### 3.1 Why one vLLM isn't enough

vLLM makes **one node** fast. But production means: millions of requests, models too big for one machine, traffic spikes, SLOs, multi-tenancy, cost control. You need **many vLLM replicas across a cluster**, plus something smart to route and scale them. Naively load-balancing requests **randomly** across replicas throws away vLLM's KV cache advantage (a replica may have to recompute a prefix another replica already has).

**llm-d** is the answer: a **Kubernetes-native, high-performance distributed LLM inference framework**, with **vLLM as its engine**. It's a young but heavyweight open-source project — a **CNCF Sandbox** project backed by **Red Hat, Google Cloud, IBM Research, CoreWeave, and NVIDIA**. Its stated goal: a "well-lit path" to serve LLMs at scale on k8s with the best performance-per-dollar.

### 3.2 Architecture (the request flow)

```
request → [ Inference Gateway (IGW) ]         ← built on Kubernetes Gateway API
                     │                            "Inference Extension" + Envoy proxy
                     ▼
          [ Endpoint Picker (EPP) ]           ← the vLLM-aware SCHEDULER: scores
                     │                            candidate pods on live metrics
                     ▼                            (queue depth, KV-cache affinity)
          [ InferencePool ]                    ← a group of same-model vLLM pods,
             ├── prefill pods                     optionally split into prefill vs
             └── decode pods                      decode "variants"
                     ▼
              vLLM  →  GPU
```

- **Inference Gateway (IGW)** — the smart front door. It's an implementation of the **Gateway API Inference Extension**, a standard k8s way to route *inference* traffic (not just generic HTTP). Uses **Envoy** under the hood.
- **Endpoint Picker (EPP)** — the **inference scheduler**, the brain. Instead of round-robin, it looks at each vLLM pod's real-time state (how full its queue is, whether it already holds the relevant KV cache) and picks the best one.
- **InferencePool** — a k8s abstraction grouping the pods serving one model, so they can be scaled and routed as a unit.

### 3.3 KV-cache-aware (prefix-aware) routing — llm-d's signature feature

> "Instead of routing requests randomly, route them to the pod that already has the right data in its KV cache."

Because vLLM caches prefixes, if a follow-up request (or another user with the same long system prompt / RAG context) lands on the **same pod that already computed that prefix**, the pod skips the recompute → **lower TTFT, less wasted GPU**. llm-d tracks which pod holds which KV blocks (via an event-driven KV index) and routes accordingly. It can also **offload** KV cache down a hierarchy (GPU → CPU RAM → SSD, via a component called **LMCache**) so it isn't lost when a GPU is under pressure.

### 3.4 Prefill/Decode (P/D) disaggregation

Recall (Part 1.4): prefill is compute-bound, decode is memory-bandwidth-bound. Running both on the same GPU makes them fight — a big prefill stalls everyone's decode.

**Disaggregation** = run prefill on one pool of GPUs and decode on another. Each pool is tuned and scaled for its job; no interference. **The cost:** the KV cache produced by prefill must be **transferred over the network** to the decode pool. llm-d does this with **NIXL** (an open transfer library) over fast **RDMA** networking (InfiniBand / RoCE / AWS EFA). The prefill pod hands over KV block metadata; the decode pod pulls the blocks. This transfer time counts against TTFT, so the networking matters a lot (a recurring research theme).

### 3.5 Wide Expert Parallelism (WideEP) — for giant MoE models

This is the AMD/IBM deep-dive territory. First, **MoE (Mixture of Experts)**:

- In a normal ("dense") model, every token flows through the *entire* network.
- In an **MoE** model, the big feed-forward layer is replaced by many **experts**; a small **router** picks the **top-k** experts per token (e.g. **DeepSeek picks 8 of 256 experts**). So a model can be *huge* in total parameters but only activate a *sparse* slice per token → far cheaper to run than its size implies.

**The problem at scale:** a giant MoE (DeepSeek-R1 can be 500 GB+ of weights) won't fit sensibly on a few GPUs, and "hot" experts get overloaded while "cold" ones idle.

**WideEP (Wide Expert Parallelism):** spread the experts across **many** GPUs/nodes (8, 16, 64+), so:
- more aggregate memory bandwidth for loading expert weights,
- more room for KV cache → higher concurrency / longer contexts,
- bigger effective batches → better GPU utilization.

**Two companion pieces you'll hear:**
- **EPLB (Expert Parallelism Load Balancer)** — dynamically rebalances which GPU hosts which experts as traffic shifts, so hot experts don't bottleneck.
- **DeepEP** — the high-performance **all-to-all communication** library that shuffles tokens to wherever their chosen experts live (over NVLink within a node, RDMA across nodes). On AMD the comms backends are **RCCL** and **MoRI**.

WideEP is usually combined with P/D disaggregation and reported to push DeepSeek-style models to thousands of tokens/sec per GPU on modern hardware (H200, GB200, MI300X).

### 3.6 Autoscaling & ops

llm-d exposes rich metrics (queue depth, KV usage) so Kubernetes can **autoscale** replicas with **HPA/KEDA**, and a **Workload Variant Autoscaler (WVA)** can place workloads to hit SLOs at lowest cost. This is the "platform team" story: elastic capacity, multi-tenancy, observability, cost per token.

### 3.7 llm-d vs vLLM vs NVIDIA Dynamo (so you're not confused)

| | What it is |
|---|---|
| **vLLM** | The inference **engine** — runs a model fast on a node. |
| **llm-d** | The **distributed serving layer** *around* vLLM on Kubernetes: routing, scheduling, disaggregation, autoscaling. Vendor-neutral, CNCF, built on the Gateway API Inference Extension. |
| **NVIDIA Dynamo** | NVIDIA's own distributed-inference stack — similar goals, more GPU/NVIDIA-centric. (llm-d and Dynamo even share the **NIXL** KV-transfer library.) |

**Rule of thumb:** vLLM = one engine. llm-d = an orchestra of engines on k8s.

---

## Part 4 — Summary of the YouTube video you shared

**Video:** *"AI Infrastructure Explained (GPUs, vLLM, and LLM-D)"* — channel **KodeKloud**
**Link:** https://www.youtube.com/watch?v=hBzUokVYQkI

> **Transparency note:** YouTube blocked automated transcript extraction from this environment (IP/bot protection), so I could not pull the video's verbatim words. The summary below is reconstructed from the video's **official title and KodeKloud's matching public course outline** ("AI Infrastructure: LLM-D, vLLM and GPUs") plus the confirmed topic set. It accurately reflects the video's *arc and content*, but is not a word-for-word transcript. Everything in Parts 1–3 above is the detailed version of what this video introduces.

**What the video is:** a **beginner-friendly explainer** that builds a *mental model* of what actually runs behind every AI product — "so you can reason about it instead of memorizing buzzwords." It's not a hands-on tutorial; it's the conceptual map. This is genuinely the perfect companion to your event.

**The arc it walks through (per the course description it mirrors):**

1. **Start with the hardware & model serving basics** — what a GPU is, what "serving a model" means, and why a single GPU + a naive loop is wildly inefficient (idle GPU, wasted memory).
2. **Zoom into a single request** — what happens *inside* one inference call: the prompt gets tokenized, the **prefill** phase reads it, the **decode** phase generates the answer token by token, and the **KV cache** stores the conversation state. This is where vLLM's ideas (PagedAttention for memory, continuous batching for keeping the GPU busy) are motivated.
3. **Scale from one GPU to a fleet** — a single node can't handle production traffic; you need many model servers, and you need to route traffic intelligently. Random load-balancing wastes the KV cache.
4. **Introduce llm-d** — how a **Kubernetes-native** framework enables **intelligent, distributed inference**: KV-cache-aware routing, splitting prefill/decode, and autoscaling across the GPU fleet. The payoff line of these explainers is usually: *"the fix for 'inference is too slow/expensive' is smarter software, not just more GPUs."*

**Your takeaway from the video:** it gives you exactly the vocabulary and the "single GPU → whole fleet" storyline. If you've read Parts 1–3 here, you already know everything the video teaches, in more depth.

---

## Part 5 — The event agenda, decoded (per session)

For each talk: **what it's about**, **why it matters**, and **a smart question you could ask**.

### 2:00 – 2:30 · vLLM & llm-d Updates — *Prasad Mukhedkar, Red Hat*
- **About:** The "state of the union" — newest features and releases across both projects.
- **Why it matters:** Both move *fast*; this is your map of what's current (e.g. V1 engine maturity, WideEP, disaggregation, semantic router).
- **Ask:** *"Which recent feature has given the biggest real-world tokens-per-dollar improvement?"*
- *Red Hat = enterprise open-source company (RHEL, OpenShift); a primary llm-d sponsor.*

### 2:30 – 3:00 · llm-d for Sovereign & Agentic Workloads — *Pravein Govindan Kannan, IBM*
- **About:** Using llm-d's distributed stack for two demanding cases, plus benchmarking.
  - **Sovereign AI** = running inference **entirely on your own infrastructure, under your own control/jurisdiction**, so sensitive data never leaves (compliance, regulation). The opposite of calling OpenAI's API.
  - **Agentic workloads** = long-running, **multi-step** AI agents that call tools, do retrieval (RAG), and hold multi-turn state. They hammer inference infra with **long/variable contexts and lots of KV-cache reuse** — exactly what llm-d's cache-aware routing and disaggregation target.
- **Why it matters:** This is where inference infra is heading — from single Q&A to persistent agents.
- **Ask:** *"For agentic multi-turn traffic, how much does prefix-cache-aware routing cut TTFT vs random routing?"*
- *IBM = IBM Research, a core llm-d contributor.*

### 3:00 – 3:30 · Distributed Inference on ROCm with WideEP — *Chaitanya Sri Krishna Lolla & Sirra Ajith, AMD*
- **About:** Running distributed vLLM + llm-d, with **WideEP** for MoE models, on **AMD GPUs via ROCm**.
  - **ROCm** = AMD's **open-source** GPU compute platform (the CUDA alternative). **WideEP** = spreading MoE experts across many GPUs (Part 3.5).
- **Why it matters:** Proves the vLLM/llm-d stack is **not NVIDIA-only** — real multi-vendor competition, often better memory-per-dollar (MI300X has 192 GB VRAM).
- **Ask:** *"On MI300X, what comms backend (RCCL vs MoRI) do you use for expert all-to-all, and how does it compare to DeepEP on NVIDIA?"*
- *AMD = the #2 GPU vendor; Instinct MI300X/MI325X/MI350X.*

### 4:00 – 4:30 · Inside vLLM Semantic Router — *Aayush Saini, Red Hat*
- **About:** A router that **classifies each request by its meaning** — domain, difficulty, whether deep "reasoning" is even needed, safety/PII — and sends it to the right model or setting. Reported results: **higher accuracy** while **cutting latency ~47% and token cost ~48%** (by *not* over-thinking easy questions). It runs the classification cheaply, **without needing its own GPU**.
- **Why it matters:** Cost control by *intelligence*, not just hardware — "don't use a sledgehammer on a thumbtack."
- **Ask:** *"How do you keep the semantic classifier's added latency negligible on every request?"*

### 4:30 – 5:00 · Scaling Inference at NxtGen Using the vLLM Ecosystem — *Abhishek Kumar, NxtGen*
- **About:** A real production/GPU-cloud provider's war stories scaling LLM serving.
- **Why it matters:** The "does this survive contact with reality?" session — SLOs, autoscaling, multi-tenancy, utilization, cost.
- **Ask:** *"What broke first when you scaled up, and which SLO (TTFT vs TPOT) was hardest to hold?"*
- *NxtGen = an India-based data-center / cloud-infrastructure provider.*

### 5:15 – 6:15 · Hands-on Workshop: vLLM Inference with AMD GPUs — *Aditya Sivagnanam*
- **About:** You'll actually run vLLM on AMD ROCm GPUs (provided by organizers — you SSH in).
- **Prep:** **Bring your laptop with SSH installed.** Expect to launch a vLLM server, hit its OpenAI-compatible endpoint, and watch batching/throughput. Skim the vLLM quickstart beforehand.
- **Ask (during):** *"How do we watch KV-cache utilization and throughput live while requests run?"*

---

## Part 6 — The full open-source stack ("all the open-source stuff going in")

You specifically wanted this. Here's the ecosystem you'll hear named, grouped by layer.

### The two headliners
| Project | Role | Where |
|---|---|---|
| **vLLM** | The inference/serving **engine**. | github.com/vllm-project/vllm |
| **llm-d** | **Kubernetes-native distributed** inference framework built on vLLM. | github.com/llm-d/llm-d |

### vLLM's engine-level companions (make a single node fast)
| Project | One-liner |
|---|---|
| **PyTorch** | The deep-learning framework vLLM is built on. |
| **torch.compile / CUDA Graphs** | Compile & capture the model's execution to cut per-step overhead. |
| **FlashAttention** | Ultra-fast, memory-efficient attention kernels. |
| **FlashInfer** | Attention/inference kernel library used for serving. |
| **xFormers** | Efficient transformer building-block kernels. |
| **Triton** | OpenAI's GPU-kernel language many of these kernels use. |
| **Hugging Face Transformers / Tokenizers** | Model definitions & tokenization; where most model weights come from. |
| **DeepGEMM** | High-performance FP8 matrix-multiply kernels (MoE/DeepSeek). |
| **Quantization: AWQ, GPTQ, bitsandbytes** | Shrink weights to INT4/INT8/FP8. |

### Distributed / MoE / KV-transfer layer (make the fleet fast)
| Project | One-liner |
|---|---|
| **DeepEP** | All-to-all expert communication library for MoE (WideEP). |
| **EPLB** | Expert-Parallel Load Balancer — rebalances hot/cold experts. |
| **NIXL** | Open KV-cache transfer library (used for P/D disaggregation; shared with NVIDIA Dynamo). |
| **LMCache** | KV-cache offloading/reuse across GPU → CPU → SSD. |
| **Ray** | Distributed Python runtime for multi-node orchestration. |
| **NCCL / RCCL** | GPU collective-comms libraries — **NCCL** (NVIDIA), **RCCL** (AMD). |
| **MoRI** | AMD's Modular RDMA Interface comms backend for distributed vLLM. |

### Kubernetes / gateway / ops layer
| Project | One-liner |
|---|---|
| **Kubernetes** | The cluster OS llm-d is native to. |
| **Gateway API Inference Extension** | The k8s standard for routing *inference* traffic; basis of the Inference Gateway. |
| **Envoy** | The proxy under the Inference Gateway. |
| **vLLM Semantic Router** | Semantic, cache-aware request routing (Red Hat talk). |
| **KServe** | Kubernetes model-serving platform that integrates llm-d. |
| **KEDA / HPA** | Kubernetes autoscalers driven by llm-d metrics. |
| **Prometheus / Grafana** | Metrics & dashboards for the SLOs above. |
| **Flux / GitOps** | Declarative deployment of the whole stack. |

### GPU compute platforms (the base layer)
| Project | One-liner |
|---|---|
| **ROCm** | AMD's **open-source** GPU compute stack (CUDA alternative) — the AMD talks + workshop. |
| **CUDA** | NVIDIA's GPU platform (proprietary, but the default target). |

### Common open models you'll hear
**DeepSeek-R1 / V3** (giant MoE, the WideEP poster child), **Llama** (Meta), **Qwen**, **Mistral/Mixtral**, **Gemma**. These are the *models* served *by* the stack above.

---

## Part 7 — Glossary (fast reference)

- **LLM** — Large Language Model; predicts the next token.
- **Token** — ~¾ of a word; the unit models read/write.
- **Inference** — running a trained model to get answers (vs training).
- **Prefill** — phase that reads the whole prompt; compute-bound; sets TTFT.
- **Decode** — phase that generates tokens one at a time; memory-bandwidth-bound.
- **KV cache** — cached attention state of prior tokens; lives in GPU memory; grows per token.
- **PagedAttention** — OS-paging-style KV cache management; kills memory waste. vLLM's founding idea.
- **Continuous batching** — requests join/leave the batch every step; keeps GPU busy.
- **Prefix caching** — reuse the KV cache of a shared prompt prefix.
- **Chunked prefill** — interleave big prefills with ongoing decode to smooth latency.
- **TP / PP / DP / EP** — Tensor / Pipeline / Data / Expert parallelism (ways to split work across GPUs).
- **MoE** — Mixture of Experts; only top-k experts activate per token (e.g. DeepSeek: 8 of 256).
- **WideEP** — Wide Expert Parallelism; spread MoE experts across many GPUs.
- **EPLB** — balances load across experts.
- **Disaggregation (P/D)** — run prefill and decode on separate GPU pools.
- **KV-cache-aware routing** — send a request to the pod that already holds its cache.
- **NIXL** — library that transfers KV cache between pods over RDMA.
- **Inference Gateway (IGW)** — llm-d's smart k8s front door (Gateway API Inference Extension + Envoy).
- **EPP (Endpoint Picker)** — llm-d's inference scheduler; picks the best pod.
- **Quantization** — store weights in fewer bits (FP8/INT4) to save memory.
- **Speculative decoding** — a draft model guesses tokens; the big model verifies in parallel.
- **ROCm / CUDA** — AMD's open / NVIDIA's proprietary GPU compute platforms.
- **TTFT / TPOT (ITL)** — time to first token / time per output token.
- **SLO** — the latency/throughput target ops teams must hit.
- **Sovereign AI** — self-hosted inference under your own control & jurisdiction.
- **Agentic workload** — long-running, multi-step, tool-using AI agent traffic.

---

## Part 8 — Logistics & how to show up confident

### Must-do before you go
- ✅ **Register** — registration closes **24 hours before** the event; unregistered = not admitted.
- ✅ **Bring a photo ID** — needed to verify your registration on arrival.
- ✅ **Bring your laptop with SSH installed** — the workshop provides GPU instances you SSH into. (macOS/Linux have `ssh` built in; on Windows use PowerShell's `ssh` or PuTTY. Test `ssh -V` beforehand.)
- ✅ Optional warm-up: skim the **vLLM quickstart** (docs.vllm.ai) so the workshop commands feel familiar.

### The 4 talking points that make you sound informed
1. *"The whole game is using the **KV cache** well — that's why PagedAttention, prefix caching, and cache-aware routing all exist."*
2. *"**vLLM** makes one node fast; **llm-d** makes the whole Kubernetes fleet fast."*
3. *"**Prefill is compute-bound, decode is memory-bound** — that's why disaggregation splits them."*
4. *"**MoE + WideEP** is how you serve giant models like DeepSeek cheaply — activate only a few experts, spread across many GPUs."*

### Good all-purpose questions
- "For our traffic mix, where's the bigger win — disaggregation or better routing?"
- "What's the realistic tokens-per-dollar gap between NVIDIA and AMD (ROCm) today?"
- "How hard is day-2 ops for llm-d — upgrades, debugging a slow pod, cost attribution?"
- "When is plain single-node vLLM enough, and when do you actually *need* llm-d?"

---

## Sources

Core projects & docs:
- vLLM docs — https://docs.vllm.ai/en/latest/
- PagedAttention paper (arXiv 2309.06180) — https://arxiv.org/pdf/2309.06180
- llm-d site & docs — https://llm-d.ai/ · https://github.com/llm-d/llm-d
- llm-d ↔ vLLM integration — https://docs.vllm.ai/en/stable/deployment/integrations/llm-d/

llm-d & distributed inference:
- Red Hat: llm-d Kubernetes-native distributed inferencing — https://developers.redhat.com/articles/2025/05/20/llm-d-kubernetes-native-distributed-inferencing
- Red Hat: Getting started with llm-d — https://developers.redhat.com/articles/2025/08/19/getting-started-llm-d-distributed-ai-inference
- Red Hat: Introduction to distributed inference with llm-d — https://developers.redhat.com/articles/2025/11/21/introduction-distributed-inference-llm-d
- Google Cloud: Enhancing vLLM for distributed inference with llm-d — https://cloud.google.com/blog/products/ai-machine-learning/enhancing-vllm-for-distributed-inference-with-llm-d/
- llm-d announce — https://llm-d.ai/blog/llm-d-announce

WideEP / MoE:
- Red Hat: Scaling DeepSeek-style MoEs with vLLM + llm-d using Wide EP — https://developers.redhat.com/articles/2025/09/08/scaling-deepseek-style-moes-vllm-and-llm-d-using-wide-ep
- vLLM blog: Large Scale Serving (DeepSeek Wide-EP) — https://vllm.ai/blog/2025-12-17-large-scale-serving
- NVIDIA: Wide Expert Parallelism on NVL72 — https://developer.nvidia.com/blog/scaling-large-moe-models-with-wide-expert-parallelism-on-nvl72-rack-scale-systems/
- llm-d docs: Multi-Node Wide Expert Parallelism — https://llm-d.ai/docs/dev/well-lit-paths/foundations/wide-expert-parallelism

Semantic Router:
- vLLM blog: Semantic Router — https://vllm.ai/blog/2025-09-11-semantic-router
- "When to Reason: Semantic Router for vLLM" (arXiv 2510.08731) — https://arxiv.org/pdf/2510.08731v1

AMD ROCm:
- ROCm blogs: MI300X inference optimization — https://rocm.blogs.amd.com/artificial-intelligence/LLM_Inference/README.html
- ROCm docs: vLLM inference — https://rocm.docs.amd.com/en/latest/how-to/rocm-for-ai/inference-optimization/workload.html

Sovereign / agentic:
- Red Hat: Building a reliable, sovereign inference layer — https://www.redhat.com/en/blog/why-self-hosted-inference-essential-building-reliable-sovereign-inference-layer

vLLM internals (PagedAttention + continuous batching explainers):
- https://www.runpod.io/articles/guides/vllm-pagedattention-continuous-batching
- https://learnopencv.com/vllm-deploy-llms-at-scale-paged-attention/

The video & its companion course:
- Video: https://www.youtube.com/watch?v=hBzUokVYQkI ("AI Infrastructure Explained (GPUs, vLLM, and LLM-D)", KodeKloud)
- KodeKloud course outline (mirrors the video): https://kodekloud.com/courses/ai-infrastructure-llm-d-vllm-and-gpus · https://kodekloud.com/courses/llm-d-a-deep-dive

*Doc generated 2026-09-18. Everything above is inference/serving — no model training involved.*
