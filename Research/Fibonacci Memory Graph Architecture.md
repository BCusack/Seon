# Fibonacci Memory Graph Architecture: A Bio-Mimetic Framework for Sovereign Memory Decay and Retrieval in Edge AI Companions

**Author:** The Seon Project

---

## Abstract

Memory management in sovereign, edge-deployed AI companions presents a distinctive computational challenge: a bounded-resource device must maintain a semantically rich, personalized knowledge graph that grows with lived experience, yet must also forget gracefully to preserve both privacy and efficiency. Existing approaches acknowledge decay as a desirable property but provide no formal mechanism. This paper proposes the **Fibonacci Memory Graph (FMG)** framework, which unifies three mathematically related structures—the Fibonacci heap for priority-ordered retrieval, the Fibonacci sequence for spaced decay checkpoints, and the golden ratio φ as the continuous decay constant—into a single, self-similar memory architecture. We situate FMG within the Seon Project's sovereign edge intelligence paradigm, demonstrating that Fibonacci-structured forgetting is not merely computationally efficient but constitutes a form of **architectural data minimisation**: stale memories are pruned by mathematical inevitability rather than user intervention or policy enforcement. This property is especially significant in the context of Phase-Adaptive Federated Learning (PAFL), where a leaner local memory graph reduces the information surface exposed during collaborative training phases.

**Keywords:** Fibonacci heap; spaced repetition; memory decay; knowledge graph; edge AI; data minimisation; sovereign AI; retrieval-augmented generation

---

## 1. Introduction

The Seon white paper describes a salience-based memory architecture in which an ephemeral context buffer promotes only significant information to a persistent knowledge graph of typed nodes and weighted edges, and acknowledges that "stale or non-salient details naturally decay or are deleted" (The Seon Project, n.d.). This acknowledgment is architecturally honest but formally incomplete: no decay function, schedule, or retrieval-priority mechanism is defined.

This gap is not trivial. Without a principled decay mechanism, two failure modes arise. First, **unbounded growth**: the memory graph accumulates low-salience nodes indefinitely, increasing storage and retrieval cost on SRAM-constrained microcontroller units (MCUs). Second, **uniform retrieval cost**: without priority ordering, every memory access must traverse the full graph, making context assembly for Retrieval-Augmented Generation (RAG) increasingly expensive as the graph grows.

The FMG framework addresses both failures simultaneously. By grounding salience decay and retrieval priority in the mathematical properties of the Fibonacci sequence, the architecture achieves:

1. **O(1) amortized salience updates** via Fibonacci heap key operations
2. **Graduated, self-reinforcing forgetting** via Fibonacci-spaced decay checkpoints
3. **A continuous, analytically tractable decay function** whose natural base is the golden ratio φ ≈ 1.618
4. **Mathematical self-similarity** that unifies the discrete and continuous components

The paper proceeds as follows. Section 2 reviews the relevant background across cognitive science, spaced-repetition systems, and data structure theory. Section 3 develops the FMG framework formally. Section 4 demonstrates integration with the Seon's existing architectural components. Section 5 discusses advantages, limitations, and open questions. Section 6 concludes.

---

## 2. Background

### 2.1 The Forgetting Curve and Spaced Repetition

Hermann Ebbinghaus (1885) established empirically that memory retention decays approximately exponentially with time, a pattern now known as the **forgetting curve**. His key finding was that the rate of forgetting is not constant: recently reinforced memories decay slowly, while unreinforced memories decay rapidly. Crucially, *retrieval itself is a reinforcement event*—recalling a memory resets its decay trajectory.

Sebastian Leitner (1972) operationalized this insight into the Leitner box system: items correctly recalled advance to a box with a longer review interval; items forgotten regress to a shorter interval. The review schedule is discrete and growing, a structure that anticipates the Fibonacci sequence. Piotr Wozniak (1990) formalized this into the SuperMemo SM-2 algorithm, which computes an *easiness factor* and assigns progressively longer inter-repetition intervals to well-retained items.

The critical shared insight across these systems is that **the optimal review interval grows super-linearly with successive successful retrievals**. A linearly growing schedule under-spaces early reviews (wasting computation) and over-clusters late reviews (failing to challenge fading memories). The Fibonacci sequence—whose growth is sub-exponential but super-linear—represents a natural calibration point.

### 2.2 Fibonacci Numbers and the Golden Ratio

The Fibonacci sequence is defined by the recurrence:

$$F_0 = 0, \quad F_1 = 1, \quad F_n = F_{n-1} + F_{n-2} \quad \text{for } n \geq 2$$

producing the series: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, …

A fundamental property is that the ratio of consecutive terms converges to the **golden ratio**:

$$\lim_{n \to \infty} \frac{F_{n+1}}{F_n} = \varphi = \frac{1 + \sqrt{5}}{2} \approx 1.618$$

This convergence property means that any system whose schedule or structure is governed by the Fibonacci sequence will exhibit *asymptotically self-similar* behaviour: the proportional step size between successive stages stabilizes at φ, regardless of the absolute scale.

### 2.3 Fibonacci Heaps

A **Fibonacci heap** (Fredman & Tarjan, 1987) is a priority-queue data structure with the following amortized time complexities:

| Operation | Amortized Cost |
|---|---|
| INSERT | O(1) |
| FIND-MAX | O(1) |
| DECREASE-KEY | O(1) |
| UNION | O(1) |
| EXTRACT-MAX | O(log n) |
| DELETE | O(log n) |

The Fibonacci heap's distinctive performance profile arises because it defers structural reorganization (consolidation) until an EXTRACT-MAX is called, accumulating "lazy" work. This is ideal for workloads where insertions and key updates are frequent and full extractions are rare—precisely the profile of an AI companion's memory graph, where new information arrives continuously but full memory reorganization is periodic.

The name derives from the fact that the amortized analysis relies on the Fibonacci sequence to bound the degree of trees in the heap's forest of binomial trees.

### 2.4 Knowledge Graphs in AI Companions

The application of knowledge graph structures to personal AI memory is well-established. Graph neural networks encode relational inductive biases that mirror human associative memory (Battaglia et al., 2018), and nearest-neighbour retrieval over graph embeddings has been shown to improve language model generalisation (Khandelwal et al., 2019). The Seon white paper describes a small, typed knowledge graph with nodes (Person, Event, Condition), edges (friend\_of, has\_condition), and metadata attributes (last\_mentioned, salience\_score, source\_confidence, consent\_tags). The FMG framework proposes a concrete mechanism for managing the salience\_score attribute and ordering retrieval from this graph.

---

## 3. The Fibonacci Memory Graph Framework

### 3.1 Overview

The FMG framework has four integrated components:

1. **FMG-H** (Heap): A Fibonacci heap imposed over knowledge graph nodes, keyed by current `salience_score`, enabling O(1) salience updates and O(log n) top-k retrieval for RAG context assembly.
2. **FMG-S** (Schedule): A Fibonacci-interval reinforcement schedule that defines decay checkpoints for each node.
3. **FMG-φ** (Phi): A continuous φ-based decay function that provides the mathematical substrate unifying FMG-H and FMG-S.
4. **FMG-T** (Topology): A graph branching rule derived from Fibonacci properties that governs edge accumulation and pruning.

### 3.2 FMG-H: Fibonacci Heap for Priority Retrieval

All nodes in the knowledge graph are simultaneously organized as a Fibonacci max-heap keyed by `salience_score ∈ [0, 1]`. The following events trigger heap operations:

- **Node creation** (e.g., new person mentioned): INSERT at initial salience $S_0$, cost O(1)
- **Node reinforcement** (e.g., same person mentioned again): DECREASE-KEY (upgraded to INCREASE-KEY via negation trick), cost O(1) amortized
- **RAG context assembly**: FIND-MAX or iterative EXTRACT-MAX for top-k nodes, cost O(k log n)
- **Decay checkpoint reached** (see FMG-S): DECREASE-KEY on all due nodes, cost O(1) per node amortized

The practical implication is that the most salient memories are always at the heap's root, immediately accessible for RAG retrieval without graph traversal. On SRAM-constrained MCUs where the full graph may exceed working memory, only the top-k heap nodes need to reside in active memory at any time.

### 3.3 FMG-S: Fibonacci-Interval Decay Schedule

Each knowledge graph node maintains a **reinforcement stage index** $r \in \{1, 2, 3, \ldots\}$ and a **next-checkpoint counter** $c = F_r$ (interaction-events or days, configurable per deployment).

**Reinforcement rule:** If the node is accessed (retrieved and used in a response) before or at checkpoint $c = F_r$:

$$r \leftarrow r + 1, \quad c \leftarrow F_{r+1}$$

The node's salience is boosted: $S \leftarrow \min(S + \delta_r, 1)$ where $\delta_r$ is a reinforcement increment that diminishes with stage (long-established memories need less boost per access).

