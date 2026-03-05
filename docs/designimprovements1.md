# Mycelium: Dynamic Agent Topology and Federated Configuration Learning

**A Vocabulary of Novel Concepts for Emergent Agent Networks**

**Version 1.0 — June 2026**  
**SuperInstance Open Source Initiative**

This document extends the Mycelium vocabulary with concepts that treat the *connections between agents*—not just the agents themselves—as learnable, adaptable structures. Drawing inspiration from synaptic plasticity in biological neural networks, these ideas enable agent swarms to experiment with different communication topologies, receive feedback on whether those connections improved task performance, and reinforce or prune connections accordingly. Furthermore, federated learning extends beyond model weights to encompass the flow logic between agents, creating muscle memory that resides in the configuration itself rather than in any single agent.

---

## 1. Dynamic Agent Orchestration

### What It Is
Dynamic agent orchestration refers to the ability of a multi-agent system to reorganize which agents communicate with whom, in what order, and with what priority—in real time, in response to task demands. Unlike static pipelines where agent A always feeds into agent B, dynamic orchestration allows the topology to evolve.

### Why It Exists
Static organizational structures struggle to adapt as task complexity and agent numbers grow, resulting in coordination overhead and inefficiencies . In biological systems, neural connections are constantly being formed, strengthened, weakened, and pruned based on activity. Mycelium needs this same plasticity to handle the infinite variety of user tasks without hardcoding interaction patterns.

### How It Works
Recent research proposes a **puppeteer-style paradigm** where a centralized orchestrator dynamically directs agents in response to evolving task states . This orchestrator is trained via reinforcement learning to adaptively sequence and prioritize agents, enabling flexible and evolvable collective reasoning . Key improvements stem from the emergence of more compact, **cyclic reasoning structures** under the orchestrator's evolution—meaning agents learn to form feedback loops and recursive patterns, not just linear chains.

In Mycelium, this orchestrator could be a specialized meta-agent that:
- Monitors task state and agent availability
- Maintains a dynamic graph of agent connections
- Uses RL to propose topology changes
- Receives reward signals based on task completion efficiency

### What Makes It Novel
While multi-agent systems have long studied coordination, the application of reinforcement learning to *evolve the orchestration strategy itself*—rather than just agent policies—is a recent breakthrough . This separates the "how of coordination" from the "what of individual agent behavior."

### Potential Value
- **Adaptability:** The system can handle novel tasks by reorganizing existing agents
- **Efficiency:** Cyclic structures can solve problems that linear pipelines cannot
- **Emergent specialization:** Agents naturally form roles as the orchestrator learns which configurations work best

### Open Questions
- How to prevent the orchestrator from becoming a bottleneck?
- Can orchestration be distributed rather than centralized?
- How to credit individual agents when the topology itself contributed to success?

---

## 2. Hypergraph Coordination Networks

### What It Is
A hypergraph coordination network represents agent relationships using **hypergraphs**—where edges can connect more than two agents simultaneously—rather than simple pairwise graphs. These structures are dynamically constructed and updated based on agent state histories .

### Why It Exists
Pairwise connections miss higher-order relationships. In a biological synapse, one neuron connects to many others, and those connections collectively determine firing patterns. Similarly, agent collaborations often involve groups (e.g., all vision agents pooling information before sending to a planner). Hypergraphs capture these group dynamics naturally.

### How It Works
The HYGMA framework integrates dynamic spectral clustering with hypergraph neural networks :
1. **Dynamic clustering:** Agents' state histories are used to compute similarity; spectral clustering forms dynamic groups.
2. **Hypergraph construction:** Groups become hyperedges connecting multiple agents.
3. **Attention mechanisms:** Within hyperedges, attention weights determine how much each agent's output influences others.
4. **Structural regularization:** A unified objective combines task performance with regularization that encourages beneficial group formations.

This enables **higher-order relationships to emerge naturally from agent interactions** .

### What Makes It Novel
Traditional multi-agent RL focuses on pairwise communication. Hypergraph networks explicitly model group interactions and allow group boundaries to shift over time, much like synaptic clusters in the brain.

### Potential Value
- **Group synergy:** Agents can form temporary coalitions for complex sub-tasks
- **Information efficiency:** Hyperedge-based communication reduces message overhead compared to all-to-all
- **Emergent teamwork:** Agents learn when to form groups and when to dissolve them

### Open Questions
- How to compute spectral clustering efficiently in real-time?
- What similarity metric best captures agent affinity?
- How to balance group cohesion with individual agent specialization?

