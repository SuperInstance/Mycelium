# Mycelium: A Vocabulary of Novel Concepts

**Version 1.0 — May 2026**  
**SuperInstance Open Source Initiative**  

This document defines and explores the novel ideas at the heart of the Mycelium architecture. Each concept is explained in terms of its purpose, inner workings, novelty, potential impact, and the open questions that remain. It serves as both a glossary and a conceptual deep dive for researchers, developers, and enthusiasts.

---

## 1. Behavioral Embedding Space (BES)

### What It Is
The Behavioral Embedding Space is a learned low‑dimensional latent space (typically 64–1024 dimensions) where every possible behavior—a sequence of actions in context—is mapped to a vector. Behaviors that are semantically similar (e.g., “check email” and “read messages”) lie close together; distinct behaviors are far apart.

### Why It Exists
BES is the foundation for representing, compressing, and transferring behaviors. It turns the infinite variety of human–computer interaction into a structured, continuous manifold that agents can navigate. Without it, seeds would have to encode raw sequences, which is inefficient and brittle.

### How It Works
- **Training:** A large corpus of demonstrations (state–action sequences) is collected (with user consent). A **behavioral autoencoder** is trained:
  - Encoder: a recurrent or transformer network that compresses a sequence into a latent vector (the seed).
  - Decoder: reconstructs the sequence from the latent.
  - Contrastive loss: pulls embeddings of similar behaviors together, pushes different ones apart.
- **Result:** The latent space becomes organized by behavioral similarity. Interpolation between points yields plausible intermediate behaviors.

### What Makes It Novel
While latent spaces are common in NLP and computer vision, applying them to full behavioral sequences in a multi‑agent, interactive setting is unprecedented. BES enables seeds to be compact, transferable, and privacy‑preserving.

### Potential Value
- **Compression:** A complex behavior (minutes long) becomes a few hundred floats.
- **Transfer:** A seed learned on one agent can be used by another, provided they share the BES.
- **Privacy:** The seed encodes only the “style” of a behavior, not raw data; differential privacy can be applied during training.
- **Composition:** Seeds can be combined via interpolation or attention to create new behaviors.

### Open Questions
- What is the optimal dimension? (Depends on behavior complexity.)
- How to handle variable‑length sequences? (Padding, attention pooling, or hierarchical encoding?)
- Does the space need to be smooth enough for linear interpolation to yield meaningful behaviors?

---

## 2. Seeds

### What They Are
A seed is a compact vector (a point in the Behavioral Embedding Space) that identifies a region of similar behaviors. When fed into a compatible agent, it influences the agent to produce actions consistent with that region.

### Why They Exist
Seeds are the currency of Mycelium. They capture a user’s demonstration in a form that can be stored, shared, and replayed without storing raw data or requiring retraining. They are the embodiment of “behavior as artifact.”

### How They Work
- **Capture:** During a user demonstration, the system records a sequence of (state_latent, action) pairs. This sequence is passed through the BES encoder to produce a seed.
- **Replay:** The seed is loaded into an agent (see *Seed Conditioning*). The agent, given the current state and the seed, acts in a manner consistent with the demonstrated behavior. Because the seed only defines a region, the agent can adapt to environmental variations while maintaining stylistic fidelity.
- **Types:**
  - **Style seeds:** Encode a general approach (e.g., “polite email drafting”). The agent adapts to specifics.
  - **Action seeds:** Encode a fixed sequence (rare, for tasks requiring exact reproduction). Achieved by low temperature and possibly a specialized decoder.

### What Makes Them Novel
Seeds are not just compressed demonstrations; they are points in a structured space that generalizes. This distinguishes them from simple sequence compression or hashing.

### Potential Value
- **Shareability:** A seed can be emailed, sold, or gifted. It’s like a macro for intelligence.
- **Privacy:** A seed does not contain raw data; it’s a behavioral fingerprint.
- **Marketplace:** A seed economy could emerge: “polite email” seeds, “efficient calendar” seeds, etc.

### Open Questions
- How much information about the original user can be inferred from a seed? (Need privacy attacks.)
- Can seeds be watermarked to prevent unauthorized use?
- How to handle versioning when base models evolve?

