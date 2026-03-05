# Mycelium Architecture

## A Blueprint for Living Intelligence

**Version 1.0 — March 2026**  
**SuperInstance Open Source Initiative**

*This document describes the architecture of Mycelium: what it is, how it works, and why it matters. It is written for developers, researchers, and anyone curious enough to help build it.*

---

## Preface: How to Read This Document

If you have read the Mycelium README, you already know the language. This document is the next step: a complete tour of the system's architecture, layer by layer. It assumes you are familiar with the core terms—agent, swarm, graph, LOG, logline, loom—and builds on them to show how everything fits together.

We will follow the flow of data and control through the system, from sensors to action, from demonstration to memory, from dreaming to collective intelligence. Each component is explained in terms of its purpose, its inputs and outputs, and its connections to other parts.

By the end, you should have a mental model of Mycelium detailed enough to implement, extend, or critique. More importantly, you should see the open spaces—the places where your own ideas could take root.

Let's begin.

---

## Part I: Foundations

### 1.1 The Problem Space

Traditional software is built, not grown. Its behavior is specified in code, compiled, and frozen. It cannot learn from its users, adapt to new contexts, or improve after deployment. This limits every application: a fishing app cannot learn your favorite spots; a study app cannot adapt to your memory patterns; a business tool cannot evolve with your workflow.

Worse, building software is slow and brittle. Each new feature requires writing and debugging code. The logic is opaque, buried in text files. There is no way for users to teach the system directly.

Mycelium inverts this. Instead of programming, you demonstrate. Instead of code, you capture logs. Instead of static binaries, you cultivate a living graph. This shift requires a new architecture—one that is learning, optimizing, and connected.

### 1.2 Design Principles

The architecture is guided by a few core principles:

- **Learning over programming.** The system acquires behavior from demonstration, not specification.
- **Optimization over stasis.** It continuously improves itself through dreaming and feedback.
- **Graph over hierarchy.** All structure is a graph of agents and connections, not a tree of commands.
- **Emergence over control.** Desired behaviors arise from local interactions, not central orchestration.
- **Privacy over collection.** Personal data stays on device; only anonymized patterns are shared.
- **Growth over completion.** The system is never finished; it evolves with its user.

### 1.3 High-Level Overview

At the highest level, Mycelium is a continuous loop:

```
[Sensors] → [Agent Swarm] → [Plinko] → [Executors] → [World]
    ↑           ↑              ↑            ↓           ↓
    └────[Memory]←────[Logger]←──────────[Outcome]─────┘
                           ↓
                      [Dreaming] → [Optimization] → [Sharing]
```

Data flows from sensors into shared memory, where agents read it and write proposals. Plinko selects an action, executors perform it, and the outcome is logged. Periodically—usually overnight—the system dreams: it simulates variations, prunes and grafts connections, and learns from the collective. Improved models and looms are redeployed.

The rest of this document unpacks each piece.

---

## Part II: The Agent Layer

### 2.1 Agents

An **agent** is the fundamental unit of computation. It is a specialized, autonomous process that performs a narrow function. Each agent contains:

- A **neural model** (typically 1–100M parameters) that implements its function.
- A set of **input topics** it subscribes to (e.g., `/sensors/camera`, `/logs/context`).
- An **output topic** where it writes proposals.
- An internal **state** that persists across activations.
- A **value function**—a learned estimate of the worth of its proposed actions.

Agents are not generalists. A vision agent identifies objects in images; a text agent extracts intent from words; a context agent tracks time and location; an executor agent performs actions. Intelligence emerges from their coordination.

**Agent lifecycle:**
- **Hibernated:** Model not in memory; only metadata kept.
- **Loading:** Being loaded from disk.
- **Active:** Loaded and inferencing.
- **Idle:** Loaded but not used recently.
- **Degraded:** Operating with reduced functionality (e.g., due to resource constraints).