**Decay rule:** If checkpoint $c = F_r$ is reached without reinforcement:

$$r \leftarrow \max(r - 1, 1), \quad c \leftarrow F_{r-1}$$

$$S \leftarrow S \cdot \varphi^{-1}$$

This multiplicative decay by $\varphi^{-1} \approx 0.618$ at each checkpoint regression is the discrete manifestation of the continuous FMG-φ function (see Section 3.4).

**Pruning:** When $S$ falls below a minimum salience threshold $S_{\min}$ (a configurable privacy parameter), the node is removed from the graph. This constitutes automatic, mathematically-driven data minimisation.

The first three schedule stages illustrate the graduated spacing:

| Stage $r$ | Checkpoint $F_r$ | Meaning |
|---|---|---|
| 1 | 1 | Review after 1 interaction-event |
| 2 | 1 | Review again after 1 interaction-event |
| 3 | 2 | Review after 2 interaction-events |
| 4 | 3 | Review after 3 interaction-events |
| 5 | 5 | Review after 5 interaction-events |
| 6 | 8 | Review after 8 interaction-events |
| … | … | … |

The two consecutive F=1 stages at the beginning mirror the Leitner system's initial close-spaced reviews, ensuring that newly promoted memories are rapidly tested before being trusted at longer intervals.

### 3.4 FMG-φ: The Continuous Golden Ratio Decay Function

The continuous analogue of FMG-S is:

$$S(t) = S_0 \cdot \varphi^{-t/\tau}$$

where:
- $S_0 \in [0, 1]$ is the salience score at the most recent reinforcement event
- $t$ is elapsed time measured in interaction-events since last reinforcement
- $\tau > 0$ is a per-user **personalizable time constant** that governs the rate of forgetting (larger $\tau$ = slower decay, appropriate for users with long interaction gaps or high continuity needs)

This is equivalent to standard exponential decay with base $e$ when written as:

$$S(t) = S_0 \cdot e^{-t \ln(\varphi) / \tau}$$

The natural decay constant is $\lambda = \ln(\varphi) / \tau \approx 0.481 / \tau$.

**Unification with FMG-S:** The continuous function evaluated at Fibonacci checkpoints recovers the discrete schedule asymptotically. For large $n$:

$$\frac{S(F_{n+1})}{S(F_n)} = \varphi^{-(F_{n+1} - F_n)/\tau} = \varphi^{-F_{n-1}/\tau}$$

As $n \to \infty$, $F_{n-1}/F_n \to \varphi^{-1}$, so the ratio of salience between successive checkpoints converges to:

$$\frac{S(F_{n+1})}{S(F_n)} \to \varphi^{-F_n / (\varphi \cdot \tau)}$$

This convergence demonstrates that **the proportional decay per Fibonacci interval stabilizes** as the schedule matures — the system's forgetting curve becomes self-similar, decaying by the same relative proportion at every successive stage. This is the mathematical basis for FMG's architectural elegance.

### 3.5 FMG-T: Graph Topology and Fibonacci Branching

Knowledge graph nodes accumulate edges as the Seon discovers relationships. FMG-T introduces a **Fibonacci branching bound**: the maximum degree (number of edges) of a node at reinforcement stage $r$ is bounded by $F_{r+2}$.

| Stage $r$ | Max degree $F_{r+2}$ |
|---|---|
| 1 | 2 |
| 2 | 3 |
| 3 | 5 |
| 4 | 8 |
| 5 | 13 |

This rule has two architectural consequences:

1. **Hub formation is earned**: high-salience, frequently reinforced nodes (large $r$) are permitted to become densely connected hubs, accurately representing their centrality in the user's life. A person mentioned daily (large $r$, high $S$) will have edges to many associated events, emotions, and other people. A peripheral acquaintance (small $r$, low $S$) remains a leaf node.

2. **Cascading pruning**: when a node's salience decays below $S_{\min}$ and it is removed, its edges are pruned. If those edges were load-bearing for other low-salience nodes, those nodes may also decay below threshold. This creates a natural cascade pruning effect — semantically peripheral subgraphs dissolve as a unit — without requiring explicit garbage collection.

---

## 4. Integration with Seon Architecture

### 4.1 RAG and Computing-in-Memory

