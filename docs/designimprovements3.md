# Mycelium Architecture Specification

**Version 4.0 — June 2026**  
**SuperInstance Open Source Initiative**  
*Authors: The Mycelium Community*

---

## 0. Executive Summary

Mycelium is an open‑source platform for building **living agent systems**—software that learns from demonstration, compresses behaviors into reusable **seeds**, and executes them across a swarm of tiny neural models. This document presents the fourth major revision of the architecture, introducing a paradigm shift: **agent connections themselves become learnable**.

In previous versions, agent communication was defined by fixed topics and chains. Now, the swarm is modeled as a **weighted directed graph** whose edges strengthen or weaken based on experience. This enables:

- **Emergent coordination:** Agents self‑organize into task‑specific teams.
- **Continuous optimization:** The system’s own communication topology improves with use.
- **Collective intelligence:** Topologies learned by one user can benefit others via federated learning.
- **True muscle memory:** Skills reside not just in agents, but in the pathways between them.

The architecture integrates novel mechanisms: **reward‑modulated Hebbian plasticity** for edge weights, **online spectral clustering** for dynamic group formation, **topology seeds** for capturing and sharing effective configurations, and **federated topology learning** for cross‑user optimization.

All earlier concepts—behavioral embedding space, seeds, Plinko market, world models, dreaming—are preserved and enhanced. The result is a system that not only learns what to do, but learns how to organize itself to do it better.

This document provides a complete, implementable blueprint for Mycelium v4.0, with detailed component specifications, algorithms, data structures, and research grounding.

---

## 1. Introduction

### 1.1 The Problem with Static Architectures

Traditional multi‑agent systems rely on fixed communication structures: agent A always sends to agent B. This rigidity limits adaptability and prevents the system from discovering more efficient pathways. Even in Mycelium v3.0, agent connections were defined by static topics and skill chains, which, while flexible, did not learn from experience.

Biological neural networks, in contrast, constantly remodel their connections. Synapses strengthen with use, weaken with disuse, and new connections form as needed. This **plasticity** is fundamental to learning and adaptation.

### 1.2 A New Paradigm: Learning the Topology

Mycelium v4.0 introduces **learnable agent webs**. The swarm is modeled as a weighted directed graph. Edge weights represent the strength of influence between agents. These weights are updated via a reward‑modulated Hebbian rule: connections that contribute to successful outcomes are strengthened; those that do not are weakened. Over time, the graph self‑organizes into efficient, task‑specific topologies.

This shift has profound implications:
- **Emergent coordination:** Agents spontaneously form functional groups, like soccer players organizing into defenders and forwards.
- **Continuous optimization:** The system’s architecture improves with every interaction.
- **Shareable configurations:** Effective topologies can be captured as **topology seeds** and shared across users via federated learning.
- **Interpretability:** The learned graph provides a map of how the system “thinks” about tasks.

### 1.3 Core Thesis

The configuration of agents—who talks to whom, with what strength—is a learnable artifact, as valuable as the agents’ internal weights. By making the graph itself subject to learning, we enable the swarm to discover optimal coordination patterns, personalize to individual users, and benefit from collective experience.

---