The Swarm Manager (see 2.3) controls loading and unloading based on context and usage patterns.

### 2.2 Agent Types

Mycelium defines a growing library of agent types, each with a standard interface. Common types include:

| Type | Function | Inputs | Outputs |
|------|----------|--------|---------|
| **Sightlogger** | Process visual data | Camera frames | Object detections, OCR text |
| **Soundlogger** | Listen for audio cues | Microphone stream | Keywords, sound events |
| **Wordlogger** | Handle text and language | Text input | Intent, entities, sentiment |
| **Statelogger** | Track context | Sensors, system state | Time, location, app, battery |
| **Actlogger** | Execute actions | Action proposals | UI commands, API calls |
| **Storylogger** | Retrieve memories | Observation embedding | Similar past experiences |
| **Watchlogger** | Safety and privacy | Action proposals | Safety score (0-1) |
| **Dreamlogger** | Run dreaming | None (scheduled) | Improved looms |

This list will grow as the community contributes new specializations.

### 2.3 Swarm Manager

The **swarm** is the collection of all active agents. The Swarm Manager is responsible for:

- **Loading and hibernation:** Keeping frequently used agents active, swapping out idle ones.
- **Recruitment:** When Plinko's entropy is high (uncertainty), the manager queries the Model Zoo for agents whose specialization embeddings are similar to the current situation. If none exist, it may spawn a temporary helper agent.
- **Heartbeat monitoring:** Detecting failed agents and marking them as degraded.
- **Resource allocation:** Distributing CPU/GPU time among active agents.

The swarm is implemented as a thread pool with lock-free shared memory for communication. Agents read from input topics and write proposals to output topics; the manager ensures fair scheduling.

### 2.4 Agent Communication

Agents communicate via **topics**—named, typed channels in shared memory. Topics are implemented as lock-free ring buffers to minimize latency. Common topics include:

- `/sensors/camera/frame`
- `/sensors/audio/mfcc`
- `/context/state`
- `/proposals/vision`
- `/proposals/action`
- `/logs/experience`

Any agent can publish to any topic; the swarm manager enforces no access control beyond what is configured. This design allows maximum flexibility and emergent connectivity.

---

## Part III: Data and Memory

### 3.1 Logs

A **log** is a timestamped record of an event or sequence. Every action, every observation, every outcome is logged. Logs are the raw material for learning.

A log entry contains:
- Timestamp
- Session ID
- Observation (compressed latent vector from the world model)
- Action (proposal that was selected)
- Outcome (success/failure, latency, user feedback)
- Context (app, location, system state)

Logs are written to the **logbook** (see 3.3) and also streamed to the experience logger for real-time analysis.

### 3.2 Loglines

A **logline** is a compressed representation of a behavioral pattern. When the system detects a recurring sequence—either through frequency or explicit demonstration—it distills the sequence into a logline vector using the Behavioral Embedding Space (BES) encoder.

Loglines are the primary unit of knowledge in Mycelium. They are:
- **Portable:** Typically 64–1024 floats, easy to store and transmit.
- **Private:** They encode patterns, not raw data; sharing a logline does not expose personal information.
- **Composable:** Loglines can be combined (via weaving) to create new behaviors.
- **Optimizable:** They improve through dreaming.

### 3.3 Logbook

The **logbook** is a local vector database that stores all logs and loglines. It provides:

- **Similarity search:** Given an observation embedding, retrieve the most similar past experiences.
- **Temporal queries:** Retrieve logs within a time range or session.
- **Metadata filtering:** Filter by app, outcome, user feedback.

The logbook is implemented using ChromaDB or LanceDB, with encryption at rest. It lives on the user's device by default; optional encrypted cloud backup can be enabled.

### 3.4 Looms

A **loom** is a logline that has been refined into a reusable, optimized routine. Looms are the "muscle memory" of the system. They can be invoked directly by a prompt or triggered automatically by context.