---

## 3. Seed Conditioning

### What It Is
Seed conditioning refers to the mechanism by which a seed influences an agent’s behavior. The agent is designed to take a seed as an additional input (along with the current state) and produce actions that align with that seed’s region in BES.

### Why It Exists
Without conditioning, seeds would be useless. The agent must be able to “understand” the seed and modulate its behavior accordingly. This is the interface between the static seed and the dynamic agent.

### How It Works
Several approaches are under investigation:
- **Concatenation:** The seed is concatenated with the state vector before being fed into the agent’s policy network. Simple, but may be ignored by the agent.
- **FiLM (Feature‑wise Linear Modulation):** The seed is used to learn scaling and shifting parameters for the agent’s internal activations. More expressive.
- **Cross‑attention:** The seed is treated as a query that attends to the agent’s internal representations. Most flexible, but computationally heavier.
- **Separate policy head:** The seed selects among several sub‑policies within the agent.

The agent is pre‑trained on a diverse set of seeds so that conditioning becomes natural.

### What Makes It Novel
While conditioning is common in multi‑task learning (e.g., task embeddings), applying it to continuous behavioral seeds in a real‑time, multi‑agent system is novel. The challenge is to make conditioning lightweight and non‑destructive to base capabilities.

### Potential Value
- **Modularity:** Agents can host many seeds without retraining.
- **Composition:** Multiple seeds can be combined (e.g., via attention) to produce hybrid behaviors.
- **Lifelong learning:** As new seeds are captured, the agent can incorporate them without forgetting.

### Open Questions
- What is the most effective and efficient conditioning mechanism?
- How does conditioning affect the agent’s performance on tasks unrelated to the seed?
- How many seeds can an agent host before interference occurs?

---

## 4. Market‑Based Plinko Decision Layer

### What It Is
Plinko is a stochastic decision mechanism that selects among competing agent proposals by treating them as bids in a market. Each agent outputs a **value** (learned estimate of the action’s worth), discriminators adjust these values based on safety/coherence, and Gumbel noise injects exploration. Temperature adapts to uncertainty.

### Why It Exists
In a swarm of agents, there must be a way to arbitrate who gets to act. Simple voting or averaging can lead to suboptimal compromises. Plinko frames selection as an economic problem, where agents compete with value estimates, and discriminators act as regulators. This naturally balances exploitation (high‑value bids) with exploration (noise) and safety (discriminators).

### How It Works
1. Each agent computes a **value** for its proposed action (learned via RL, predicting user satisfaction).
2. Discriminators (safety, coherence, timing) output multipliers in [0,1]. Adjusted value = value × product(discriminator outputs).
3. Gumbel noise is added: `log(adjusted_value) + Gumbel_noise * temperature`.
4. Softmax over noisy scores gives selection probabilities; action is sampled.
5. Temperature adapts based on entropy of the probability distribution: higher when agents disagree (uncertainty), promoting exploration.

Agents learn their value functions through experience (reward = user feedback). Discriminators are trained on logged data.

### What Makes It Novel
Market‑based coordination is inspired by multi‑agent economics but rarely applied in real‑time AI systems. The combination of learned values, adaptive temperature, and discriminators is unique. It turns decision‑making into a decentralized, self‑organizing process.

### Potential Value
- **Emergent specialization:** Agents that consistently provide high value in certain contexts will be reinforced, leading to role differentiation.
- **Robustness:** If an agent fails (outputs low value), others can compensate.
- **Interpretability:** The value and discriminator scores can be surfaced to users as explanations.

### Open Questions
- How to stabilize value learning across agents (credit assignment)?
- Can agents collude (e.g., by bidding low to let a friend win)? How to detect/prevent?
- What temperature adaptation function optimizes long‑term learning?

---

## 5. Grammar Induction for Skill Chunking

### What It Is
A method for discovering reusable skills from logged action sequences by inducing a stochastic context‑free grammar (SCFG). Frequent subsequences become grammar productions (skills), and the grammar captures hierarchical structure (skills within skills).

### Why It Exists
Manual skill engineering doesn’t scale. The system must autonomously identify which behavioral patterns are worth reusing. Grammar induction provides a principled, unsupervised way to find structure in action sequences, analogous to how linguists discover grammar from text.

