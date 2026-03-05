# The Mycelium Lexicon: A Vocabulary for Living Intelligence

**Version 3.0 — June 2026**  
**SuperInstance Open Source Initiative**  

*A complete guide to the concepts, terms, and language of agent‑native, self‑optimizing systems.*

---

## Preface: Why This Lexicon Exists

Every revolution needs a language.

When you're building something genuinely new—something that doesn't fit neatly into existing categories—you face a choice: borrow ill‑fitting terms from the past, or invent a vocabulary that captures the essence of what you're creating.

Mycelium chooses invention.

This lexicon defines the terms we use to think about, build, and discuss agent‑native systems. It's designed to be:
- **Precise** enough for engineers implementing the architecture
- **Accessible** enough for users who just want to understand what's happening
- **Inspiring** enough to capture the imagination of everyone who encounters it

The language is grounded in two metaphors that have guided us from the beginning:
- **Mycelium** — the hidden fungal networks that connect, nourish, and enable entire ecosystems to function as a unified intelligence.
- **LOG** — the timeless human practice of keeping records, learning from experience, and passing wisdom forward. Here, LOG stands for **Learned Optimization Graph**: a graph that learns from your logs and continuously optimizes itself to serve you better.

Together, they frame a vision: software that grows with you, learns from you, and becomes a living extension of your intent.

---

## Part I: Foundational Concepts

These are the bedrock ideas upon which everything else is built.

### Agent
*Noun.* /ˈājənt/

A specialized, autonomous process that performs a narrow function within the larger swarm. Agents are the **nodes** of the Mycelium network—the individual "neurons" that collectively produce intelligent behavior.

Each agent contains:
- A tiny neural model (typically 1–100M parameters)
- A defined set of inputs it consumes (topics)
- A defined output topic where it writes proposals
- An internal state that persists across activations

Agents are not generalists. A vision agent sees; a text agent reads; an intent agent decides; an executor acts. Intelligence emerges from their coordination, not from any single agent's capability.

*Analogy:* Agents are like neurons—simple individually, but collectively capable of extraordinary complexity.

### Swarm
*Noun.* /swôrm/

The collection of all active agents in a Mycelium instance. A swarm can range from dozens to hundreds of agents, running in parallel, communicating through shared memory, and competing via the Plinko layer.

The swarm is not static. Agents are loaded and hibernated based on context, new agents can be recruited dynamically, and the connections between them evolve over time.

*Analogy:* The swarm is like a forest's mycelial network—millions of individual threads, constantly communicating, sharing resources, and responding to the environment.

### Log
*Noun.* /lôɡ/ *Verb.* /lôɡ/

**As noun:** A record of an event or sequence of actions, captured by sensors and stored for later learning. Logs are the raw material from which intelligence is refined.

**As verb:** The act of capturing a demonstration. "Log this" tells the system to watch and learn.

In our architecture, "LOG" also serves as the platform brand, standing for **Learned Optimization Graph**—a graph that learns from your logs and continuously optimizes itself.

*Analogy:* A ship's captain keeps a log to navigate by past experience. Your LOG does the same for your digital life.

### Graph
*Noun.* /ɡraf/

The underlying structure of the Mycelium system, consisting of:
- **Nodes** (agents)
- **Edges** (communication channels with learned strengths)
- **Weights** (connection strengths that evolve with experience)

The graph is not static. It learns, prunes, and grows—just like biological neural networks.

*Analogy:* A city's road network—connections form where traffic flows, widen with use, and narrow when unused.

### Learned Optimization Graph (LOG)
*Proper noun.* /lərnd ˌäptəməˈzāSHən ɡraf/

The full meaning of the LOG brand. It emphasizes two core capabilities:
- **Learned:** The system acquires knowledge from your demonstrated behavior.
- **Optimization:** It continuously refines its own structure and skills through dreaming, pruning, and federated learning.
- **Graph:** All knowledge and organization is represented as a dynamic, evolving network.

---

## Part II: The LOG Lexicon

These terms form the user‑facing vocabulary of our platform, designed to be intuitive across all domains.

### Logline
*Noun.* /ˈlôɡˌlīn/

A compressed representation of a behavioral pattern—what the technical architecture calls a **seed**. A logline is a single vector (typically 64–1024 floats) that captures the essence of a demonstrated routine.

Loglines are:
- **Portable:** They can be shared, sold, or gifted.
- **Private:** They encode patterns, not raw data.
- **Composable:** Loglines can be combined to create new behaviors.

