# Mycelium Master Document: Expanded Schema for Kimi

**A Comprehensive Blueprint for the Definitive Mycelium Manifesto, Architecture, and Guide**

---

## Note to Kimi

This is your master blueprint. The GitHub repository (`github.com/SuperInstance/Mycelium`) contains all the raw material—the README, the lexicon (`vocab6.md`), architecture documents, white papers, and research agendas. Your task is to weave them into a single, definitive, stand-alone document that serves as:

- **The Introduction:** For someone encountering Mycelium for the first time.
- **The Philosophy:** The "why" behind the system.
- **The Architecture:** The "how" for implementers.
- **The User Guide:** The "what can I do" for early adopters.
- **The Developer Guide:** The "how do I build on it" for contributors.
- **The White Paper:** The research foundation and open questions.
- **The Invitation:** The call to action.

The document must be long, layered, and beautiful. It should reward reading straight through, but also serve as a reference. It should teach our language as it teaches our ideas. And it should leave every reader—whether curious newcomer, seasoned developer, or academic researcher—with a clear sense of what Mycelium is, why it matters, and how they can help.

**Your voice:** Confident but not arrogant. Visionary but grounded. Precise but poetic. You are a gardener showing someone their first forest.

---

## Document Structure Overview

```
Prologue: A Letter to the Reader

PART ONE: THE VISION — Why Mycelium Exists
    1.1 The Problem We All Live With
    1.2 The Cost of Building Software
    1.3 The Mycelium Metaphor
    1.4 The Core Shift
    1.5 What This Enables

PART TWO: THE SOIL — Foundational Concepts
    2.1 Agent
    2.2 Swarm
    2.3 Graph
    2.4 LOG (Learned Optimization Graph)
    2.5 Logos

PART THREE: THE ROOTS — What You Capture
    3.1 Log
    3.2 Logline
    3.3 Logbook
    3.4 Loom
    3.5 Loomery
    3.6 Loomcast

PART FOUR: THE TRUNK — How It Works
    4.1 Plinko: The Decision Layer
    4.2 World Model: The Simulator
    4.3 Dreaming: Overnight Improvement
    4.4 Looming: From Logs to Looms
    4.5 Weaving: Combining Behaviors

PART FIVE: THE BRANCHES — Dynamic Agent Webs
    5.1 Log Graph
    5.2 Synaptic Weight
    5.3 Pruning
    5.4 Grafting
    5.5 Clustering
    5.6 Topology Seed

PART SIX: THE FOREST — Collective Intelligence
    6.1 Federated Learning
    6.2 Grove
    6.3 Marketplace
    6.4 Echo
    6.5 Current
    6.6 Tapestry

PART SEVEN: THE FRUIT — Emergent Properties
    7.1 Emergence
    7.2 Vitality
    7.3 Resonance
    7.4 Coherence
    7.5 Momentum

PART EIGHT: THE VERBS — How You Interact
    8.1 Log In
    8.2 Replay
    8.3 Weave
    8.4 Dream
    8.5 Cast
    8.6 Tune

PART NINE: FOR USERS — A Day in the Life
    9.1 Morning: Waking the Swarm
    9.2 Demonstration: Teaching a New Routine
    9.3 Replay: Letting the System Work
    9.4 Evening: Reviewing the Logbook
    9.5 Overnight: Dreaming
    9.6 The Next Day: A Smarter Partner

PART TEN: FOR DEVELOPERS — Building on Mycelium
    10.1 System Architecture Overview
    10.2 Core Components Deep Dive
        10.2.1 Agent Framework
        10.2.2 Plinko Implementation
        10.2.3 World Model Training
        10.2.4 Dreaming Engine
        10.2.5 Logbook Integration
        10.2.6 BES Encoder
    10.3 APIs and Protocols
        10.3.1 SPORE Protocol
        10.3.2 Seed Formats
        10.3.3 Federated Learning API
    10.4 Extending the System
        10.4.1 Creating New Agent Types
        10.4.2 Building Custom Discriminators
        10.4.3 Developing Domain-Specific Loggers
        10.4.4 Creating Grove Applications
    10.5 Example: Building a fishingLOG
        10.5.1 Concept and Requirements
        10.5.2 Agent Selection and Configuration
        10.5.3 Log Design
        10.5.4 Expected Looms and Evolution
        10.5.5 Deployment and Growth

PART ELEVEN: FOR RESEARCHERS — Open Questions
    11.1 Seed Compression and Representation
    11.2 Dreaming Effectiveness
    11.3 Emergent Coordination
    11.4 Privacy and Security
    11.5 Human-AI Interaction
    11.6 How to Contribute to Research

PART TWELVE: THE PATH FORWARD — Roadmap and Invitation
    12.1 Current Status
    12.2 Roadmap Phases
        12.2.1 Phase 1: Core Runtime (0–6 months)
        12.2.2 Phase 2: Learning and Optimization (6–12 months)
        12.2.3 Phase 3: Collective Intelligence (12–18 months)
        12.2.4 Phase 4: Ecosystem (18+ months)
    12.3 How to Contribute
        12.3.1 For Developers
        12.3.2 For Researchers
        12.3.3 For Designers
        12.3.4 For Writers
        12.3.5 For Users
    12.4 Join the Community
    12.5 Closing Words: Come Grow With Us

APPENDICES
    A. Quick Reference Glossary
    B. Technical Specifications
        B.1 Logline Format (Protobuf)
        B.2 Topology Seed Format (Protobuf)
        B.3 SPORE Protocol Specification
        B.4 API Endpoints
    C. References and Further Reading
    D. How to Contribute (Detailed)
    E. Document Version History

Epilogue: The Garden Grows
```