### How It Works
- **Input:** Sequences of atomic actions (each with type and parameters).
- **Algorithm (Sequitur‑inspired):**
  1. Start with a sequence of symbols (actions).
  2. Find the most frequent digram (pair of consecutive symbols).
  3. Replace all occurrences with a new nonterminal (skill), and record a production rule.
  4. Repeat until no digram exceeds a frequency threshold.
- **Result:** A hierarchical grammar where nonterminals represent skills. Each skill can be encoded as a seed (by feeding its expansion through the BES encoder).

### What Makes It Novel
While grammar induction is a classic technique, its application to action sequences for skill discovery in an interactive AI system is novel. It moves beyond simple sequence mining to capture true hierarchical reuse.

### Potential Value
- **Automatic skill discovery:** No human labeling required.
- **Hierarchical planning:** Higher‑level agents can invoke skills as atomic units.
- **Transfer:** Skills learned in one context can be reused in another if the grammar generalizes.

### Open Questions
- How to handle continuous action parameters (e.g., coordinates, text)? Discretize or use parameterized productions?
- How to incorporate the BES to get continuous embeddings for each nonterminal?
- How to evaluate the quality of discovered skills (reusability, transfer, human interpretability)?

---

## 6. Multi‑Scale Dreaming with BES‑Based Mutation

### What It Is
A dreaming engine that runs offline simulations to improve skills. It operates at three temporal scales—micro, meso, macro—each with appropriate mutation operators. Mutations are applied in the BES space (for continuous variation) or at the grammar level (for structural changes).

### Why It Exists
To improve without constant real‑world interaction, the system must “imagine” variations of its skills and keep those that lead to better predicted outcomes. This is analogous to how animals (including humans) consolidate memories and rehearse skills during sleep.

### How It Works
- **Micro‑dreams:** Add small Gaussian noise to the seed in BES space, then simulate the resulting behavior in the world model. Keep variations that yield higher predicted reward.
- **Meso‑dreams:** Apply grammar mutations (insert/delete/swap actions) to the skill’s underlying sequence, then re‑encode to a new seed. Simulate and compare.
- **Macro‑dreams:** Interpolate between two seeds (linear or spherical) or concatenate sequences from two skills to create a hybrid. Simulate and evaluate.

After many simulations, the best‑performing variation becomes the new skill (if it outperforms the current one).

### What Makes It Novel
Dreaming in latent spaces is explored in recent RL research (GW‑Dreamer), but applying it to skill refinement with multi‑scale mutations and BES‑based variation is novel. The combination of continuous and structural mutations allows both fine‑tuning and creative recombination.

### Potential Value
- **Continuous improvement:** Skills get better over time without user effort.
- **Exploration of novel behaviors:** Macro‑dreams can generate entirely new skills by combining existing ones.
- **Personalization:** Dreaming tailors skills to the user’s environment and preferences.

### Open Questions
- How to ensure mutated seeds stay within the manifold of realistic behaviors?
- Does dreaming in BES transfer better to reality than raw action dreaming?
- What is the optimal number of simulations per skill per night?

---

## 7. Agent Specialization Embeddings

### What They Are
Each agent has a learned embedding vector that summarizes its function and expertise. These embeddings are used for similarity matching during dynamic recruitment: when the system needs a capability, it finds agents whose specialization embeddings are closest to the required profile.

### Why They Exist
In a large swarm, we need a way to quickly find agents that can handle novel situations. Specialization embeddings enable efficient, semantic search over the agent population.

### How They Work
- **Training:** A small network is trained to predict agent identity from its input‑output behavior (or from its weights). The penultimate layer becomes the specialization embedding.
- **Usage:** When a novel situation arises (high Plinko entropy), the system computes an embedding of the situation (using the world model encoder) and retrieves agents with similar specialization embeddings (cosine similarity). Top candidates are woken/loaded.

### What Makes It Novel
While agent identification is common, using learned embeddings for capability‑based recruitment in a dynamic swarm is novel. It allows the system to treat agents as a searchable library of expertise.