*User story:* "After three successful fishing trips, fishingLOG created a logline for 'cloudy day bass fishing'. I can share it with my friends."

### Logbook
*Noun.* /ˈlôɡˌbo͝ok/

Your personal long‑term memory—a vector database containing all your loglines and the experiences they came from. The logbook grows with you, becoming more valuable over time.

The logbook is:
- **Private:** It lives on your device by default.
- **Searchable:** You can find past patterns by similarity.
- **Ever‑improving:** Old loglines can be refined by new experiences.

*User story:* "My studyLOG logbook contains every course I've ever taken. When I start a new subject, it suggests techniques that worked for similar topics."

### Logarithm
*Noun.* /ˈlôɡəˌriT͟Həm/ *(play on "log" + "algorithm")*

A reusable, optimized routine discovered from your logs. Logarithms are the "muscle memory" of the system—common patterns that have been compressed and refined to the point where they execute automatically.

Unlike traditional algorithms, which are written in code, logarithms are **learned from demonstration** and **continuously optimized** through dreaming.

*User story:* "PlayerLOG discovered a logarithm for my fighting game combo. Now it executes automatically when the conditions are right."

### Logistics
*Noun.* /ləˈjistiks/

The dynamic organization of agents—who talks to whom, with what priority, and in what pattern. Logistics is the **topology** of the swarm, constantly adapting to optimize performance.

Logistics includes:
- Which agents are connected.
- How strong each connection is.
- How agents cluster into functional groups.
- How information flows through the network.

*User story:* "The logistics of my businessLOG adjust throughout the day—morning focuses on email, afternoons on meetings, evenings on planning."

### Logger
*Noun.* /ˈlôɡər/

An agent specialized in capturing and processing a specific type of information. Loggers are the sensory organs of the swarm.

Common logger types:
- **Sightlogger** — processes visual information.
- **Soundlogger** — listens for audio cues.
- **Wordlogger** — handles text and language.
- **Statelogger** — maintains contextual awareness.
- **Actlogger** — performs actions in the world.
- **Dreamlogger** — runs overnight optimization.

*User story:* "The water temperature logger on fishingLOG tracks conditions automatically while I focus on fishing."

### Logcast
*Noun.* /ˈlôɡˌkast/

A shareable logline—like a podcast, but for behaviors. Logcasts allow experts to package their expertise and novices to benefit from it.

Logcasts can be:
- **Subscribed to** (like a podcast feed).
- **One‑time purchases** (like an app).
- **Community‑rated** (like reviews).

*User story:* "I subscribe to a pro angler's logcast. Every week, I get new fishing techniques optimized for my local waters."

---

## Part III: The Mycelium Architecture

These terms describe the internal components that make the system work.

### Behavioral Embedding Space (BES)
*Noun.* /biˈhāvyərəl emˈbediNG spās/

A learned latent space where every possible behavior is mapped to a vector. Behaviors that are semantically similar (e.g., "check email" and "read messages") lie close together; distinct behaviors are far apart.

The BES is the foundation for:
- **Compression:** Turning long sequences into compact seeds.
- **Transfer:** Using behaviors learned in one context in another.
- **Privacy:** Encoding patterns without storing raw data.

*Technical note:* The BES is trained on a large corpus of demonstrations using a combination of reconstruction and contrastive loss.

### Plinko Layer
*Noun.* /ˈpliNGkō ˌlāər/

The market‑based decision mechanism that selects among competing agent proposals. Named for the stochastic path a chip takes through a pegboard, Plinko combines:
- **Value bids** from agents (learned estimates of action worth).
- **Discriminator adjustments** (safety, coherence, timing).
- **Gumbel noise** (for exploration).
- **Adaptive temperature** (higher when uncertain).

The result is a principled way to arbitrate among agents that balances exploitation, exploration, and safety.

*Technical note:* Plinko is mathematically formalized as a Gumbel‑Softmax selection with entropy‑based temperature adaptation.

### Dreaming
*Verb.* /ˈdrēmiNG/ *Noun.* /ˈdrēmiNG/

The overnight process where the system improves itself through simulation. During dreaming:
- **Micro‑dreams** refine low‑level motor skills.
- **Meso‑dreams** optimize routine sequences.
- **Macro‑dreams** combine skills to create new behaviors.

