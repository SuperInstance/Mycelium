# Dynamic Agent Webs: From Fixed Chains to Adaptive, Self-Optimizing Architectures

**A Mycelium White Paper**  
**May 2026**

---

## The Core Insight

Your observation cuts to the heart of what makes biological intelligence so resilient and adaptive: synapses are not fixed wires—they are dynamic, strengthening with use, weakening with disuse, and constantly being pruned or grown. In Mycelium today, agents communicate through fixed topics and chains of invocation. But what if the connections themselves could learn?

What if the *configuration* of agents—the graph of who talks to whom—became part of the solution space, optimized not by a programmer but by experience, just like the weights inside each agent?

This is not merely an efficiency improvement. It is a paradigm shift: **the application's logic lives in the topology, not just the nodes.** Muscle memory becomes resident in the network structure itself.

---

## Part I: The Biological Blueprint

### Synaptic Plasticity in Brief

Biological neurons don't just adjust their firing thresholds; they constantly remodel their connections:
- **Hebbian plasticity:** "Cells that fire together, wire together." Repeated co-activation strengthens a synapse.
- **Synaptic pruning:** Infrequently used connections weaken and eventually disappear.
- **Homeostatic plasticity:** The overall excitability of a neuron adjusts to maintain stable activity levels.
- **Structural plasticity:** New connections can grow; old ones can be retracted entirely.

### Translating to Agent Swarms

In Mycelium, each agent is like a neuron. But currently, their connections are defined by:
- **Input topics:** Which sensor streams they consume.
- **Output topics:** Where their proposals go.
- **Skill chains:** Fixed sequences of agent invocations (e.g., vision → intent → executor).

What if we made these connections:
- **Weighted:** Some connections are stronger (more influence) than others.
- **Dynamic:** Connection strengths change based on usefulness.
- **Malleable:** New connections can form; useless ones can dissolve.
- **Learnable:** The entire topology optimizes for task success.

---

## Part II: A Framework for Dynamic Agent Webs

### 2.1 Weighted, Directed Agent Graph

We model the agent swarm as a directed graph `G = (V, E, W)` where:
- `V` is the set of agents (nodes).
- `E` is the set of possible communication channels (edges).
- `W: E → [0,1]` assigns a strength to each edge.

An edge from agent A to agent B means: "A's output can influence B's input." The strength determines how much influence.

Initially, edges might be sparse (only those explicitly defined by topics). Over time, they evolve.

### 2.2 The Learning Rule: Multi-Agent Hebbian Plasticity

We need a rule that strengthens useful connections and weakens harmful ones. Inspired by Hebbian learning but adapted for a multi-agent system:

```
Δw_ij = η * (success_signal) * (co_activation - decay * w_ij)
```

Where:
- `Δw_ij` = change in connection strength from agent i to agent j
- `η` = learning rate
- `success_signal` = global or local reward (e.g., user satisfaction, task completion)
- `co_activation` = how often agent i's proposal preceded a successful action by agent j
- `decay` = prevents unbounded growth

This is a form of **reward-modulated Hebbian learning**. It strengthens connections between agents that tend to fire together in successful sequences, and weakens those associated with failures.

**Research grounding:** The HYGMA framework  demonstrates that dynamic spectral clustering on agent state histories enables adaptive group formation, allowing higher-order relationships to emerge naturally from agent interactions. This provides a mathematical foundation for learning connection strengths based on co-activation patterns.

### 2.3 Dynamic Grouping via Spectral Clustering

Agents don't need to connect to everyone. They should form **functional groups**—clusters of agents that frequently work together on subtasks. These groups should be dynamic, forming and dissolving as needed.

We can use **online spectral clustering** on the agent graph:
1. Periodically compute the graph Laplacian of the current weighted agent graph.
2. Find the eigenvectors corresponding to the smallest eigenvalues.
3. Use these to identify clusters (groups of agents with strong mutual connections).
4. Within each cluster, allow richer communication (e.g., all-to-all with learned weights).
5. Between clusters, maintain sparser connections.

The HYGMA framework  shows that this approach enables agents to "figure out their own groupings based on what they're doing... like how soccer players naturally form small groups during a game—defenders work together, forwards coordinate, but these groups change as the game evolves." This is exactly the dynamic we want.