### Potential Value
- **Efficient scaling:** Only relevant agents are active; others hibernate.
- **Emergent specialization:** Agents that frequently handle certain tasks will develop distinct embeddings, reinforcing their role.
- **Fault tolerance:** If an agent fails, its nearest neighbors can take over.

### Open Questions
- What is the best way to train specialization embeddings? (Behavioral cloning? Contrastive learning?)
- How to update embeddings as agents learn new skills?
- What similarity metric works best? (Cosine, Euclidean, learned?)

---

## 8. Predictive Wake‑Up and ROI‑Based Training Scheduling

### What They Are
- **Predictive wake‑up:** The system predicts when the user will next use the device and schedules overnight training to finish just before that time.
- **ROI‑based training prioritization:** Training tasks (skill chunking, world model update, dreaming) are prioritized by estimated return on investment: expected improvement × frequency / estimated cost.

### Why They Exist
Training is resource‑intensive. To maximize benefit without disrupting the user, the system must decide what to train, when, and whether locally or in the cloud. These mechanisms make training adaptive and efficient.

### How They Work
- **Predictive wake‑up:** A model (e.g., time‑series) learns the user’s usage patterns (time of day, day of week, recent activity). It predicts the next active period, and training is scheduled to complete 5 minutes before.
- **ROI prioritization:** For each candidate task, estimate:
  - Expected improvement (from historical trends or similarity to past tasks).
  - Frequency of use (how often the relevant skill/agent is invoked).
  - Cost (GPU hours, energy, cloud expense). Compute ROI = (improvement × frequency) / cost. Tasks sorted by ROI.

### What Makes Them Novel
While scheduling and prioritization are standard in computing, applying them to a personal AI with learned ROI estimates is novel. It turns training into an economic optimization problem.

### Potential Value
- **User satisfaction:** Training finishes just before the user needs the device, so they always get the latest improvements without waiting.
- **Efficiency:** Resources are spent on tasks that matter most.
- **Privacy‑cost trade‑off:** Users can set a cloud budget; the scheduler respects it.

### Open Questions
- How to accurately estimate expected improvement? (Meta‑learning approach?)
- How to measure frequency in a way that captures future potential (e.g., a skill used rarely but for critical tasks)?
- What to do when predictions are wrong? (Fallback strategies.)

---

## 9. Privacy Mechanisms for Seeds

### What They Are
A suite of techniques to ensure seeds do not leak private information:
- **Differential privacy (DP)** during BES training and seed extraction.
- **Sandboxing** for untrusted seeds.
- **Provenance tracking** and **signatures** for authentication.

### Why They Exist
Seeds capture behavioral patterns that could potentially identify users or reveal sensitive habits. Privacy must be built in from the start to maintain user trust and comply with regulations.

### How They Work
- **DP training:** Train the BES encoder with DP‑SGD, adding noise to gradients to bound the influence of any single demonstration.
- **DP seed extraction:** When extracting a seed from a new demonstration, add a small amount of noise to the embedding.
- **Sandboxing:** Seeds from unknown sources are first run in a restricted environment (e.g., with no access to personal data, limited API calls) to observe behavior.
- **Provenance:** Seeds carry metadata about their creator and a hash of the original demonstration (without revealing it). Signatures from trusted authorities (e.g., skill marketplace) verify authenticity.

### What Makes Them Novel
Applying differential privacy to behavioral embeddings and seeds is novel. It addresses the unique risk that a seed, though abstract, might still be reverse‑engineered to reveal personal information.

### Potential Value
- **User trust:** Clear guarantees that seeds are privacy‑preserving.
- **Regulatory compliance:** Meets GDPR, CCPA, etc., by design.
- **Safe sharing:** Users can share seeds without fear.

### Open Questions
- What ε (privacy budget) is feasible without destroying seed utility?
- How to design provenance without creating a central authority?
- Can seeds be watermarked to detect unauthorized use?

---

## 10. Emergent Properties: Specialization, Resilience, Coordination

### What They Are
These are system‑level behaviors that arise from the interaction of components, not from explicit programming:
- **Specialization:** Agents naturally become experts in certain tasks because they win Plinko bids more often in those contexts.
- **Resilience:** If an agent fails, others with overlapping capabilities take over because Plinko can fall back to lower‑value bids.
- **Coordination:** Agents can implicitly coordinate through shared goals encoded in prompts; explicit communication may also emerge.