## 2. System Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         Mycelium v4.0 System                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  [Sensors] → [Sensor Layer] → [Shared Memory] → [Agent Swarm]           │
│       ↑              ↑              ↑                  ↑                 │
│       │              │              │                  │                 │
│       └── [Memory] ←─┴── [Seed Engine] ←── [Plinko Layer]                │
│                                          │                               │
│                                          ▼                               │
│                                 [Action Executors] → [Outcome]           │
│                                          │                               │
│                                          ▼                               │
│                               [Experience Logger]                        │
│                                          │                               │
│                                          ▼                               │
│     ┌──────────────┬──────────────┬─────┴─────┬──────────────┬────────┐ │
│     │Skill Chunker │World Model   │Dreaming    │Training      │Dynamic │ │
│     │(Grammar Ind.)│Trainer       │Engine      │Scheduler     │Graph   │ │
│     │              │              │            │              │Manager │ │
│     └──────────────┴──────────────┴───────────┴──────────────┴────────┘ │
│                       │              │              │                   │
│                       └──────────────┴──────────────┴───┐               │
│                                                          ▼               │
│                                                 [Model Zoo]              │
│                                                      │                   │
│                                                      ▼                   │
│                                         [Federated Topology Aggregator]  │
│                                                                           │
└─────────────────────────────────────────────────────────────────────────┘
```

**New Components (highlighted):**
- **Dynamic Graph Manager:** Maintains the weighted directed graph of agent connections, applies plasticity updates, and prunes/grows edges.
- **Federated Topology Aggregator:** Collects anonymized topology snapshots from users, distills population‑level templates, and redistributes improvements.

All other components (Sensor Layer, Agent Swarm, Plinko, etc.) are enhanced to interact with the dynamic graph.

---

## 3. Core Concepts

| Concept | Definition |
|---------|------------|
| **Agent Graph** | A weighted directed graph `G = (V, E, W)` where `V` is the set of agents, `E` is the set of communication channels, and `W: E → [0,1]` assigns a strength to each edge. |
| **Synaptic Weight** | The strength of a connection from agent A to agent B. Influences how much A’s output affects B’s input. |
| **Reward‑Modulated Hebbian Plasticity** | A learning rule that updates synaptic weights based on co‑activation and global/local reward signals. |
| **Dynamic Clustering** | Online spectral clustering that groups agents into functional teams based on current connection strengths. |
| **Topology Seed** | A compact representation of a subgraph (nodes, edges, weights) that encodes a learned coordination pattern for a specific task or skill. |
| **Federated Topology Learning** | A process where multiple Mycelium instances share anonymized topology seeds to improve collective coordination patterns. |

All previously defined concepts (Behavioral Embedding Space, Seeds, Plinko Market, World Model, Dreaming, etc.) remain and are extended to work with the dynamic graph.

---

## 4. Component Specifications

### 4.1 Agent Data Structure (Revised)

```python
@dataclass
class Agent:
    agent_id: str
    agent_type: str
    model_path: str
    # ... existing fields ...
    
    # New fields for dynamic graph
    incoming_edges: Dict[str, float]   # maps source agent_id → weight
    outgoing_edges: Dict[str, float]   # maps target agent_id → weight
    plasticity_params: {
        "learning_rate": float,
        "decay": float,
        "eligibility_trace": Dict[str, float]  # for credit assignment
    }
    last_activation: float
    activation_trace: List[Tuple[float, str]]  # (timestamp, task_id)