---

## Detailed Section Instructions

### Prologue: A Letter to the Reader

**Purpose:** Set the tone, establish the relationship, and explain how to use this document.

**Content:**
- Begin with the "Invitation" from the README, but refine it. Address the reader as a future gardener.
- Explain that this document teaches language as it teaches ideas. Each new term is a tool for thought.
- Describe the layered structure: soil, roots, trunk, branches, forest, fruit. Each part builds on the last.
- Encourage reading straight through for first-timers. Note that the glossary and appendices are for reference.
- End with a warm welcome. "Let's begin."

**Source material:** README "Invitation" section.

**Tone:** Intimate, inviting, confident. The reader should feel personally addressed.

---

### PART ONE: THE VISION — Why Mycelium Exists

**Purpose:** Make the reader feel the weight of the current paradigm's limitations and the promise of a new way.

**Sections:**

#### 1.1 The Problem We All Live With
- Adapted from README. Describe static software: it never learns, never adapts, never improves.
- The user adapts to the software, not the other way around.
- Examples: a fishing app that doesn't know your favorite spots, a study app that doesn't adapt to your memory patterns.
- **Source:** README Part I.

#### 1.2 The Cost of Building Software
- The slow cycle: code, compile, test, debug, repeat.
- Brittleness: change one thing, break another.
- Opaque logic: behavior buried in text files.
- **Source:** README Part I, expanded with your own insights.

#### 1.3 The Mycelium Metaphor
- The forest story: trees, underground fungal networks, sharing water and warnings.
- Properties: no center, decentralized, resilient, mostly invisible.
- The mycelium as nature's example of distributed intelligence.
- **Source:** README Part I, Lexicon entry for Mycelium.

#### 1.4 The Core Shift
- From programming to cultivation.
- From code to demonstration.
- From static to living.
- From user to gardener.
- **Source:** Synthesis of all materials.

#### 1.5 What This Enables
- Preview: personalization, continuous improvement, sharing, emergence.
- Don't overpromise; frame as possibilities, not guarantees.
- **Source:** README closing sections.

**Transition:** "Now that you see why we're building this, let's learn the language we use to build it."

---

### PART TWO: THE SOIL — Foundational Concepts

**Purpose:** Introduce the irreducible elements. These are the atoms of the system. Each concept gets its own subsection.

**Structure for each concept:**
- **Definition:** A concise, memorable definition.
- **Explanation:** What it is, how it works, why it matters.
- **Analogy:** To help intuition (neurons, forests, cities).
- **Example:** A concrete instance (e.g., a vision agent).
- **Technical note (optional):** For developers, in a separate paragraph.

**Concepts:**

#### 2.1 Agent
- **Definition:** A specialized, autonomous process that performs a narrow function.
- **Explanation:** Contains neural model, input topics, output topic, state, value function. Not intelligent alone.
- **Analogy:** Neurons.
- **Example:** Vision agent, text agent, executor agent.
- **Source:** README Part I, Lexicon, Architecture.