Internally, a loom may be represented as:
- A small recurrent network that generates actions.
- A grammar production (see 5.2).
- A pointer to a topology seed (see 6.6).

Looms are stored in the **loomery**—a user's personal collection, organized by domain.

### 3.5 Loomcasts

A **loomcast** is a shareable loom, packaged with metadata (author, description, tags, ratings). Loomcasts are the medium of exchange in the Mycelium ecosystem.

---

## Part IV: Decision Making

### 4.1 Proposals

Every agent, when activated, may write a **proposal** to its output topic. A proposal contains:

- `agent_id`
- `action_type` (click, type, apiCall, etc.)
- `target` (element ID, coordinates, URL, etc.)
- `value` – the agent's learned estimate of the action's worth
- `features` – an embedding of the input that led to this proposal

Proposals are timestamped and stored briefly in a ring buffer for Plinko to consume.

### 4.2 Discriminators

**Discriminators** are lightweight neural models that evaluate proposals. They output a multiplier in [0,1] that adjusts the proposal's value. Common discriminators:

- **Safety discriminator:** Trained on human-labeled harmful actions.
- **Coherence discriminator:** Trained to predict whether an action will lead to user correction.
- **Timing discriminator:** Prevents rapid-fire repeated actions.
- **Privacy discriminator:** Blocks actions that might expose sensitive data.

Discriminators are updated periodically using logged feedback.

### 4.3 Plinko

**Plinko** is the stochastic decision layer that selects among competing proposals. Its algorithm:

1. **Collect** all proposals from the current time window.
2. For each proposal, compute **adjusted value** = `value × ∏ discriminator_outputs`.
3. Add **Gumbel noise** for exploration: `log(adjusted_value) + Gumbel(0, τ)`.
4. Compute **selection probabilities** via softmax.
5. **Sample** an action from this distribution.

The temperature `τ` is adapted based on the entropy of the proposal distribution: higher entropy (more disagreement) leads to higher temperature, encouraging exploration.

Plinko is implemented as a separate process that runs every decision interval (e.g., 33ms). Its outputs are sent to the executor layer.

### 4.4 Executors

**Executors** are specialized modules that carry out actions. They translate abstract proposals into concrete commands:

- **UI Executor:** Uses platform accessibility APIs to click, type, scroll.
- **API Executor:** Makes HTTP requests with OAuth handling.
- **File Executor:** Reads/writes files in sandboxed directories.
- **Physical Executor:** Sends commands to robots via ROS2 or MQTT.

Executors log the outcome (success/failure, latency) back to the experience logger.

---

## Part V: Learning and Optimization

### 5.1 World Model

The **world model** is a learned simulator that predicts how the environment will respond to actions. It consists of:

- **Encoder:** Compresses observations into a latent state `z` (VAE).
- **Transition model:** Predicts next latent state given current `z` and action.
- **Reward model:** Predicts user satisfaction (scalar) from latent state.
- **Decoder:** Reconstructs observation from latent state (optional).

The world model is trained on logged experience using a combination of reconstruction loss, prediction loss, and reward prediction loss. Counterfactual augmentation (swapping actions in similar contexts) improves generalization.

### 5.2 Skill Chunker

The **skill chunker** discovers reusable patterns in sequences of logs. It uses grammar induction (e.g., Sequitur) to find frequent subsequences and replace them with nonterminals (skills). The result is a hierarchical grammar where each production is a candidate loom.

The chunker runs periodically (e.g., nightly) on recent logs. Discovered looms are added to the loomery after validation.

### 5.3 Dreaming Engine

The **dreaming engine** improves looms through simulation. It operates at three scales:

- **Micro-dreams:** Apply small Gaussian noise to loom parameters, simulate in world model, keep improvements.
- **Meso-dreams:** Mutate the structure of a loom (swap actions, insert pauses) and simulate.
- **Macro-dreams:** Combine two or more looms via interpolation or concatenation, simulate.