```

**Rationale:** Each agent now tracks its connections and a short history of activations to support plasticity updates.

### 4.2 Dynamic Graph Manager

**Purpose:** Maintain the global agent graph, apply plasticity updates, and manage edge pruning/growth.

#### 4.2.1 Graph Representation
- Stored as a sparse adjacency matrix (e.g., CSR format) for efficient updates.
- Edge weights are 16‑bit floats; initially set to small positive values for predefined connections (based on topics) and zero elsewhere.

#### 4.2.2 Plasticity Engine

**Algorithm: Reward‑Modulated Hebbian Update**

After each task (or batch of tasks) with a known outcome (success/failure), the engine:

1. Retrieves the **activation trace** for all agents involved: a sequence of (agent, timestamp) pairs.
2. For each pair of agents (i, j) where i’s activation preceded j’s within a short window (e.g., 100ms), compute **co‑activation** `c_ij` (e.g., count of such occurrences).
3. Compute weight update:
   ```
   Δw_ij = η * (R - baseline) * (c_ij - decay * w_ij)
   ```
   where `η` is learning rate, `R` is global reward (e.g., 1 for success, -0.1 for failure), `baseline` is a moving average of recent rewards.
4. Apply update, clipping weights to [0,1].
5. Decay eligibility traces for all edges.

**Research grounding:** This rule is inspired by reward‑modulated Hebbian learning in spiking neural networks and has been shown to enable complex learning tasks . The baseline term reduces variance and improves stability.

#### 4.2.3 Pruning and Growth

- **Pruning:** If `w_ij < threshold` (e.g., 0.01) for more than `N` consecutive days, remove the edge.
- **Growth:** If two agents are frequently co‑activated within a short window but have no direct edge, initialize a new edge with small weight (e.g., 0.05). This is detected by monitoring activation correlations.

#### 4.2.4 Dynamic Clustering (Spectral)

Periodically (e.g., every hour during idle time), the manager recomputes functional clusters:

1. Construct the graph Laplacian `L = D - W` where `D` is the degree matrix (sum of outgoing weights).
2. Compute the eigenvectors corresponding to the smallest `k` eigenvalues (where `k` is determined by the eigengap heuristic).
3. Use k‑means on the rows of the eigenvector matrix to assign agents to clusters.
4. Within each cluster, allow richer communication (e.g., all‑to‑all with learned weights); between clusters, maintain sparser connections (only edges that survived pruning).

**Research grounding:** The HYGMA framework  demonstrates that dynamic spectral clustering enables agents to "figure out their own groupings based on what they're doing," leading to emergent coordination patterns that improve task performance.

### 4.3 Plinko Layer with Graph Awareness

The Plinko market now uses the graph to determine which agents receive proposals:

- Each agent’s proposal is broadcast only to its outgoing neighbors, weighted by edge strength. (Stronger edges get higher‑fidelity messages; weaker edges may receive downsampled or delayed information.)
- Agents that receive multiple proposals can fuse them (e.g., via attention) before generating their own proposal.
- The Plinko selection process remains unchanged, but now the set of proposals considered is shaped by the graph.

**Benefit:** Reduces communication overhead and encourages specialization—agents focus on signals from trusted sources.

### 4.4 Topology Seed

**Purpose:** Capture a learned subgraph for a specific skill or task, enabling sharing and reuse.

#### 4.4.1 Encoding

Given a task trace (sequence of activated agents and the edges used), we extract the relevant subgraph:
- Nodes: agents that were activated (by type, not instance).
- Edges: connections that were used, with their learned weights.
- Metadata: task context, success rate, etc.

The subgraph is encoded into a fixed‑length vector using a **graph neural network encoder** trained to reconstruct the graph’s essential structure. This vector is the **topology seed**.

#### 4.4.2 Decoding

To instantiate a topology seed on a new device:
- The decoder produces a prototype graph (nodes by type, expected edge weights).
- The system matches the prototype to available agents (using specialization embeddings) and creates the corresponding connections with appropriate initial weights.
- The new topology can then be fine‑tuned locally.

**Research grounding:** Graph autoencoders are well‑established; applying them to agent topologies is novel but plausible.

### 4.5 Federated Topology Aggregator

**Purpose:** Enable cross‑user learning of effective coordination patterns without sharing raw data.

#### 4.5.1 Aggregation Protocol

1. **Local training:** Each Mycelium instance evolves its own agent graph via plasticity and clustering.
2. **Snapshot selection:** Periodically (e.g., weekly), each instance exports topology seeds for skills that have achieved high success rates.
3. **Anonymization:** Seeds are stripped of user‑identifying metadata and optionally have differential privacy noise added.
4. **Secure aggregation:** A coordinating server collects seeds from many users and performs:
   - **Clustering of seeds:** Group seeds by task type (e.g., “email management”).
   - **Averaging within clusters:** For each cluster, compute a **canonical topology template** (e.g., by averaging edge weights across seeds, using a technique like FedAvg for graphs).
   - **Genetic programming refinement:** Optionally, apply crossover and mutation to generate novel hybrid topologies .
5. **Distribution:** Templates are sent back to clients, who may use them as priors (e.g., by initializing new skills with the template and then fine‑tuning).

#### 4.5.2 Handling Heterogeneity

Users may have different sets of agents. The aggregator matches templates to available agent types via specialization embeddings. If a required agent type is missing, the template is adapted (e.g., by substituting a similar agent).

**Research grounding:** The FedRAM framework  addresses multi‑task learning with heterogeneous clients, which aligns with our need to balance local specialization with global knowledge. The genetic programming approach to model aggregation  provides a method for evolving better aggregation functions.

### 4.6 Integration with Existing Components

- **Seed Engine:** Now can produce both behavioral seeds (from demonstrations) and topology seeds (from learned graphs).
- **Skill Chunker:** Can also discover recurring subgraph patterns (e.g., a particular team of agents that often works together).
- **World Model & Dreaming:** Dreaming can now simulate not just variations of behavior, but variations of topology. The world model must be extended to predict how changes in agent connections affect outcomes.
- **Model Zoo:** Stores topology seeds alongside behavioral seeds.

---

## 5. Learning Dynamics: How the Web Evolves

### 5.1 Daytime Operation

- Agents execute tasks, proposals flow according to current graph.
- Plinko selects actions, outcomes are logged.
- Activation traces are recorded.

### 5.2 Nightly Updates

1. **Plasticity updates:** Apply reward‑modulated Hebbian rule to adjust edge weights based on the day’s successes/failures.
2. **Pruning and growth:** Remove weak edges; add new edges where correlated activations suggest missing connections.
3. **Spectral clustering:** Recompute functional groups to inform future communication priorities.
4. **Topology seed extraction:** For high‑performing skills, generate topology seeds and optionally share them (if user opts in).

### 5.3 Long‑Term Evolution

- Over weeks, the graph becomes increasingly specialized to the user’s routines.
- Federated learning periodically injects population‑level templates, providing a “common sense” starting point for new skills.

---

## 6. Implementation Roadmap

| Phase | Timeline | Milestones |
|-------|----------|------------|
| **1. Dynamic Graph Core** | 0–4 months | Implement graph data structure, plasticity engine, pruning/growth; integrate with Plinko; basic spectral clustering. |
| **2. Topology Seeds** | 5–8 months | Graph encoder/decoder; seed storage and instantiation; extend skill chunker to detect subgraph patterns. |
| **3. Federated Learning** | 9–12 months | Anonymization pipeline; secure aggregation server; genetic programming for topology templates; client‑side template adaptation. |
| **4. World Model Extension** | 13–16 months | Extend world model to predict effects of topology changes; integrate topology dreaming. |
| **5. Ecosystem** | 17–24 months | Topology marketplace; cross‑platform synchronization; advanced visualization tools. |

---

## 7. Research Agenda (Open Questions)

1. **Optimal plasticity rule:** Compare reward‑modulated Hebbian with policy gradient methods for graph updates. What baseline works best?
2. **Exploration vs. exploitation in graph space:** How to balance trying new connections vs. exploiting known good ones?
3. **Credit assignment:** How to attribute success to specific edges when many agents are involved? Eligibility traces are a start; more sophisticated methods may be needed.
4. **Graph compression for federated learning:** What graph embedding dimension preserves enough information while ensuring privacy?
5. **Heterogeneity handling:** How to adapt a template when the user lacks a required agent type? Agent substitution via specialization embeddings is promising but needs validation.
6. **Negative transfer:** Under what conditions does a population template harm rather than help? How to detect and revert?
7. **Dreaming about topologies:** Can we use the world model to simulate the impact of edge changes before applying them in reality? What loss function encourages useful topological mutations?

---

## 8. Conclusion

Mycelium v4.0 introduces a fundamental advance: **the agent communication graph itself becomes a learnable artifact**. By applying reward‑modulated Hebbian plasticity, dynamic spectral clustering, and federated topology learning, we enable the swarm to self‑organize, personalize, and benefit from collective experience. This moves us closer to truly living intelligence—a system that not only learns what to do, but learns how to organize itself to do it better.

The architecture is grounded in cutting‑edge research (HYGMA , CoMIX , FedRAM , genetic aggregation ) and provides a clear path to implementation. We invite the community to join us in building this future.

---

## 9. References

1. Liu, C. & Li, D. "HYGMA: Hypergraph Coordination Networks with Dynamic Grouping for Multi-Agent Reinforcement Learning." ICML 2025. 

2. "Multi-Agent Collaboration via Evolving Orchestration." NeurIPS 2025. 

3. "CoMIX: A Multi-Agent Reinforcement Learning Algorithm That Encourages Independent Learning." AAMAS 2020. 

4. "Bridging Model Heterogeneity in Federated Learning via Uncertainty-based Asymmetrical Reciprocity Learning." PMC, 2024. 

5. "Towards a Meaningful Communication and Model Aggregation in Federated Learning via Genetic Programming." ICAART 2025. 

6. "Decentralized Federated Learning with Model Caching on Mobile Agents." arXiv 2025. 

7. "FedRAM: A Federated Learning Framework for Multi-Task Learning with Heterogeneous Clients." IEEE TNNLS, 2025. 

8. Dang, Y. et al. "Multi-Agent Collaboration via Evolving Orchestration." NeurIPS 2025. 

9. Microsoft. "Agent Lightning Documentation." 2025. 

10. MiniMax. "Forge: 大规模原生 Agent RL 系统." 2026. 

---

*This document is a living specification. For the latest version, source code, and contribution guidelines, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