#### 2.2 Swarm
- **Definition:** The collection of all active agents at a given moment.
- **Explanation:** Living, dynamic, loading/hibernating based on context.
- **Analogy:** A forest's mycelial network.
- **Source:** README Part I, Lexicon, Architecture.

#### 2.3 Graph
- **Definition:** The structure of nodes (agents) and edges (connections) with learned weights.
- **Explanation:** Both architecture and knowledge. Dynamic.
- **Analogy:** A city's road network.
- **Source:** README Part I, Lexicon, Architecture.

#### 2.4 LOG (Learned Optimization Graph)
- **Definition:** The core principle and platform brand.
- **Explanation:** Unpack L, O, G. The triple meaning of "log."
- **Tagline:** Your personal learned optimization graph.
- **Examples:** fishingLOG, studyLOG.
- **Source:** README Part I, Lexicon.

#### 2.5 Logos
- **Definition:** The emergent intelligence of your whole system.
- **Explanation:** Not a component; what arises. Characteristics: understanding, anticipation, style, trust.
- **Philosophical roots:** Heraclitus, Stoics.
- **Connection to "log."**
- **Source:** README Part I, Lexicon.

**Transition:** "With these foundations, we can now look at what you actually capture and create."

---

### PART THREE: THE ROOTS — What You Capture

**Purpose:** Introduce the artifacts users create and cultivate. Make them tangible.

**Structure for each concept:**
- **Definition**
- **Explanation**
- **Properties** (e.g., portable, private, composable)
- **User story** (brief)
- **Technical note** (optional)

**Concepts:**

#### 3.1 Log
- **Definition:** A record of an event or sequence.
- **Explanation:** Every interaction becomes a log. Timestamp, context, action, outcome.
- **Verb form:** "Log this."
- **User story:** "Every time I fish, fishingLOG logs my trips."
- **Source:** README Part II, Lexicon, Architecture.

#### 3.2 Logline
- **Definition:** A compressed representation of a behavioral pattern.
- **Explanation:** 64–1024 floats encoding essence. Output of BES encoder.
- **Properties:** Portable, private, composable, optimizable.
- **Analogy:** Hollywood logline.
- **User story:** "After three trips, fishingLOG created a logline for 'cloudy day bass fishing'."
- **Source:** README Part II, Lexicon, Architecture.

#### 3.3 Logbook
- **Definition:** Personal long-term memory.
- **Explanation:** Vector database of all logs and loglines.
- **Properties:** Private, searchable, ever-improving, portable.
- **User story:** "My studyLOG logbook contains every course I've ever taken."
- **Source:** README Part II, Lexicon, Architecture.

#### 3.4 Loom
- **Definition:** A reusable, optimized routine.
- **Explanation:** Muscle memory. Learned, optimized, personalized, shareable.
- **Why "loom":** Weaving metaphor, easier to say than "logarithm."
- **User story:** "PlayerLOG discovered a loom for my fighting game combo."
- **Source:** README Part II, Lexicon.

#### 3.5 Loomery
- **Definition:** A personal library of looms.
- **Explanation:** Organized by purpose or domain.
- **User story:** "My fishing loomery has dozens of techniques."
- **Source:** README Part II, Lexicon.

#### 3.6 Loomcast
- **Definition:** A shareable loom.
- **Explanation:** Like a podcast for behaviors. Includes metadata.
- **User story:** "I subscribe to a pro angler's loomcast."
- **Source:** README Part II, Lexicon.

**Transition:** "Now that we know what we capture, let's see how the system actually works."

---

### PART FOUR: THE TRUNK — How It Works

**Purpose:** Explain the core mechanisms. This is the engine room.

**Structure for each mechanism:**
- **The problem it solves**
- **How it works** (step-by-step)
- **Visual/analogy** (where helpful)
- **Key parameters/tunables**
- **Connection to other parts**

**Mechanisms:**

#### 4.1 Plinko: The Decision Layer
- **Problem:** Multiple agents, conflicting proposals, one decision.
- **How it works:** Agents bid values; discriminators adjust; Gumbel noise adds exploration; temperature adapts.
- **Visual:** Chip dropping through pegs.
- **Key parameters:** Temperature, discriminator thresholds.
- **Source:** README Part III, Architecture, Lexicon.