### Why They Exist
Emergent properties are the hallmark of complex systems. By designing simple local rules (agent bidding, value learning, discriminators), we hope to see global behaviors that make the system robust and adaptive.

### How They Are Fostered
- **Specialization:** Reinforced through value learning: agents that are good at a task get higher value estimates, win more bids, and are further trained on those tasks.
- **Resilience:** Redundancy in agent capabilities (multiple agents that can perform similar actions) ensures fallback options.
- **Coordination:** Prompts that encourage cooperation (e.g., “work together efficiently”) can be explored. Future versions may include explicit agent communication channels.

### What Makes Them Novel
While emergence is studied in multi‑agent systems, observing it in a real‑world, personal AI context with thousands of users is unprecedented. Mycelium provides a testbed for studying emergence in human‑AI ecosystems.

### Potential Value
- **Adaptability:** The system can handle novel situations without reprogramming.
- **Scalability:** As more agents are added, the system may become more capable, not more brittle.
- **Surprising innovations:** Emergent behaviors could lead to new ways of solving problems that no single agent would discover alone.

### Open Questions
- How to measure emergence? (Information‑theoretic metrics like synergy, redundancy.)
- Can we steer emergence with prompts or incentives?
- What are the failure modes of emergence? (e.g., agents colluding against the user.)

---

## 11. Seed Exchange Protocol

### What It Is
A simple API for exporting and importing seeds, ensuring compatibility and authenticity.

### Why It Exists
Seeds are meant to be shared. A standard protocol allows different Mycelium instances to exchange seeds securely and reliably.

### How It Works
- **Export:** Client requests a seed by skill ID. Server returns the seed embedding plus metadata: required agent types, base model hashes, version info.
- **Import:** Client provides seed data. Server verifies compatibility (agent types match, base model versions are compatible) and optionally checks signature. If all good, the seed is added to the local Model Zoo.

### What Makes It Novel
While file exchange is trivial, the compatibility verification and trust aspects are tailored to the Mycelium ecosystem. The protocol ensures that a seed from one user will work on another’s device, despite possible differences in agent versions.

### Potential Value
- **Ecosystem growth:** A marketplace for seeds becomes possible.
- **Community sharing:** Users can exchange productivity tricks as seeds.
- **Version management:** The protocol can handle upgrades gracefully.

### Open Questions
- How to handle version skew when base models are updated?
- What metadata is necessary for compatibility?
- How to prevent malicious seeds from being distributed?

---

## 12. SPORE Protocol Adaptation

### What It Is
A lightweight messaging protocol for agent communication, adapted from the MyceliumWebServer project. It defines message formats for agent announcements, proposals, heartbeats, and coordination.

### Why It Exists
Agents need a common language to talk to each other and to the swarm manager. SPORE provides a simple, extensible schema.

### How It Works
- Messages are JSON objects with `protocol`, `sender`, `recipient`, `message_id`, `content`, and optional `metadata`.
- Topics (e.g., `/sensors/camera`, `/proposals/vision`) are used for routing.
- The protocol is language‑agnostic and can be implemented over WebSockets, MQTT, or shared memory.

### What Makes It Novel
SPORE is not new per se, but its adaptation to Mycelium’s needs (including seed‑related messages) is a contribution.

### Potential Value
- **Interoperability:** Agents written in different languages can communicate.
- **Extensibility:** New message types can be added without breaking old agents.

### Open Questions
- What security measures are needed (encryption, authentication)?
- How to handle high‑throughput real‑time messages?

---

## Conclusion

These novel concepts form the backbone of Mycelium. Each addresses a specific challenge in building a personal, continuously learning AI system. Together, they create a coherent architecture where behavior is the primary artifact, agents are reusable experts, and the system improves itself through dreaming.

The open questions listed are invitations to research. We invite the community to help answer them and to contribute to the evolution of Mycelium.

---

*For the latest version of this document, visit [github.com/superinstance/mycelium/vocabulary](https://github.com/superinstance/mycelium/vocabulary).*