---

## 3. Synaptic Reinforcement Learning

### What It Is
Synaptic reinforcement learning applies Hebbian principles ("neurons that fire together wire together") to agent connections. Agents that are simultaneously active and contribute to successful outcomes have their connection strength increased; agents that fire together without success (or that interfere) have their connections weakened.

### Why It Exists
In biological brains, learning is not just about updating neuron weights—it's about forming and pruning synapses. Mycelium's agents are already specialized; the next level of adaptation is how they connect. Synaptic RL allows the *topology itself* to be shaped by experience.

### How It Works
- Each directed connection between agents has an associated **synaptic weight** (learned scalar).
- When agent A sends a proposal to agent B, the message is weighted by this synaptic value.
- After task completion, a global reward signal is used to update synaptic weights via a form of **episodic trace**—connections that were active during successful episodes are strengthened.
- Connections that fall below a threshold are pruned; new connections can be formed when agents detect repeated co-activation patterns.

This is inspired by research showing that key improvements in multi-agent systems consistently stem from the emergence of more compact, cyclic reasoning structures .

### What Makes It Novel
Most multi-agent learning focuses on individual agent policies. Synaptic RL treats the *graph topology* as a learnable parameter, enabling the system to discover optimal communication patterns without manual design.

### Potential Value
- **Self-organization:** The swarm develops efficient communication patterns without central orchestration
- **Robustness:** Pruning weak connections reduces noise; forming new connections enables adaptation
- **Interpretability:** Synaptic weights provide a window into how agents are coordinating

### Open Questions
- How to assign credit to individual connections in a long chain?
- What prevents all connections from strengthening uniformly?
- How to balance exploration (trying new connections) with exploitation (using known good ones)?

---

## 4. Federated Configuration Learning

### What It Is
Federated configuration learning extends federated learning beyond model weights to encompass the **flow logic between agents**—the orchestration policies, synaptic weights, and topological structures that define how agents collaborate. Multiple user instances share anonymized configuration updates to improve collective coordination patterns.

### Why It Exists
Individual users benefit from learning how others organize their agent swarms. Just as federated learning improves model weights without sharing data, federated configuration learning improves *how agents work together* without sharing private interaction logs.

### How It Works
Drawing on multi-agent federated learning research  and genetic programming approaches to model aggregation :