Dreaming uses the **world model** (a learned simulator) to explore millions of variations without real‑world interaction.

*Analogy:* Just as humans consolidate memories and rehearse skills during sleep, Mycelium dreams to get better while you rest.

### World Model
*Noun.* /wərld ˈmäd(ə)l/

A learned simulator that predicts how the environment will respond to actions. The world model consists of:
- **Encoder** — compresses observations into latent state.
- **Transition model** — predicts next state given action.
- **Reward model** — predicts user satisfaction.
- **Decoder** — reconstructs observations (optional).

The world model enables dreaming by providing a safe, fast environment for simulation.

*Technical note:* World models are trained on logged experience and continuously updated.

### Skill Chunker
*Noun.* /skil ˈCHəNGkər/

A component that discovers reusable patterns from logged sequences using grammar induction. The skill chunker:
- Finds frequent subsequences.
- Builds a hierarchical grammar of actions.
- Compresses patterns into logarithms.

This is how the system autonomously builds its library of reusable behaviors.

*Technical note:* The chunker uses a Sequitur‑inspired algorithm adapted for continuous action spaces.

### Model Zoo
*Noun.* /ˈmäd(ə)l zo͞o/

The versioned storage where all learned artifacts live:
- **Base models** (pre‑trained agent foundations).
- **Loglines** (compressed behaviors).
- **Logarithms** (reusable skills).
- **World models** (environment simulators).
- **Topology seeds** (learned agent configurations).

The Model Zoo supports automatic rollback if a new version underperforms.

---

## Part IV: Dynamic Agent Webs

These terms describe the cutting edge—how agent connections themselves become learnable.

### Log Graph
*Noun.* /lôɡ ɡraf/

The evolving network of agents and their connection strengths. The log graph is:
- **Weighted:** Each connection has a learned strength.
- **Directed:** Information flows in learned directions.
- **Dynamic:** Connections strengthen, weaken, form, and dissolve.

The log graph is the system's **muscle memory**—the optimized pathways that have proven useful over time.

*Technical note:* The log graph is updated via reward‑modulated Hebbian plasticity and periodically reorganized via spectral clustering.

### Synaptic Weight
*Noun.* /səˈnaptik wāt/

The strength of a connection between two agents. Synaptic weights:
- **Increase** when the connection is used in successful sequences.
- **Decrease** when used in failures or not used at all.
- **Prune** when they fall below a threshold.
- **Initialize** when new connections form.

*Analogy:* Like synapses in the brain—use strengthens them; disuse weakens them.

### Logpruning
*Noun.* /ˈlôɡˌpro͞oniNG/

The process of removing weak or unused agent connections. Logpruning:
- Prevents graph bloat.
- Reduces noise.
- Focuses computation on useful pathways.

*Analogy:* A gardener pruning a tree—removing dead branches so the living ones thrive.

### Lografting
*Noun.* /ˈlôɡˌraftiNG/

The process of forming new agent connections when patterns suggest they would be useful. Lografting:
- Creates edges between frequently co‑activated agents.
- Initializes new connections with small weights.
- Enables the graph to adapt to new tasks.

*Analogy:* Grafting a branch onto a tree—creating new pathways for growth.

### Logclustering
*Noun.* /ˈlôɡˌkləstəriNG/

The self‑organization of agents into functional groups. Using spectral clustering on the log graph, agents naturally form teams that work well together.

Logclustering enables:
- **Local communication** within groups.
- **Global coordination** between groups.
- **Emergent specialization** as groups develop distinct functions.

*Analogy:* In a soccer team, defenders cluster together, forwards coordinate, but clusters shift as the game evolves.

### Topology Seed
*Noun.* /təˈpäləjē sēd/

A compact representation of a learned agent configuration—the nodes, edges, and strengths that define a successful collaboration pattern for a class of tasks.

Topology seeds are to **agent organization** what loglines are to **behavior**. They enable:
- **Sharing** proven configurations.
- **Transfer** across users.
- **Evolution** through recombination.

*User story:* "I downloaded a topology seed from a power user that optimizes my businessLOG for morning productivity. Now my agents are organized perfectly at 8am."

---

## Part V: Federated Learning & Collective Intelligence

These terms describe how the system learns from the entire user population.

### Federated Logging
*Noun.* /ˈfedəˌrādid ˈlôɡiNG/