The Seon employs Retrieval-Augmented Generation (RAG) accelerated by Computing-in-Memory (CiM) to avoid costly data transfers between compute and memory (Qin et al., 2024). FMG-H directly optimizes this pipeline: rather than scanning the full memory graph to assemble RAG context, the system performs FIND-MAX operations on the Fibonacci heap to retrieve the top-k most salient nodes in O(k log n) time. On typical edge deployments with SRAM-constrained MCUs (32–512 kB), k << n, making this retrieval essentially constant-cost in practice.

The CiM architecture processes the retrieved top-k node embeddings in-memory, avoiding the traditional von Neumann bottleneck. FMG-H's lazy consolidation property further aligns with CiM: in-memory operations are most efficient when access patterns are predictable and localized, both properties of heap root access.

### 4.2 Phase-Adaptive Federated Learning

PAFL uses a tunable phase parameter $\phi \in [0, 1]$ to balance privacy and utility across distributed nodes (Chen et al., 2025). It is worth noting a striking notational coincidence: the PAFL phase parameter $\phi$ shares its symbol with the golden ratio $\varphi$ of FMG-φ. While these are functionally distinct—PAFL's $\phi$ is an optimization hyperparameter, FMG's $\varphi$ is an irrational constant—the resonance is not without meaning.

A Fibonacci-pruned memory graph is structurally smaller than an unpruned one, and its top-salience nodes are explicitly ranked by FMG-H. During PAFL's utility-optimized phases (high $\phi$), the federated update gradient can be computed over only the top-k FMG-H nodes rather than the full graph, reducing both the communication cost of the federated round and the membership inference risk reported at 62% reduction in Chen et al. (2025). FMG-S's pruning further ensures that the local model's private "memory surface" — the set of nodes that could, even in principle, be inferred from the federated update — shrinks automatically over time.

### 4.3 Salience Promotion from the Ephemeral Buffer

The Seon's ephemeral context buffer promotes information to long-term memory only when repeated, consented signals cross a salience threshold (The Seon Project, n.d.). Under FMG-S, this threshold corresponds to initiating a node at stage $r = 1$, with checkpoint $F_1 = 1$. A newly promoted node must survive its very first reinforcement interval — one interaction-event — before it is trusted at the longer $F_2 = 1$, $F_3 = 2$ intervals. Nodes that fail this first checkpoint immediately regress and decay toward $S_{\min}$, meaning that the ephemeral buffer's selectivity is extended into the early stages of long-term memory. **Promotion is not binary but a graduated entry into a continuum of salience.**

### 4.4 OML and the Cryptographic Memory Boundary

The Open-access, Monetizable, Loyal (OML) primitive (Cheng et al., 2025) enforces cryptographic authorization over model execution. FMG adds a complementary property: because pruned nodes are deleted from the graph, the set of user data that OML must protect shrinks continuously. The cryptographic boundary and the FMG decay schedule together constitute a **two-layer data minimisation architecture** — OML prevents unauthorized access to what exists; FMG ensures that stale data eventually ceases to exist.

---

## 5. Discussion

### 5.1 Advantages

**Computational alignment with edge constraints.** Fibonacci heap operations are O(1) amortized for the most common operations (INSERT, DECREASE-KEY), matching the access-heavy, reorganization-rare profile of a personal memory graph on a resource-constrained device.

**Privacy by mathematics.** Unlike policy-based data retention (which requires user action or scheduled jobs), FMG-S pruning is deterministic and unconditional. A memory that is never reinforced will inevitably reach $S_{\min}$, regardless of system state or user oversight. This constitutes a hard privacy guarantee rather than a soft commitment.

**Personalisation through τ.** The per-user time constant $\tau$ allows the decay rate to be calibrated to individual interaction patterns. A user who interacts with the Seon daily will have a different natural τ than one who uses it weekly. Τ can be estimated from the empirical inter-interaction interval distribution during the genesis event or updated adaptively as usage patterns emerge.

**Biological plausibility.** The use of spaced repetition to model forgetting is grounded in over a century of empirical memory research (Ebbinghaus, 1885; Leitner, 1972; Wozniak, 1990). The FMG framework aligns the AI companion's memory dynamics with the cognitive processes it aims to support, creating a system whose forgetting feels intuitive to users rather than arbitrary.

### 5.2 Limitations and Open Questions