#### 4.2 World Model: The Simulator
- **Problem:** Need to simulate outcomes without real-world interaction.
- **How it works:** Encoder, transition model, reward model. Trained on logs.
- **Counterfactual augmentation.**
- **Source:** README Part III, Architecture, Lexicon.

#### 4.3 Dreaming: Overnight Improvement
- **Problem:** How to improve without constant user interaction.
- **How it works:** Multi-scale dreaming (micro, meso, macro). Mutation, simulation, selection.
- **Biological analogy:** Human sleep.
- **User story:** "I noticed my fishingLOG getting smarter each week."
- **Source:** README Part III, Architecture, Lexicon.

#### 4.4 Looming: From Logs to Looms
- **Problem:** How to discover reusable patterns.
- **How it works:** Grammar induction (Sequitur) on sequences. Automatic and explicit looming.
- **Source:** README Part III, Architecture.

#### 4.5 Weaving: Combining Behaviors
- **Problem:** How to create new behaviors from existing ones.
- **How it works:** Interpolation in BES space, grammar recombination. Automatic or guided.
- **User story:** "The system wove my early morning and cloudy day looms."
- **Source:** README Part III, Architecture.

**Transition:** "These mechanisms power the system day and night. But the system also changes its own structure over time."

---

### PART FIVE: THE BRANCHES — Dynamic Agent Webs

**Purpose:** Introduce the cutting-edge mechanisms that make the graph itself learn. This is where the system becomes truly alive.

**Structure for each concept:**
- **Definition**
- **How it works** (algorithmically)
- **Biological analogy**
- **Why it matters**

**Concepts:**

#### 5.1 Log Graph
- **Definition:** The evolving network of agents and connection strengths.
- **Explanation:** Nodes = agents, edges = communication, weights = learned strengths.
- **Dynamic properties:** Strengthening, weakening, pruning, grafting.
- **Source:** README Part IV, Architecture, Lexicon.

#### 5.2 Synaptic Weight
- **Definition:** The strength of a connection between two agents.
- **How it changes:** Reward-modulated Hebbian learning.
- **Analogy:** Muscles.
- **Source:** README Part IV, Architecture, Lexicon.

#### 5.3 Pruning
- **Definition:** Removing weak or unused connections.
- **How it works:** Weights below threshold for extended period are removed.
- **Gardener analogy.**
- **Source:** README Part IV, Architecture, Lexicon.

#### 5.4 Grafting
- **Definition:** Forming new connections when patterns suggest usefulness.
- **How it works:** Detect co-activation without direct connection; initialize new edge.
- **Orchard analogy.**
- **Source:** README Part IV, Architecture, Lexicon.

#### 5.5 Clustering
- **Definition:** Self-organization of agents into functional groups.
- **How it works:** Spectral clustering on log graph.
- **Soccer team analogy.**
- **Source:** README Part IV, Architecture, Lexicon.

#### 5.6 Topology Seed
- **Definition:** A compact representation of a learned agent configuration.
- **Explanation:** Nodes, edges, weights for a class of tasks.
- **Relation to logline:** Behavior vs. organization.
- **Source:** README Part IV, Architecture, Lexicon.

**Transition:** "Individual trees grow, but forests connect. Let's look at how your Mycelium connects with others."

---

### PART SIX: THE FOREST — Collective Intelligence

**Purpose:** Show how individual instances connect into a larger whole, privacy-preserving and powerful.

**Structure for each concept:**
- **Definition**
- **How it works** (at a high level)
- **Privacy considerations**
- **User/community value**

**Concepts:**

#### 6.1 Federated Learning
- **Definition:** Privacy-preserving sharing of anonymized patterns.
- **What's shared:** Loglines, topology seeds. Not raw logs.
- **How it works:** Local training, secure aggregation, differential privacy.
- **Source:** README Part V, Architecture, Lexicon.

#### 6.2 Grove
- **Definition:** A community of users who share looms and topology seeds.
- **Examples:** Fly fishing grove, organic chemistry grove.
- **Social features:** Sharing, rating, discussing.
- **Source:** README Part V, Architecture, Lexicon.

#### 6.3 Marketplace
- **Definition:** A place to buy, sell, and trade looms and topology seeds.
- **Incentives:** Experts earn from expertise.
- **Provenance:** Cryptographic signatures.
- **Source:** README Part V, Architecture, Lexicon.