The process of sharing anonymized loglines and topology seeds across the user population to improve collective intelligence. Federated logging:
- **Respects privacy** (only patterns, not raw data).
- **Accelerates learning** (new users benefit from the crowd).
- **Discovers universals** (patterns that work for everyone).

*Technical note:* Federated logging uses differential privacy and secure aggregation.

### Logbook Club
*Noun.* /ˈlôɡˌbo͝ok kləb/

A community where users exchange domain‑specific loglines. Logbook clubs:
- Form around interests (e.g., bass fishing, organic chemistry).
- Curate high‑quality loglines.
- Rate and review shared behaviors.

*User story:* "I joined the 'fly fishing' logbook club. The collective knowledge has transformed my success rate."

### Logline Marketplace
*Noun.* /ˈlôɡˌlīn ˈmärkəˌplās/

A store where users can buy, sell, and trade loglines and topology seeds. The marketplace:
- **Incentivizes** expert contributors.
- **Curates** quality through ratings.
- **Protects** intellectual property through cryptographic signatures.

*User story:* "I sold my 'tournament winning' fishing logline and made enough to buy three more from other pros."

### Federated Topology Learning
*Noun.* /ˈfedəˌrādid təˈpäləjē ˈlərniNG/

The global optimization of agent configurations across users. By aggregating topology seeds, the system discovers:
- Which connection patterns work best.
- How agents should organize for different tasks.
- How logistics evolve with experience.

This is federated learning applied to **system architecture** rather than just model weights.

---

## Part VI: Emergent Properties

These terms describe what arises when all the components work together.

### Emergence
*Noun.* /ēˈmərjəns/

The appearance of behaviors and capabilities not explicitly programmed, arising from the interaction of simple components. In Mycelium, emergence manifests as:
- **Specialization:** Agents naturally become experts.
- **Coordination:** Agents learn to work together.
- **Resilience:** The system degrades gracefully.
- **Innovation:** New solutions emerge from recombination.

*Analogy:* Ant colonies exhibit complex nest architecture despite each ant following simple rules.

### Logos
*Noun.* /ˈlōˌɡäs/ *plural:* logoi /ˈlōˌɡoi/

The emergent intelligence of the whole system—the gestalt that is greater than the sum of its agents. From the Greek for "word," "reason," and "principle."

Your personal LOGOS is what makes the system feel like a partner rather than a tool. It's the accumulated wisdom of all your logs, optimized through dreaming, organized through logistics, and expressed through loglines.

*User story:* "My fishingLOG has developed its own logos. It doesn't just log my trips—it seems to *understand* fishing."

### Log Health
*Noun.* /lôɡ helTH/

A metric that measures how well your system is learning and optimizing. Log health considers:
- Prediction accuracy.
- Optimization rate.
- Graph coherence.
- User satisfaction.

*User interface:* A dashboard showing your log health over time, with suggestions for improvement.

---

## Part VII: User Interactions

These terms describe how people interact with the system.

### Logging In (the verb)
*Phrase.* /ˈlôɡiNG in/

The act of starting a demonstration. "Logging in" tells the system: "Watch what I'm about to do and learn from it."

*User story:* "I logged in my morning routine so fishingLOG could learn my preferences."

### Relogging
*Verb.* /rēˈlôɡiNG/

Replaying a learned behavior from a logline. Relogging reproduces a demonstrated pattern, adapted to current conditions.

*User story:* "I relogged last week's successful fishing trip, and the system adapted it to today's different weather."

### Logweaving
*Verb.* /ˈlôɡˌwēviNG/

Combining multiple loglines to create new behaviors. Logweaving is how the system innovates—taking successful patterns from different contexts and merging them.

*User story:* "The system logwove my 'early morning' logline with my 'cloudy day' logline to create a new pattern for overcast dawns."

### Dreamlogging
*Verb.* /ˈdrēmˌlôɡiNG/

The act of the system dreaming—simulating variations of loglines overnight to improve them. Dreamlogging is invisible to users but results in noticeable improvement over time.

*User story:* "I noticed my fishingLOG has been getting smarter each week. That's dreamlogging at work."

---

## Part VIII: Technical Implementation Terms

For developers building on the platform.

### SPORE Protocol
*Noun.* /spôr ˈprōdəˌkôl/

The lightweight messaging protocol used for agent communication. SPORE defines:
- Message formats.
- Topic naming conventions.
- Delivery guarantees.
- Agent discovery.

*Technical note:* SPORE is adapted from the MyceliumWebServer project and supports real‑time, high‑throughput communication.