Dreaming runs during idle periods (typically overnight) and produces updated looms. If a new loom outperforms the old one on a validation set, it replaces it.

### 5.4 Behavioral Embedding Space (BES)

The **BES** is a learned latent space where all behaviors (logs, loglines, looms) are mapped to vectors. It is trained on a large corpus of demonstrations using a combination of reconstruction and contrastive loss. The BES enables:

- **Similarity search** for retrieving relevant past experiences.
- **Composition** via vector arithmetic (e.g., `early_morning + cloudy_day`).
- **Privacy** by encoding patterns without storing raw data.

The BES is updated as new logs are collected, but the core mapping is relatively stable.

---

## Part VI: Dynamic Agent Webs

### 6.1 Log Graph

The **log graph** is a weighted, directed graph where nodes are agents and edges are communication channels with learned **synaptic weights**. The graph evolves through:

- **Strengthening:** When agent A's proposal leads to a successful action by agent B, the edge A→B is incremented.
- **Weakening:** When the connection is used in failures or not used, it decays.
- **Pruning:** Edges below a threshold are removed.
- **Grafting:** If two agents are frequently co-activated but not directly connected, a new edge is initialized with a small weight.

The log graph is stored as a sparse matrix and updated via reward-modulated Hebbian learning.

### 6.2 Clustering

Periodically (e.g., nightly), the system performs **spectral clustering** on the log graph to identify functional groups of agents. These clusters are used to:

- Optimize communication: within a cluster, allow richer (e.g., all-to-all) connections; between clusters, maintain sparser links.
- Guide recruitment: when a new task arises, activate agents from relevant clusters.

Clusters are dynamic and can overlap—an agent may belong to multiple groups.

### 6.3 Topology Seeds

A **topology seed** is a compact representation of a learned agent configuration: the nodes, edges, and weights that define a successful collaboration pattern. Topology seeds can be:

- **Shared** with others (via groves or marketplace).
- **Transferred** to new users to bootstrap their graph.
- **Evolved** through recombination.

Topology seeds are stored alongside looms in the model zoo.

---

## Part VII: Collective Intelligence

### 7.1 Federated Learning

Mycelium uses **federated learning** to improve from the entire user population while preserving privacy. Only anonymized patterns—loglines and topology seeds—are aggregated. The process:

1. Each device trains local models (agents, world model, BES) on its own data.
2. Periodically, it sends differentially private updates (gradients or pattern statistics) to a central aggregator.
3. The aggregator computes a global update and distributes it back to devices.

This allows the collective to discover universal patterns while keeping raw data local.

### 7.2 Groves

A **grove** is a community of users who share interests. Groves are implemented as decentralized networks (using ActivityPub or similar) where members can:

- Publish looms and topology seeds.
- Rate and review shared artifacts.
- Discuss techniques and discoveries.

Groves are self-moderating; reputation systems help surface quality contributions.

### 7.3 Marketplace

The **marketplace** is a global exchange for looms and topology seeds. It supports:

- Free and paid listings.
- Cryptographic signatures for provenance.
- Micropayments via traditional or community currencies.

The marketplace accelerates the spread of expertise and incentivizes contribution.

### 7.4 Echo and Current

**Echo** is the phenomenon where a shared pattern returns to its originator, improved by the collective. It is a natural outcome of federated learning: when many users refine a pattern, the aggregated version may surpass the original.

**Current** is a trend—a pattern that is gaining popularity in a domain. Currents are detected by analyzing sharing and usage statistics.

### 7.5 Tapestry

The **tapestry** is the emergent collective intelligence of the whole ecosystem. It is not stored in one place; it exists in the distributed web of shared patterns, ratings, and connections. The tapestry evolves continuously, reflecting the combined experience of all users.

---

## Part VIII: The Human Interface

### 8.1 User Interactions

Users interact with Mycelium through a set of simple verbs:

- **Log in:** Start a demonstration. The system records subsequent actions until told to stop.
- **Replay:** Invoke a loom by name or context.
- **Weave:** Explicitly combine two or more looms (e.g., via a prompt like "weave my morning routine with my cloudy day technique").
- **Cast:** Share a loom as a loomcast.
- **Tune:** Adjust an imported loom to local conditions (e.g., "tune this for my lake").

These interactions can be mediated by voice, text, or GUI, depending on the application.

### 8.2 Translator UI

The **Translator UI** makes the system's internal state visible. It displays:

- A live **mycelium map** showing active agents and their connections.
- **Plinko paths** for recent decisions—what was considered and why.
- **Vitality dashboard** with metrics (coherence, momentum, resonance).
- **Loomery browser** for managing personal looms.

The Translator UI is designed to build trust through transparency and to give users a sense of partnership.

---

## Part IX: Implementation Roadmap

### Phase 1: Core Runtime (0–6 months)
- Implement agent framework with shared memory communication.
- Build Plinko layer with basic discriminators.
- Create logbook with vector search (ChromaDB).
- Develop simple world model and dreaming engine (micro-scale only).
- Release as experimental alpha.

### Phase 2: Learning and Optimization (6–12 months)
- Add grammar-based skill chunker.
- Implement full multi-scale dreaming.
- Develop BES and integrate with loglines.
- Build federated learning infrastructure.
- Release beta with studyLOG and fishingLOG prototypes.

### Phase 3: Collective Intelligence (12–18 months)
- Launch grove protocol and marketplace.
- Implement topology seeds and dynamic agent webs.
- Refine Translator UI based on user feedback.
- Expand agent library with community contributions.
- Release 1.0 with multiple domain applications.

### Phase 4: Ecosystem (18+ months)
- Foster independent application development on the platform.
- Support hardware acceleration (CXL, neuromorphic chips).
- Integrate with robotic systems and IoT.
- Continue research on emergence and collective intelligence.

---

## Part X: Open Research Questions

Mycelium is not just an engineering project; it is a research platform. Many questions remain unanswered, and we invite the community to explore them.

### 10.1 Seed Compression

- What is the optimal latent dimension for loglines?
- How does reconstruction quality scale with sequence length?
- Can we guarantee that a logline captures all necessary information for a task?

### 10.2 Dreaming Effectiveness

- Does dreaming in latent space transfer better than dreaming in action space?
- How many dreaming iterations are optimal per skill?
- What mutation operators work best for different scales (micro/meso/macro)?

### 10.3 Emergent Coordination

- Can we measure emergence using information-theoretic metrics?
- How does the log graph's structure correlate with task performance?
- What prompts encourage beneficial emergence (and discourage harmful)?

### 10.4 Privacy and Security

- How much information can be extracted from a logline? (Membership inference attacks.)
- Can differential privacy protect loglines without destroying utility?
- How to design a secure, decentralized marketplace for looms?

### 10.5 Human-AI Interaction

- What mental models do users form of Mycelium?
- How to calibrate trust in a continuously learning system?
- What explanation interfaces are most effective?

These are not obstacles; they are invitations. Every open question is a place where your contribution could make a difference.

---

## Epilogue: The Garden Grows

This document describes an architecture that does not yet fully exist. Some components are implemented in prototype; others are still on the drawing board. The path from here to a living system is long, but it is walkable—and you are invited to walk it.

Mycelium is not a product to be bought. It is a garden to be cultivated. Every line of code, every experiment, every shared loom adds to the soil. The more of us who tend it, the richer it becomes.

If you see a place where you can help—an unanswered question, a missing component, a better way to explain—join us. The garden is waiting.

*— The Mycelium Team*  
[GitHub](https://github.com/superinstance/mycelium) | [Discord](https://discord.gg/mycelium) | [Lexicon](LEXICON.md) | [Roadmap](ROADMAP.md)