### 2.4 Connection Pruning and Growth

To prevent the graph from becoming a dense, unmanageable tangle, we need mechanisms for:
- **Pruning:** If `w_ij` falls below a threshold for an extended period, the edge is removed entirely.
- **Growth:** If two agents are frequently co-activated but not directly connected, a new edge can be initialized with a small weight.

This mirrors biological synaptic pruning and synaptogenesis. The CoMIX framework  shows that allowing agents to occasionally pursue local strategies independently, rather than mandating constant coordination, can lead to better overall team performance—this suggests that pruning unnecessary connections is not just efficient but functionally beneficial.

---

## Part III: From Chains to Webs—Emergent Agent Architectures

### 3.1 Static Chains vs. Dynamic Webs

**Traditional chain (fixed):**
```
[Vision Agent] → [Intent Agent] → [Executor Agent]
```
This works for known tasks but cannot adapt to novel situations or optimize the pathway.

**Dynamic web (learned):**
```
[Vision Agent] ⇄ [Intent Agent] ⇄ [Context Agent] ⇄ [Executor Agent]
      ↓              ↓              ↓              ↓
[Memory Agent] ⇄ [Safety Agent] ⇄ [Planning Agent]
```
The actual path taken for a given task emerges from the current connection strengths and agent proposals.

### 3.2 How Execution Flows in a Web

1. A trigger (user prompt or sensor event) activates a set of "root agents."
2. These agents produce proposals and broadcast them according to current connection strengths.
3. Agents that receive proposals can themselves produce new proposals, creating a cascade.
4. The Plinko layer selects actions not just from leaf agents, but from any agent whose proposal reaches sufficient adjusted value.
5. The path taken—the sequence of agents that contributed to the final action—is logged.

This is analogous to how activity propagates through a neural network, but here the "network" is composed of discrete, specialized agents with their own internal models.

### 3.3 Learning the Web Itself

After each successful (or failed) task, we have a trace: a subgraph of agents that were activated, with timings and connection strengths used.

We then apply the plasticity rule (Section 2.2) to update connection strengths:
- Strengthen edges along the path of a successful task.
- Weaken edges that were activated but didn't contribute to success.
- Prune edges that consistently fail to participate in successful paths.

Over time, the graph self-organizes into an efficient, task-specific topology. The "muscle memory" for a routine is no longer just a seed in one agent—it's a **learned pathway** through the swarm.

**Research grounding:** The Bottom Up Network (BUN) approach  treats the collective of multi-agents as a unified entity while dynamically establishing connections among agents using gradient information, enabling coordination when necessary while maintaining connections as limited and sparse to effectively manage computational budget. This is precisely the philosophy we need.

---

## Part IV: Beyond Intra-Agent—Inter-Agent Federated Learning

### 4.1 The Current Limitation

Today, federated learning in Mycelium (via LucidDreamer.ai) operates at the model level: agents of the same type share weight updates to improve their individual capabilities. But what about the **configuration** of agents—the graph topology itself?

### 4.2 Learning Topologies Across Users

Different users will develop different optimal agent topologies for similar tasks. One user's email workflow might flow through: `Vision → OCR → Intent → Executor`. Another's might go: `Vision → Context → Intent → Memory → Executor`. Both work, but which is more efficient? Can they learn from each other?

**Proposed mechanism: Federated Topology Learning**

1. Each Mycelium instance periodically exports not just model weights, but a compressed representation of its **agent graph**—the nodes, edges, and learned strengths for a given skill or task domain.
2. These topology snapshots are anonymized and aggregated in a privacy-preserving manner (e.g., using secure aggregation).
3. The aggregated topology statistics (e.g., which connections are most common, which are most correlated with success) are distilled into a **canonical topology template**.
4. Individual instances can use this template as a prior, initializing their own graphs closer to the population optimum, then fine-tuning locally.

This is federated learning applied to **system architecture**, not just model parameters. The "logic of agent flow between the frontal cortex and the muscle fiber" becomes something that can be optimized across the entire user population.

**Research grounding:** Decentralized federated learning with model caching on mobile agents  demonstrates that agents can store and exchange models of agents they encounter, enabling delay-tolerant learning. Extending this to topology representations is a natural next step. The FedRAM framework  addresses multi-task learning with heterogeneous clients, which aligns with the need to balance local specialization with global knowledge sharing.