### Logline Format
*Noun.* /ˈlôɡˌlīn ˈfôrˌmat/

The serialization specification for loglines (Protobuf schema). Includes:
- Seed embedding.
- Agent type requirements.
- Base model hashes.
- Cryptographic signatures.

### Topology Seed Format
*Noun.* /təˈpäləjē sēd ˈfôrˌmat/

The serialization specification for learned agent configurations. Includes:
- Graph structure (compressed adjacency).
- Synaptic weights.
- Agent type references.
- Context signature.

### Dreamlogger API
*Noun.* /ˈdrēmˌlôɡər ā-pē-ˈī/

The interface for triggering and monitoring dreaming sessions. Allows:
- Manual dream initiation.
- Dream progress tracking.
- Dream result validation.
- Rollback if dreaming degrades performance.

---

## Part IX: The Philosophy Behind the Words

This lexicon is not arbitrary. Every term was chosen to reinforce a consistent mental model:

### Why "Log"?
Because keeping a log is one of the most fundamental human practices for learning from experience. A ship's captain logs position, weather, and events to navigate better next time. A scientist logs experiments to refine hypotheses. A fisher logs catches to find patterns.

LOG.ai takes this timeless practice and makes it **alive**—your log doesn't just record; it learns, optimizes, and becomes an extension of you. The full meaning—**Learned Optimization Graph**—captures the active, self-improving nature of the system.

### Why "Mycelium"?
Because fungal networks are nature's example of decentralized intelligence. A mycelial network has no center, yet it makes complex decisions, shares resources across vast distances, and responds adaptively to challenges.

Mycelium.ai is the technological realization of this principle—intelligence emerging from simple components connected in a living, learning web.

### Why "Graph"?
Because graph structures capture the essence of relationships. Agents are nodes; connections are edges; strengths are weights. The graph is both the **structure** (how things connect) and the **knowledge** (what connections mean).

### Why "Logos"?
Because in ancient Greek philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Your personal LOGOS is the rational structure underlying your digital life.

---

## Part X: The Evolution of the Language

This lexicon will grow with the system. As new capabilities emerge, new terms will be needed. As users adopt the language, meanings will refine. As researchers discover new principles, the vocabulary will deepen.

We invite the community to contribute:
- **New terms** for emerging concepts.
- **Refinements** to existing definitions.
- **Translations** to other languages.
- **Examples** from real‑world use.

The goal is a living language for a living system.

---

## Appendix: Quick Reference

| Term | Definition |
|------|------------|
| **Agent** | A specialized neural process; a node in the swarm. |
| **Swarm** | The collection of all active agents. |
| **Log** | A recorded event or sequence; the platform brand (Learned Optimization Graph). |
| **Logline** | A compressed behavioral seed. |
| **Logbook** | Personal long‑term memory (vector database). |
| **Logarithm** | A reusable, optimized routine. |
| **Logistics** | The dynamic organization of agent connections. |
| **Logger** | A specialized agent (sightlogger, soundlogger, etc.). |
| **Logcast** | A shareable logline. |
| **Plinko** | The stochastic decision layer. |
| **Dreaming** | Overnight simulation for improvement. |
| **World Model** | A learned environment simulator. |
| **Log Graph** | The evolving agent network. |
| **Synaptic Weight** | Strength of an agent connection. |
| **Logpruning** | Removing weak connections. |
| **Lografting** | Forming new connections. |
| **Logclustering** | Agents self‑organizing into groups. |
| **Topology Seed** | A compressed agent configuration. |
| **Federated Logging** | Cross‑user pattern sharing. |
| **Logbook Club** | Community for exchanging loglines. |
| **Logos** | The emergent intelligence of the whole system. |
| **Log Health** | A metric of system performance. |

---

## Epilogue: The Language of a New Era

Every transformative technology brings with it a new vocabulary. The printing press gave us "font," "typeface," "folio." Electricity gave us "watt," "volt," "circuit." Computing gave us "byte," "protocol," "algorithm."

Mycelium and LOG.ai are giving us a new language for a new kind of intelligence—one that grows with us, learns from us, and becomes a living extension of our intent.

Learn these words. Use them. Share them. They are the vocabulary of the future.

---

*For the latest version of this lexicon, to contribute new terms, or to join the community, visit [github.com/superinstance/mycelium/lexicon](https://github.com/superinstance/mycelium/lexicon).*