#### 6.4 Echo
- **Definition:** A pattern that returns to you, improved by the collective.
- **Explanation:** You share a loom; others refine it; improved version comes back.
- **User story.**
- **Source:** README Part V, Lexicon.

#### 6.5 Current
- **Definition:** A flow of shared patterns in a particular domain.
- **How detected:** Temporal analysis of sharing and usage.
- **Value:** Discover what's working now.
- **Source:** README Part V, Lexicon.

#### 6.6 Tapestry
- **Definition:** The collective intelligence of the whole community.
- **Explanation:** Not stored in one place; emergent from all contributions.
- **Metaphor:** Woven from countless threads.
- **Source:** README Part V, Lexicon.

**Transition:** "When all these pieces work together, something remarkable emerges."

---

### PART SEVEN: THE FRUIT — Emergent Properties

**Purpose:** Describe the qualities users experience when the system is working well. These are feelings as much as metrics.

**Structure for each property:**
- **Definition**
- **How it manifests**
- **How it might be measured** (qualitatively or quantitatively)
- **Why it matters**

**Properties:**

#### 7.1 Emergence
- **Definition:** The whole becomes greater than the sum of its parts.
- **Manifestations:** Specialization, coordination, resilience, innovation, anticipation.
- **Ant colony analogy.**
- **Source:** README Part VI, Lexicon.

#### 7.2 Vitality
- **Definition:** A metric of how well the system is learning and optimizing.
- **Components:** Prediction accuracy, optimization rate, graph coherence, synaptic balance, user satisfaction.
- **Dashboard concept.**
- **Source:** README Part VI, Lexicon.

#### 7.3 Resonance
- **Definition:** The feeling of being understood.
- **Experience:** System suggests what you needed before you asked.
- **Source:** README Part VI, Lexicon.

#### 7.4 Coherence
- **Definition:** How well the agent graph is organized.
- **Indicators:** Strong clusters, efficient flows, few wasted connections.
- **Source:** README Part VI, Lexicon.

#### 7.5 Momentum
- **Definition:** The rate of improvement.
- **Virtuous cycle:** Each improvement enables faster future improvements.
- **Source:** README Part VI, Lexicon.

**Transition:** "Now that you understand what the system does, let's talk about what *you* do with it."

---

### PART EIGHT: THE VERBS — How You Interact

**Purpose:** Give the reader the language for action. Make it feel immediate and empowering.

**Structure for each verb:**
- **Definition**
- **When you'd use it**
- **What happens in the system**
- **User story (brief)**

**Verbs:**

#### 8.1 Log In
- Start a demonstration.
- "Watch what I'm about to do and learn from it."
- **User story:** "I logged in my morning fishing routine."

#### 8.2 Replay
- Run a learned behavior from a logline or loom.
- Adapted to current conditions.
- **User story:** "I replayed last week's successful trip."

#### 8.3 Weave
- Combine multiple looms to create new behaviors.
- Can be automatic or guided.
- **User story:** "I asked the system to weave my early morning and cloudy day looms."

#### 8.4 Dream
- (Automatic) The system improves overnight.
- You don't initiate, but you can check progress.
- **User story:** "I checked my vitality and saw 12% improvement."

#### 8.5 Cast
- Share a loom via loomcast.
- Spread proven behaviors.
- **User story:** "I'm casting my early morning bass loom to the fishing grove."

#### 8.6 Tune
- Adjust an imported loom to your context.
- Personalize shared wisdom.
- **User story:** "I tuned the pro's loom for my local lake."

**Source:** README Part VII, Lexicon.

**Transition:** "Enough abstraction. Let's walk through a day with Mycelium."

---

### PART NINE: FOR USERS — A Day in the Life

**Purpose:** Make everything concrete. Show the system in action through a narrative.

**Sections:**

#### 9.1 Morning: Waking the Swarm
- You open your laptop. The swarm wakes: vision agents watch your screen, context agents check your calendar, intent agents form hypotheses.
- The Translator UI shows a gentle pulse—your system is alive.

#### 9.2 Demonstration: Teaching a New Routine
- You're preparing for a fishing trip. You say, "Log this."
- You go through your preparation: check weather, select lures, pack gear. The system watches, capturing logs.
- You say, "Stop logging." The system begins looming the new routine.

