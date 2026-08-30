# Abhineeth Duddela

Distributed systems and ML infrastructure, implemented from the primary
literature. I like the parts where a claim can be checked, so most of these
repos ship a report whose every number came out of a run rather than out of a
sentence.

**[Portfolio](https://abho7.github.io/portfolio-site/)** ·
USACO Gold Division ·
NLP paper submitted to NHSJS 2025

---

### Things that are running

| | what it is | the number that matters |
|---|---|---|
| **[fluid-sim](https://github.com/abho7/fluid-sim)** | Incompressible Navier-Stokes on WebGPU compute shaders, MAC staggered grid, five pressure solvers | Numerical viscosity measured at **ν_num = 5.79e-4**, 2.9% of the physical ν |
| **[ml-infra-platform](https://github.com/abho7/ml-infra-platform)** | A Raft engine, an HNSW index and a training framework composed into one platform, driven from outside as read-only dependencies | First cross-layer bug: **both components correct, every replica crashed** |
| **[distributed-training-framework](https://github.com/abho7/distributed-training-framework)** | Data-parallel SGD, ring all-reduce and parameter server, six invariants checked every step | **1,960 checked steps**, 22 workers killed mid-step, worst gradient error **8.9e-16** |
| **[raft-chaos-testing](https://github.com/abho7/raft-chaos-testing)** | Per-link drop and delay injection against a real Raft implementation | **3 safety properties asserted per tick** across a 600-seed sweep |
| **[vectordb-hnsw](https://github.com/abho7/vectordb-hnsw)** | HNSW from the Malkov & Yashunin paper, in NumPy. No FAISS, no hnswlib | **recall@10 = 1.000**, 20x faster than brute force at n=8000 |
| **[mcp-memory-server](https://github.com/abho7/mcp-memory-server)** | Local-first persistent memory for Claude, HNSW over on-device ONNX embeddings | **Zero network calls** after the model is cached once |

Also: [raft-kv-store](https://github.com/abho7/raft-kv-store) (Raft from the
paper, tested by killing servers mid-write over real TCP),
[mcts-code-reasoner](https://github.com/abho7/mcts-code-reasoner) (test-time
tree search with a budget-discounted UCB1 and an RLIMIT sandbox),
[crisis-nlp-demo](https://github.com/abho7/crisis-nlp-demo) (attributions in
closed form, so they are exact rather than sampled), and
[flightpath-scheduler](https://github.com/abho7/flightpath-scheduler) (course
scheduling as an NP-hard CSP, CP-SAT plus a dependency-free fallback).

---

### How these are built

**From scratch means from scratch.** The consensus protocol, the HNSW graph,
the FFT, the multigrid V-cycle and the all-reduce are written here, not
imported. Where a library would have done it, the repo says so and explains
what implementing it taught.

**The measuring code gets tested too.** Three of the four bugs written up on
fluid-sim's report were in the validators rather than the solver. A check that
has never been observed to fail proves nothing, so the validators get
deliberately broken to confirm they catch what they claim to.

**Negative and partial results get published.** fluid-sim's enstrophy cascade
comes out at -4.529 against a theoretical -3, and the report says so and
diagnoses why. Four of the six findings on distributed-training-framework's
report are defects in its own harness, two of which would have produced a
confidently wrong result. They are on the report rather than quietly fixed.

**Python · C++ · Java · JavaScript · R · NumPy · WebGPU · asyncio**