**Graph consistency during pruning cascades.** When FMG-T cascading pruning removes a hub node, connected nodes lose edges. If two remaining nodes were connected only through the pruned hub, their relational context is lost. This may be intentional (the relationship was mediated by a peripheral person who faded from the user's life) or undesirable (important context is lost). Future work should define policies for **edge migration** or **indirect relation inference** before pruning.

**Τ estimation and cold start.** During early use, there is insufficient data to estimate τ reliably. An inappropriate initial τ may cause too-aggressive pruning (frustrating users whose memories are deleted) or too-slow pruning (inflating graph size during the privacy-sensitive early period). Bayesian approaches to τ estimation with informative priors from population-level data are a natural extension.

**Heap implementation on MCUs.** Fibonacci heap implementations require pointer-based tree structures that can be memory-intensive relative to simpler priority queues (e.g., binary heaps). On MCUs with 32 kB SRAM, the heap overhead must be characterised empirically against the theoretical O(1) benefits. A **lazy binary heap with periodic Fibonacci-schedule rebalancing** may be a pragmatic approximation for the most constrained deployments.

**Interaction-event granularity.** The FMG-S schedule is parameterized in "interaction-events," an intentionally abstract unit. Concretely, an interaction-event might be defined as a conversational turn that involves a given entity, a day, or a session. The choice of granularity affects the perceived decay rate significantly and must be validated in user studies.

---

## 6. Conclusion

The Fibonacci Memory Graph framework addresses a formally unresolved gap in the Seon architecture: the absence of a principled memory decay and retrieval-priority mechanism. By unifying the Fibonacci heap (FMG-H), Fibonacci-interval decay schedule (FMG-S), golden ratio decay function (FMG-φ), and Fibonacci branching topology (FMG-T) into a single coherent framework, FMG provides an architecture in which forgetting is not a maintenance task but a structural property. Memories accumulate salience through reinforcement, decay toward deletion through neglect, and organize themselves into a priority-ordered graph that exposes the most salient context to RAG retrieval at minimal computational cost.

This design is particularly well-suited to the Seon's sovereign edge intelligence paradigm, where privacy is not merely a policy commitment but an architectural guarantee. A FMG-governed knowledge graph is self-minimising, self-organising, and self-similar — properties that align the AI companion's inner life with the cognitive patterns of the human it serves.

For full architectural context, see the Seon White Paper (The Seon Project, n.d.) and the companion papers *Sovereignty in the Age of Cognitive Extractivism* and *Effective AI Companions: Psychological Effects of Seon-Style AI Companions*.

---

## References

- Battaglia, Peter W., Jessica B. Hamrick, Victor Bapst, et al. 2018. "Relational inductive biases, deep learning, and graph networks." *arXiv preprint* arXiv:1806.01261. https://arxiv.org/abs/1806.01261
- Chen, Xiaolong, et al. 2025. "Phase-Adaptive Federated Learning for Privacy-Preserving Personalized Travel Itinerary Generation." *Tourism and Hospitality*.
- Cheng, Zerui, et al. 2025. "OML: A Primitive for Reconciling Open Access with Owner Control in AI Model Distribution." *OpenReview*.
- Ebbinghaus, Hermann. 1885. *Über das Gedächtnis: Untersuchungen zur experimentellen Psychologie*. Leipzig: Duncker & Humblot. [Translated as *Memory: A Contribution to Experimental Psychology*, 1913.]
- Fredman, Michael L., and Robert Endre Tarjan. 1987. "Fibonacci Heaps and Their Uses in Improved Network Optimization Algorithms." *Journal of the ACM* 34, no. 3: 596–615. https://dl.acm.org/doi/10.1145/28869.28874
- Khandelwal, Urvashi, Angela Fan, Dan Jurafsky, and Luke Zettlemoyer. 2019. "Generalization through Memorization: Nearest Neighbor Language Models." *arXiv preprint* arXiv:1911.00172. https://arxiv.org/abs/1911.00172
- Leitner, Sebastian. 1972. *So lernt man lernen: Der Weg zum Erfolg*. Freiburg im Breisgau: Herder.
- Qin, Ruiyang, et al. 2024. "Robust Implementation of Retrieval-Augmented Generation on Edge-based Computing-in-Memory Architectures." *arXiv preprint* arXiv:2405.04700.
- The Seon Project. n.d. *White Paper: The Seon Project — The AI Companion*. Unpublished manuscript.
- Wozniak, Piotr A. 1990. "Optimization of Learning." MS thesis, University of Technology, Poznań. https://www.supermemo.com/en/blog/application-of-a-computer-to-improve-the-results-obtained-in-working-with-the-supermemo-method