### 4.3 Meta-Learning the Graph Itself

Going further, we could treat the graph learning process itself as something to be optimized. Different plasticity rules, pruning thresholds, or clustering algorithms might work better for different users or tasks. We could use a **meta-learning** approach:

- The system has a set of candidate graph-learning "strategies" (different hyperparameters, different update rules).
- It periodically evaluates which strategy leads to the fastest improvement in task success.
- The best-performing strategy is selected and itself updated via a slow outer loop.

This creates a hierarchy of learning: agents learn their policies, the graph learns its connections, and the graph-learning algorithm learns its own parameters.

---

## Part V: Implementation Considerations

### 5.1 Graph Storage and Computation

Representing a dynamic graph of hundreds of agents is lightweight:
- Store edges as a sparse matrix (e.g., adjacency list).
- Edge weights can be 16-bit floats.
- Periodically (e.g., nightly) recompute clusters and prune edges.

The spectral clustering step is more expensive but can be run offline during the training window.

### 5.2 Backward Compatibility

Existing agents designed for fixed topics can still participate:
- They continue reading from their specified input topics and writing to output topics.
- The graph layer sits between them, routing messages according to learned weights.
- Over time, as agents are updated, they can be made "graph-aware" (e.g., by including connection strengths as context in their input).

### 5.3 Privacy Considerations

Topology snapshots could reveal behavioral patterns (e.g., which agents you use most). Therefore:
- Snapshots should be aggregated with differential privacy.
- Individual edges should be anonymized (e.g., agent types but not instance IDs).
- Users should opt in to topology sharing.

### 5.4 Cold Start

A new user starts with a default graph (perhaps based on population templates). As they use the system, edges strengthen along their personal workflows. This is analogous to how a newborn brain starts with rough structure that refines through experience.

---

## Part VI: The Vision Realized

With dynamic agent webs and federated topology learning, Mycelium becomes a system that:

1. **Self-organizes:** The swarm finds efficient pathways for common tasks without manual configuration.
2. **Personalizes:** Your graph reflects your unique workflows, learned from your behavior.
3. **Benefits from the crowd:** Population-level topology templates give every user a head start.
4. **Keeps learning:** As your needs change, the graph adapts—pruning old pathways, growing new ones.
5. **Is interpretable:** The graph itself is a map of how the system "thinks" about your tasks. A user (or developer) could inspect it and see, for example, that "every time I check email, these five agents activate in this sequence."

Most importantly, it realizes your insight: **the configuration of agents is the application's solution.** The code is no longer the sole artifact; the learned topology is equally a product of learning, as valuable and shareable as any seed.

---

## Part VII: Open Research Questions

1. **What is the optimal plasticity rule?** Hebbian? Reward-modulated? Something with eligibility traces?
2. **How to balance exploration and exploitation in graph space?** Too much plasticity and the graph churns; too little and it stagnates.
3. **How to measure the "success signal" for connection updates?** Global task reward? Local coherence? A combination?
4. **How to compress topologies for federated learning?** Graph embeddings? Statistical summaries of edge distributions?
5. **How to prevent negative transfer?** If another user's topology is shared, how do we ensure it helps rather than hurts?
6. **What is the right level of abstraction for sharing?** Full graphs? Subgraphs for specific skills? Edge probability distributions?

---

## Conclusion

Your insight—that agents should form dynamic, self-optimizing webs rather than fixed chains—opens a new frontier for Mycelium. By treating the connection graph as learnable, we enable:

- **Emergent coordination:** Agents self-assemble into effective teams for each task.
- **Continuous optimization:** The system's own architecture improves with use.
- **Collective intelligence:** Topologies learned by one user can benefit others.
- **True muscle memory:** Skills reside not just in agents, but in the pathways between them.

This is not merely an incremental improvement. It is a step toward making Mycelium truly alive—a system that not only learns what to do, but learns how to organize itself to do it better.

---

*This document is a living specification. For the latest version, visit [github.com/superinstance/mycelium/research/dynamic-webs](https://github.com/superinstance/mycelium/research/dynamic-webs).*