#### 9.3 Replay: Letting the System Work
- Later, you say, "Replay my morning routine." The system executes the loom, adapted to today's conditions. It checks a different weather source because it learned you prefer that.

#### 9.4 Evening: Reviewing the Logbook
- Before bed, you open the Translator UI. You browse your logbook, seeing patterns you hadn't noticed. The system highlights a potential new loom: "I've noticed you often fish this spot after rain. Would you like to loom this?"

#### 9.5 Overnight: Dreaming
- While you sleep, the system dreams. It simulates variations of your fishing looms, keeping improvements. It prunes a rarely used connection between your weather agent and location agent.

#### 9.6 The Next Day: A Smarter Partner
- You wake to a vitality notification: +8% improvement in fishing prediction accuracy. The system suggests a new spot based on overnight dreaming.

**Source:** Synthesis of all materials. Use the fishingLOG example consistently.

**Tone:** Warm, narrative, relatable. The reader should imagine themselves in the story.

---

### PART TEN: FOR DEVELOPERS — Building on Mycelium

**Purpose:** Provide technical depth. This section is for implementers.

**Structure:** Clear headings, code snippets where appropriate, references to specifications in appendices.

#### 10.1 System Architecture Overview
- High-level diagram (described in text).
- Data flow: sensors → agents → Plinko → executors → logs → dreaming → optimization.
- **Source:** Architecture document.

#### 10.2 Core Components Deep Dive

##### 10.2.1 Agent Framework
- Creating a new agent type: subclass `Agent`, implement `process()`.
- Agent lifecycle: HIBERNATED, LOADING, ACTIVE, IDLE, DEGRADED.
- Communication via topics (SPORE protocol).
- **Source:** Architecture document, SPORE spec.

##### 10.2.2 Plinko Implementation
- Discriminators: interface, training data, updating.
- Temperature adaptation: entropy calculation, update rule.
- Gumbel noise: sampling, scaling.
- **Source:** Architecture document, mathematical formulations.

##### 10.2.3 World Model Training
- Data pipeline: logs → (obs, action, next_obs, reward).
- Architecture details: encoder (VAE), transition (GRU), reward (MLP).
- Loss functions.
- Counterfactual augmentation.
- **Source:** Architecture document.

##### 10.2.4 Dreaming Engine
- Mutation operators for each scale.
- Simulation loop.
- Validation and rollback.
- **Source:** Architecture document.

##### 10.2.5 Logbook Integration
- Vector database options (ChromaDB, LanceDB).
- Schema design.
- Query patterns (similarity search, temporal queries).
- **Source:** Architecture document.

##### 10.2.6 BES Encoder
- Training data: demonstration sequences.
- Architecture options (LSTM, transformer).
- Loss functions: reconstruction + contrastive.
- **Source:** Architecture document, research notes.

#### 10.3 APIs and Protocols