1. **Local configuration learning:** Each Mycelium instance evolves its own orchestration policy, synaptic weights, and topology via local experience.
2. **Configuration encoding:** These structures are encoded into a portable format (e.g., graphs with learned parameters).
3. **Secure aggregation:** Only configuration updates (not raw data) are shared with a coordinating server, using differential privacy.
4. **Genetic programming for aggregation:** Rather than simple averaging (which doesn't work for graph structures), genetic programming techniques evolve better aggregation equations .
5. **Selective recombination:** Successful configurations from different users are recombined to create novel hybrid topologies.

### What Makes It Novel
Traditional federated learning aggregates model weights. Configuration learning aggregates *how agents are organized*—a fundamentally different kind of knowledge that operates at the system level rather than the component level.

### Potential Value
- **Cross-user improvement:** Users benefit from collective wisdom about agent organization
- **Privacy-preserving:** Configuration patterns reveal less about individual behavior than raw data
- **Emergent best practices:** The community converges on effective coordination patterns

### Open Questions
- How to represent orchestration policies in a way that enables meaningful aggregation?
- What genetic operators work for graph-based configurations?
- How to prevent malicious configuration updates from propagating?

---

## 5. Proxy Models for Inter-Agent Communication

### What They Are
Proxy models are small, identical models that each client maintains alongside their larger private models. They serve as **agents for information exchange** between clients, enabling heterogeneous model aggregation without sharing sensitive private models .

### Why They Exist
In federated configuration learning, clients may have very different internal agent structures. Directly sharing configuration updates is impossible if the underlying agent architectures differ. Proxy models provide a common substrate for exchange.

### How They Work
The FedType framework introduces this concept :
1. Each client has a large **private model** (unique architecture) and a small **proxy model** (identical across clients).
2. During local training, bidirectional knowledge distillation transfers knowledge between private and proxy models.
3. **Uncertainty-based asymmetrical reciprocity learning** enhances how the proxy guides the private model's learning.
4. Only proxy models are uploaded to the server for aggregation.
5. The aggregated proxy model is then redistributed to clients, where it distills knowledge back into private models.

This eliminates reliance on public data, ensures model security, and achieves efficient communication simultaneously .

### What Makes It Novel
Proxy models decouple *what is learned* (private models) from *what is shared* (proxy models). This enables collaboration across heterogeneous architectures—a long-standing challenge in federated learning.

### Potential Value
- **Heterogeneity tolerance:** Users can keep their preferred agent architectures while still benefiting from collective learning
- **Privacy:** Private models never leave the device
- **Communication efficiency:** Proxy models are much smaller than full configurations

### Open Questions
- How to design proxy models that capture enough information without being too large?
- What distillation loss works best for transferring configuration knowledge?
- Can proxy models themselves be personalized over time?

---

## 6. Multi-Scale Agent Clustering

### What It Is
Multi-scale agent clustering dynamically groups agents at multiple temporal and functional scales simultaneously—micro-clusters for immediate coordination, meso-clusters for task-specific teams, and macro-clusters for long-term strategic alignment.

### Why It Exists
Biological brains operate at multiple scales simultaneously: local circuits handle immediate processing, larger networks coordinate complex behaviors, and global brain regions align overall goals. Mycelium's agents need this same hierarchical organization to handle tasks spanning milliseconds to hours.

### How It Works
Inspired by dynamic spectral clustering approaches , but extended to multiple scales:
- **Micro-scale:** Agents that need to exchange information every few milliseconds (e.g., vision and attention agents) form tight clusters with fast communication channels.
- **Meso-scale:** Agents collaborating on a specific task (e.g., email handling) form looser clusters that persist for minutes.
- **Macro-scale:** Agents aligned with user goals and preferences form stable clusters that evolve over days.

Clusters at different scales can overlap and nest—an agent can belong to multiple clusters simultaneously, just as a neuron participates in many functional circuits.

### What Makes It Novel
Most clustering in multi-agent systems is single-scale. Multi-scale clustering acknowledges that agent relationships are not flat; they operate at multiple temporal and functional resolutions simultaneously.

### Potential Value
- **Hierarchical coordination:** Local decisions don't require global consensus
- **Resource efficiency:** Fast communication confined to micro-clusters; slower communication across scales
- **Emergent hierarchies:** The system naturally develops layered organization

### Open Questions
- How to automatically detect the relevant scales for a given task?
- How to manage conflicts when an agent receives contradictory signals from different-scale clusters?
- How to visualize multi-scale organization for human understanding?

---

## 7. Cyclic Reasoning Structures

### What They Are
Cyclic reasoning structures are agent communication patterns where information flows in loops rather than linear chains—agents can send feedback to previous agents, revisit earlier decisions, and iteratively refine solutions.

### Why They Exist
Recent research reveals that the key improvements in evolving multi-agent collaboration consistently stem from the emergence of more compact, **cyclic reasoning structures** . Linear pipelines are inherently limited; cycles enable refinement, error correction, and emergent problem-solving.

### How They Work
In a cyclic structure:
- Agent A processes input and passes to Agent B
- Agent B's output feeds back to Agent A for refinement
- This loop continues until a stopping criterion is met
- Additional agents can join the cycle as needed

This is analogous to recurrent processing in neural networks, where feedback loops enable complex computations that feedforward networks cannot perform.

### What Makes It Novel
Traditional multi-agent systems are predominantly feedforward. Cyclic structures introduce recurrence at the system level, enabling behaviors like iterative improvement, recursive reasoning, and adaptive refinement.

### Potential Value
- **Error correction:** Agents can catch and fix mistakes
- **Iterative deepening:** Solutions improve with each cycle
- **Emergent recursion:** The system can learn to apply the same reasoning pattern at multiple levels of abstraction

### Open Questions
- How to prevent infinite loops or uncontrolled recursion?
- How to assign credit in cyclic structures (which agent contributed to which refinement)?
- When should a cycle terminate?

---

## 8. Configuration as Muscle Memory

### What It Is
Configuration as muscle memory refers to the idea that optimal agent topologies, once discovered, become **cached configurations** that can be rapidly deployed without relearning. Just as muscle memory allows athletes to execute complex movements automatically, configuration memory allows Mycelium to instantly instantiate proven collaboration patterns.

### Why It Exists
Reinforcement learning agent networks can develop generalized strategies through training . But training a new topology from scratch for every task is inefficient. Configuration memory stores successful patterns for reuse.

### How It Works
- When a particular agent topology proves consistently successful for a class of tasks, it is saved as a **configuration seed** (analogous to behavioral seeds).
- The configuration seed encodes:
  - Which agents are involved
  - Their connection weights/synaptic strengths
  - The orchestration policy (if centralized)
  - Typical task context where this configuration works
- When a new task matches the context, the configuration is loaded and instantiated—agents are woken, connections established, and the system is ready to go in milliseconds.

### What Makes It Novel
This extends the seed concept from *behavioral sequences* to *agent topologies*. Now, not just what agents do, but how they are organized, becomes a portable, reusable artifact.

### Potential Value
- **Instant expertise:** The system can immediately adopt proven collaboration patterns
- **Transfer learning:** Configurations learned in one context transfer to similar contexts
- **Community sharing:** Users can share configuration seeds just as they share behavioral seeds

### Open Questions
- How to encode a topology (graph) into a compact seed vector?
- What makes two task contexts "similar enough" for configuration transfer?
- How to update configurations as agents themselves evolve?

---

## 9. Virtual-Physical Co-Simulation for Topology Learning

### What It Is
Virtual-physical co-simulation involves running agent swarms simultaneously in simulated environments and real environments, with cross-cutting communication loops that enable learning in simulation while executing in reality .

### Why It Exists
Learning optimal agent topologies through real-world trial and error is slow and potentially costly. Simulation allows rapid experimentation with millions of topology variations. But simulations are never perfect; co-simulation bridges the sim-to-real gap.

### How It Works
Drawing on multi-agent teaming research :
- A virtual environment runs a digital twin of the user's device and apps
- Physical agents execute in the real environment
- The multiagent perception-action-communication loop cross-cuts between virtual and physical agents
- Virtual agents can explore risky or unusual topologies without affecting the user
- Successful virtual topologies are gradually migrated to physical agents
- The unified world model (see earlier architecture) is trained on both virtual and physical experiences, improving both simulation fidelity and real-world performance

### What Makes It Novel
While simulation is common in robotics, co-simulation where virtual and physical agents *interact in real time* is an emerging frontier . This enables continuous learning without disrupting the user experience.

### Potential Value
- **Safe exploration:** Radical topology changes can be tested in simulation first
- **Accelerated learning:** Millions of simulated trials per night
- **Continuous adaptation:** The system adapts to changing environments without downtime

### Open Questions
- How to synchronize virtual and physical time when simulations run faster?
- How to transfer topologies learned in simulation to reality?
- What level of simulation fidelity is needed for useful topology learning?

---

## 10. Credit Assignment for Topology Changes

### What It Is
Credit assignment for topology changes is the problem of determining which agent connections and reconfiguration decisions contributed to a successful (or unsuccessful) outcome, and updating those structures accordingly.

### Why It Exists
In a dynamic topology, the configuration itself is part of the solution. If a task succeeds, we need to know: was it because of the agents' individual skills, or because of how they were connected? Both matter, and both need appropriate credit.

### How It Works
Inspired by reinforcement learning for agent systems :
- Each topology change (forming a connection, pruning a connection, adjusting a synaptic weight) is treated as an action with its own value function.
- A hierarchical credit assignment scheme:
  - **Outcome level:** Did the overall task succeed?
  - **Trajectory level:** Which sequences of agent interactions led to success?
  - **Connection level:** Which specific connections were active during successful steps?
- Temporal difference learning propagates credit backward through the interaction graph.
- Structural regularization (from HYGMA ) encourages sparse, interpretable topologies.

### What Makes It Novel
Traditional credit assignment focuses on individual agent actions. Here, the *configuration actions* (changing the topology) also receive credit, enabling the system to learn not just how to act, but how to organize.

### Potential Value
- **Explainability:** We can trace success back to specific structural features
- **Efficient learning:** The system learns both what to do and how to organize to do it
- **Emergent design:** Optimal organizational patterns emerge from first principles

### Open Questions
- How to separate agent skill from configuration quality in credit assignment?
- What timescale is appropriate for topology credit (immediate vs. delayed rewards)?
- How to prevent spurious correlations from reinforcing unhelpful structures?

---

## 11. Emergent Division of Labor

### What It Is
Emergent division of labor refers to the phenomenon where agents, through dynamic topology learning and synaptic reinforcement, naturally specialize into different roles without explicit programming—some become generalists, others specialists; some become coordinators, others executors.

### Why It Exists
In biological systems, division of labor emerges from simple local rules and selection pressures. Mycelium's agents, with their ability to form and prune connections based on success, should exhibit similar emergence.

### How It Works
- Initially, all agents are generalists with random connections.
- Over time, agents that consistently contribute to successful outcomes in certain contexts have their incoming connections strengthened.
- Agents that specialize may become more efficient in their niche, further reinforcing the pattern.
- The orchestrator (if present) learns to route tasks to specialized agents.
- The system develops a functional organization where each agent has a role, but roles can shift as needs change.

This aligns with research showing that multi-agent systems can develop generalized strategies through reinforcement learning  and that collaboration patterns evolve toward efficiency .

### What Makes It Novel
Emergent division of labor is not programmed; it's an *outcome* of the learning dynamics. The system discovers that specialization improves performance, just as biological systems discovered it through evolution.

### Potential Value
- **Scalability:** Specialization reduces interference and improves efficiency
- **Robustness:** If a specialist fails, generalists can temporarily cover
- **Adaptability:** Roles can shift as the environment changes

### Open Questions
- What prevents excessive specialization that reduces flexibility?
- How to measure division of labor quantitatively?
- Can we guide emergence toward desirable role structures?

---

## 12. Topology Seeds

### What They Are
Topology seeds are compact vector representations of agent connection patterns—the graph structure, synaptic weights, and orchestration policies that define how a swarm is organized for a particular class of tasks.

### Why They Exist
Just as behavioral seeds capture *what* agents do, topology seeds capture *how they are organized* to do it. Together, they form a complete specification of a multi-agent solution.

### How They Work
- A topology seed encodes:
  - Agent types involved (references to behavioral seeds)
  - Graph structure (adjacency matrix or edge list, compressed)
  - Synaptic weights for each connection
  - Orchestration policy parameters (if centralized)
  - Context signature (when this topology is appropriate)
- The seed is learned via experience with successful task executions.
- When a new task matches the context signature, the topology seed is loaded, and the appropriate agents are connected accordingly.

This extends the seed concept from behavior to organization—now the *configuration* itself is a portable artifact.

### What Makes It Novel
While behavioral seeds capture *temporal sequences*, topology seeds capture *relational structures*. This completes the picture: a full agent solution requires both what agents do and how they work together.

### Potential Value
- **Complete portability:** Entire multi-agent solutions can be shared as seeds
- **Rapid deployment:** Instantiate proven organizations in milliseconds
- **Composition:** Topology seeds can be combined (e.g., merge two organizational patterns)

### Open Questions
- How to encode graphs compactly while preserving essential structure?
- How to measure similarity between topology seeds?
- Can topology seeds evolve (mutate and recombine) like behavioral seeds?

---

## Conclusion

These concepts collectively describe a vision where agent swarms are not fixed pipelines but dynamic, self-organizing networks that learn both *what to do* and *how to organize* to do it. Drawing on recent advances in dynamic orchestration , hypergraph coordination , multi-agent federated learning , and reinforcement learning for agents , Mycelium can evolve toward truly adaptive, emergent intelligence.

The key insight is that in biological brains, learning happens at multiple levels: neurons adjust their firing, synapses strengthen or weaken, and entire circuits reorganize. Mycelium's agents already learn; now their connections can learn too.

---

## References

1. Dang, Y. et al. "Multi-Agent Collaboration via Evolving Orchestration." NeurIPS 2025. 

2. DSIAC. "Multiagent Federated Learning, Interoperability, and Virtual-Physical Co-simulation." 2025. 

3. Wang, R. et al. "AgentFly: Scalable and Extensible Reinforcement Learning for LM Agents." arXiv 2507.14897, 2025. 

4. "Multi-Agent Collaboration via Evolving Orchestration." Hugging Face Papers, 2025. 

5. "Towards a Meaningful Communication and Model Aggregation in Federated Learning via Genetic Programming." ICAART 2025. 

6. Microsoft. "Agent Lightning Documentation." 2025. 

7. "Multi-Agent Collaboration via Evolving Orchestration." PULRC Portal, 2025. 

8. "Bridging Model Heterogeneity in Federated Learning via Uncertainty-based Asymmetrical Reciprocity Learning." PMC, 2024. 

9. MiniMax. "Forge: 大规模原生 Agent RL 系统." 2026. 

10. Liu, C. & Li, D. "HYGMA: Hypergraph Coordination Networks with Dynamic Grouping for Multi-Agent Reinforcement Learning." ICML 2025. 

---

*For the latest version of this document, visit [github.com/superinstance/mycelium/vocabulary-dynamic](https://github.com/superinstance/mycelium/vocabulary-dynamic).*