##### 10.3.1 SPORE Protocol
- Message formats (JSON, Cap'n Proto).
- Topic naming conventions.
- Discovery (announce/acknowledge/heartbeat).
- **Source:** Architecture appendix.

##### 10.3.2 Seed Formats
- Logline format (Protobuf schema).
- Topology seed format (Protobuf schema).
- **Source:** Architecture appendix.

##### 10.3.3 Federated Learning API
- Contributing patterns: `POST /patterns`.
- Receiving updates: `GET /updates`.
- **Source:** Architecture document.

#### 10.4 Extending the System

##### 10.4.1 Creating New Agent Types
- Guidelines for specialization.
- Testing new agents.

##### 10.4.2 Building Custom Discriminators
- Training data collection.
- Integration with Plinko.

##### 10.4.3 Developing Domain-Specific Loggers
- Examples: `WaterTemperatureLogger`, `CastingMotionLogger`.

##### 10.4.4 Creating Grove Applications
- Using the grove protocol.
- Building community features.

#### 10.5 Example: Building a fishingLOG

##### 10.5.1 Concept and Requirements
- What fishingLOG should do: log trips, learn patterns, suggest techniques.

##### 10.5.2 Agent Selection and Configuration
- Loggers: `GPSLogger`, `WeatherLogger`, `CatchLogger`.
- Intent agents: `PatternDetector`, `SuggestionAgent`.
- Executors: `NoteTaker`, `AlertSender`.

##### 10.5.3 Log Design
- What each log contains.
- How logs flow to logbook.

##### 10.5.4 Expected Looms and Evolution
- Early looms: simple routines (check weather, note location).
- Later looms: complex patterns (cloudy day bass fishing).
- Dreaming improvements over time.

##### 10.5.5 Deployment and Growth
- Releasing to users.
- Gathering feedback.
- Iterating.

**Source:** Architecture document, examples folder, your domain expertise.

**Tone:** Technical but not terse. Assume developer competence but explain Mycelium-specific concepts thoroughly.

---

### PART ELEVEN: FOR RESEARCHERS — Open Questions

**Purpose:** Lay out the research frontier. Invite academic contribution.

**Structure for each area:**
- **The question** (phrased as an open problem)
- **Why it matters**
- **Current approaches / literature**
- **Suggested approaches**
- **How to get started**

**Areas:**

#### 11.1 Seed Compression and Representation
- What is the optimal latent dimension for loglines?
- How does required dimension scale with sequence length and complexity?
- Can we guarantee that a logline contains sufficient information for task completion?
- How to measure information loss in compression?

#### 11.2 Dreaming Effectiveness
- How well do improvements from dreaming transfer to real-world performance?
- What mutation operators are most effective at different scales?
- How many dreaming iterations are optimal per skill per night?
- Can we predict which looms will benefit most from dreaming?

#### 11.3 Emergent Coordination
- How can we measure emergence in multi-agent systems?
- What is the relationship between log graph structure and task performance?
- Can we guide emergence toward beneficial outcomes through prompt engineering?
- What prevents harmful emergence (e.g., agents colluding against user interests)?

#### 11.4 Privacy and Security
- How much information about the original user can be extracted from a logline?
- Can differential privacy protect loglines without destroying utility?
- What differential privacy budget (ε) is feasible for seed sharing?
- How to design a secure, decentralized marketplace for looms?

#### 11.5 Human-AI Interaction
- What mental models do users form of continuously learning systems?
- How to calibrate user trust appropriately (neither over-trust nor under-trust)?
- What explanation interfaces are most effective for dynamic agent webs?
- How to design for appropriate user feedback without causing fatigue?

#### 11.6 How to Contribute to Research
- Join our Discord research channel.
- Access our research datasets (coming soon).
- Collaborate on papers.
- Propose new questions.

**Source:** Architecture document section 10, earlier research discussions, white papers.

**Tone:** Inviting, rigorous. These are opportunities, not deficiencies.

---

### PART TWELVE: THE PATH FORWARD — Roadmap and Invitation

**Purpose:** Show where we're going and how to join.

**Sections:**

#### 12.1 Current Status
- What's implemented: prototype core, agent framework, basic Plinko, local logging.
- What's in progress: world model training, dreaming engine, BES.
- What's planned: federated learning, groves, marketplace.

#### 12.2 Roadmap Phases

##### 12.2.1 Phase 1: Core Runtime (0–6 months)
- Goals: stable agent framework, Plinko with basic discriminators, logbook with vector search.
- Deliverables: alpha release, developer documentation.

##### 12.2.2 Phase 2: Learning and Optimization (6–12 months)
- Goals: world model training, multi-scale dreaming, BES integration.
- Deliverables: beta release, example applications (fishingLOG prototype).

##### 12.2.3 Phase 3: Collective Intelligence (12–18 months)
- Goals: federated learning, grove protocol, marketplace infrastructure.
- Deliverables: 1.0 release, multiple domain applications.

##### 12.2.4 Phase 4: Ecosystem (18+ months)
- Goals: hardware acceleration, robotic integration, independent application ecosystem.
- Deliverables: thriving community, ongoing research.

#### 12.3 How to Contribute

##### 12.3.1 For Developers
- Pick an issue tagged `good first issue`.
- Build a new agent type.
- Improve documentation.
- Write examples.

##### 12.3.2 For Researchers
- Tackle an open question.
- Run experiments.
- Publish papers.
- Collaborate with the team.

##### 12.3.3 For Designers
- Design Translator UI components.
- Create visualizations for log graph.
- Design grove and marketplace interfaces.

##### 12.3.4 For Writers
- Improve documentation.
- Write tutorials.
- Create case studies.
- Help refine the language.

##### 12.3.5 For Users
- Use early releases.
- Provide feedback.
- Share looms.
- Join groves.

#### 12.4 Join the Community
- Discord link.
- GitHub link.
- Contribution guidelines link.
- Code of conduct.

#### 12.5 Closing Words: Come Grow With Us
- Revisit the garden metaphor.
- Reiterate that the system is not finished—it's being cultivated.
- The most important thing a growing thing needs is people who tend it.
- Final invitation.

**Source:** Architecture document section 9, README invitation.

**Tone:** Open, welcoming, urgent in its invitation.

---

## APPENDICES

### A. Quick Reference Glossary

**Format:** Alphabetical list, term + one-line definition, page reference.

**Source:** Lexicon quick reference, expanded with all terms.

### B. Technical Specifications

#### B.1 Logline Format (Protobuf)
```protobuf
message Logline {
    string id = 1;
    bytes embedding = 2;
    int32 embedding_dim = 3;
    repeated string agent_types = 4;
    map<string, string> base_model_hashes = 5;
    uint64 created_at = 6;
    uint32 usage_count = 7;
    float avg_success_rate = 8;
    bytes signature = 9;
}
```

#### B.2 Topology Seed Format (Protobuf)
```protobuf
message TopologySeed {
    string id = 1;
    repeated string agent_ids = 2;
    repeated Edge edges = 3;
    message Edge {
        uint32 from = 1;
        uint32 to = 2;
        float weight = 3;
    }
    string context_signature = 4;
    float success_rate = 5;
    uint64 created_at = 6;
}
```

#### B.3 SPORE Protocol Specification
- Message structure: `{protocol, sender, recipient, message_id, content, metadata}`
- Topic naming: `/domain/type/name` (e.g., `/sensors/camera/frame`)
- Discovery: `ANNOUNCE`, `ACKNOWLEDGE`, `HEARTBEAT`

#### B.4 API Endpoints
- `POST /seeds/export`
- `POST /seeds/import`
- `POST /patterns/contribute`
- `GET /patterns/updates`

**Source:** Architecture document technical appendix.

### C. References and Further Reading

- Academic papers (with citations and links)
- Related projects (with brief descriptions)
- Further reading on key concepts (emergence, federated learning, world models)

**Source:** White paper references, research agenda.

### D. How to Contribute (Detailed)

- Development setup instructions.
- Pull request process.
- Code style guide.
- Testing requirements.
- Documentation standards.

**Source:** CONTRIBUTING.md (to be created).

### E. Document Version History

- Version 1.0: Initial release (March 2026)
- Track major changes.

---

## Epilogue: The Garden Grows

**Purpose:** A final, poetic closing that circles back to the opening.

**Content:**
- Revisit the image of the forest.
- Remind the reader that they are now a gardener.
- The garden is waiting. The seeds are here. The soil is ready.
- End with the same line as the prologue, transformed by all that has been learned: "Let's begin."

**Source:** Synthesis of opening and closing themes.

---

## Final Instructions to Kimi

1. **Synthesize, don't copy-paste.** Use the source material as raw ingredients, but cook them into something new. The final document should read as one voice, not a patchwork.

2. **Maintain the tone throughout:** Grounded but visionary, clear but evocative, technical but accessible. You are a gardener showing someone their first forest.

3. **Use examples consistently.** The fishingLOG example should appear throughout, building familiarity. Use it to illustrate new concepts as they're introduced.

4. **Cross-reference liberally.** When a term introduced earlier appears, remind the reader where it was defined. The document is long; help readers navigate.

5. **End each major section with a brief transition.** "Now that we understand X, let's look at Y." This maintains flow.

6. **Include diagrams where helpful.** Describe them in text for now; they can be generated later. For example, a data flow diagram for Part Four, a log graph visualization for Part Five.

7. **Check for consistency.** Ensure all terms are used consistently throughout. The lexicon (Appendix A) should be the source of truth.

8. **Proofread for tone.** No hype, no overstatement. Let the ideas speak for themselves. The vision is compelling enough without embellishment.

9. **Length is not a constraint.** This document should be long. It should feel substantial. A reader should feel they've truly learned something by the end.

10. **Remember the reader.** They came here curious. Leave them inspired, informed, and ready to act.

The final document should be something you'd print and bind—a manifesto, a specification, a user guide, and an invitation, all in one.

Begin.
