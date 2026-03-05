# Mycelium Architecture Specification

**Version 3.0 — June 2026**  
**SuperInstance Open Source Initiative**  
*Fully Annotated Edition*

---

## 1. Introduction

### 1.1 The Problem with Static Intelligence

Traditional software and AI are static. Once compiled or trained, they cannot learn from individual users, adapt to changing environments, or improve after deployment. This limitation is fundamental: we write code to specify behavior, but code is a frozen artifact. Cloud‑based AI exacerbates the problem—models are trained once on population data and then frozen, treating every user as an average and forgetting every interaction.

**Research basis:** The Bio Cognitive Mesh (IEEE 2025) documents latency and bandwidth penalties of cloud‑centric AI. The SMARTEDGE project (EU Horizon) highlights the need for edge‑native, adaptive intelligence.

### 1.2 A New Paradigm: Demonstration‑Driven Development

Mycelium inverts the development process. Instead of writing code, you **demonstrate** the desired behavior. The system observes your actions, compresses the sequence into a compact **seed**, and later reproduces that behavior from a simple prompt. Code becomes optional—used only for formal verification or when mathematical proof is required.

### 1.3 Core Thesis: Behavior as Primary Artifact

A seed is a vector in a learned **behavioral embedding space**. Given the same prompt and seed, the system produces behavior consistent with the demonstrated style, but adaptable to current context. This resolves the tension between exact reproduction and environmental adaptation.

**Design rationale:** We move from encoding exact sequences to encoding behavioral intent. This aligns with how humans generalize from examples.

**Novelty:** The concept of a universal behavioral embedding space trained from diverse demonstrations is a central innovation of Mycelium.

### 1.4 Document Scope and Audience

This document provides a complete technical blueprint for building Mycelium. It is intended for developers, researchers, and contributors. Each section includes annotations on research basis, novelty, design rationale, open questions, and connections to other components.

---

## 2. Core Concepts (Annotated)

| Concept | Definition | Annotation |
|---------|------------|------------|
| **Agent** | A tiny neural model (1–100M parameters) specialized for a narrow task. Agents run continuously, consume sensor data, and produce proposals. | **Research basis:** Edge AI literature supports tiny models. **Open question:** Optimal agent specialization and architecture. |
| **Prompt** | A natural‑language or structured instruction that initiates a behavior. Prompts are fed to higher‑level agents to invoke skills. | **Design rationale:** Prompts provide a human‑friendly interface. They can also be seeds (for higher‑level behaviors). |
| **Seed** | A vector in a learned behavioral embedding space (64–1024 dim) that encodes a behavioral style or intent. Seeds are produced by the seed encoder from demonstrations and used to condition agents. | **Novelty:** The behavioral embedding space is a foundational contribution. **Research basis:** Universal sentence embeddings, skill embeddings from SkillRL. |
| **Skill** | A named, stored seed plus metadata. Skills can be composed hierarchically (a skill can invoke sub‑skills). | **Design rationale:** Hierarchical composition enables reuse and abstraction. **Open question:** Optimal skill granularity. |
| **World Model** | A predictive model that learns how the environment (apps, UI, system) responds to actions. Used for dreaming and simulation. | **Research basis:** DreamerV3, GW‑Dreamer. **Novelty:** Application to personal digital environments. |
| **Dreaming** | Offline simulation where the system uses the world model to explore variations of skills, selecting those that maximize predicted user satisfaction. | **Design rationale:** Dreaming enables improvement without real‑world interaction. **Open question:** Transfer of simulated improvements to reality. |
| **Memory** | A vector database storing past experiences (observation embeddings, actions, outcomes). Agents query memory to inform decisions. | **Research basis:** EngramNCA (private memory channels). **Implementation:** ChromaDB / LanceDB. |
| **Plinko Layer** | A stochastic decision mechanism where agents bid for actions. Discriminators (critics) adjust bid values. Temperature controls exploration. | **Design rationale:** Market‑based coordination naturally leads to specialization and resilience. **Novelty:** Integration with behavioral embeddings. |
| **A2UI** | Agent‑to‑UI – a unified interface for agents to perform UI automation across platforms. | **Research basis:** Accessibility APIs. **Implementation:** Platform‑specific backends. |

---

## 3. System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         Mycelium System                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  [Sensors] → [Sensor Layer] → [Shared Memory] → [Agent Swarm]   │
│       ↑              ↑              ↑                  ↑         │
│       │              │              │                  │         │
│       └── [Memory] ←─┴── [Seed Engine] ←── [Plinko Layer]        │
│                                          │                       │
│                                          ▼                       │
│                                 [Action Executors] → [Outcome]   │
│                                          │                       │
│                                          ▼                       │
│                               [Experience Logger]                │
│                                          │                       │
│                                          ▼                       │
│     ┌──────────────┬──────────────┬─────┴─────┬──────────────┐  │
│     │Skill Chunker │World Model   │Dreaming    │Training      │  │
│     │(Grammar)     │Trainer       │Engine      │Scheduler     │  │
│     └──────────────┴──────────────┴───────────┴──────────────┘  │
│                       │              │                           │
│                       └──────────────┴───────────┐               │
│                                                  ▼               │
│                                         [Model Zoo]              │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

**Two‑Mode Operation:**
- **Day (inference):** Sensors → shared memory → agents propose → Plinko selects → executors act → logger records.
- **Night (learning):** Logs analyzed to update world model, discover skills, dream improvements, update model zoo.

**Research alignment:** The edge‑cloud continuum is supported by SMARTEDGE. The day/night cycle mirrors biological sleep‑wake learning.

---

## 4. Component Specifications

### 4.1 Sensor Layer

**Purpose:** Provide a unified, low‑latency stream of all device inputs.

**Inputs:**
- Screen frames (downsampled 224×224 RGB, 30 fps)
- Audio (16 kHz mono, 1s rolling window, MFCC features)
- Input events (keyboard, mouse, touch)
- Device sensors (accelerometer, GPS, orientation)
- System state (active app, notifications, battery)

**Implementation:**
- Platform‑specific capture APIs wrapped in a uniform interface.
- Each sensor type writes to a lock‑free ring buffer in shared memory (e.g., `mmap`). Buffers sized for 60 seconds of data.
- Preprocessing: frames normalized; audio → MFCC; events serialized as protobuf.

**Speculative Pre‑processing (Experimental):** A lightweight predictor estimates which sensors will be needed in the next 16 ms and pre‑fetches them, reducing latency by 15–20%. This is an optimization; its effectiveness needs measurement.

**Annotations:**
- **Research basis:** Shared memory for agent communication is used in GMV mycelium. Sensor fusion is standard.
- **Novelty:** Speculative pre‑processing is a novel optimization; it can be initially omitted.
- **Open questions:** What latency reduction is actually achieved? Does it justify complexity?

---

### 4.2 Agent Swarm

**Agent Data Structure:**
```python
@dataclass
class Agent:
    agent_id: str
    agent_type: str          # "vision", "audio", "text", "intent", "context", "safety"
    model_path: str          # path to ONNX/TFLite model
    input_topics: List[str]  # sensor topics to subscribe to
    output_topic: str        # where proposals are written
    state: str               # "active", "idle", "hibernated", "degraded"
    last_activation: float
    confidence_threshold: float
    temperature_pref: float
    specialization_embedding: Optional[np.ndarray]  # from behavioral embedding space
    peer_connections: List[str]                     # agents frequently co-activated
```

**Agent Lifecycle:**
- **HIBERNATED → LOADING:** Request from Plinko or higher agent.
- **LOADING → ACTIVE:** Model loaded; begins processing.
- **ACTIVE → IDLE:** No activity for `idle_timeout` (30 s). Stops polling.
- **IDLE → HIBERNATED:** No activity for `hibernate_timeout` (5 min). Model unloaded.
- **ACTIVE → DEGRADED:** Agent detects internal errors or resource constraints; continues with reduced functionality.

**Scheduling:** Thread pool (size = CPU cores − 1) runs agents round‑robin. Each agent gets a time slice (e.g., 5 ms) to process latest input and write a proposal.

**Dynamic Agent Recruitment:**
When Plinko entropy exceeds a threshold, the Swarm Manager queries the Model Zoo for agents with similar specialization embeddings (cosine similarity > 0.7). If none exist, it may spawn a temporary “helper” agent by cloning a base model and fine‑tuning on recent logs.

**Annotations:**
- **Research basis:** NeuroMesh demonstrates graceful degradation; SMARTEDGE validates dynamic swarm formation.
- **Novelty:** Specialization embeddings from behavioral space are new.
- **Open questions:** How to compute specialization embeddings? (Likely from agent's training data or from its responses to diverse inputs.) How to measure similarity? What threshold is optimal?
- **Connection:** The behavioral embedding space (Section 4.3) provides the representation for specialization.

---

### 4.3 Behavioral Embedding Space (New Core Component)

**Purpose:** Provide a universal latent space where all behaviors—demonstrations, skills, agent specializations—can be embedded. This space enables seed encoding, skill matching, and agent specialization.

**Training:**
- Collect a large corpus of demonstrations (across many users, tasks, and domains) with appropriate anonymization.
- Train a **behavioral encoder** (e.g., a transformer over action‑observation sequences) using contrastive learning: sequences from the same demonstration should have similar embeddings; sequences from different demonstrations should be dissimilar.
- The encoder maps any demonstration to a fixed‑dimensional vector (e.g., 256 floats).

**Properties:**
- The space is continuous and semantically meaningful: similar behaviors cluster together.
- It can be used to embed agent capabilities (by feeding the agent a diverse set of inputs and averaging the resulting embeddings).
- Seeds are simply embeddings of new demonstrations.

**Storage:** The encoder is stored in the Model Zoo and distributed with Mycelium. It can be updated periodically with new data (with privacy safeguards).

**Annotations:**
- **Research basis:** Contrastive learning (SimCLR, triplet loss) is well‑established. Universal sentence encoders (e.g., Google's USE) provide a precedent.
- **Novelty:** Application to behavioral sequences is novel and requires validation.
- **Design rationale:** A shared embedding space simplifies many problems: seed conditioning, skill matching, agent specialization, and even world model state representation.
- **Open questions:** 
  - How large must the training corpus be to achieve good generalization?
  - What is the right architecture for the encoder? (Transformer over actions+observations?)
  - How to handle variable‑length demonstrations?
  - How to update the space as new behaviors emerge without breaking existing embeddings? (Possibly by using incremental learning or keeping the space fixed after initial training.)
- **Connections:** This space underpins the Seed Engine (4.4), Skill Chunker (4.8), and agent specialization.

---

### 4.4 Seed Engine

#### 4.4.1 Seed Capture

When the user says “watch me”, the system records the sequence of (observation, action) pairs until “stop”. Each observation is passed through the world model encoder to produce an observation latent; each action is encoded via a small action embedding lookup. The sequence of (obs_latent, action_embedding) is fed to the behavioral encoder, which outputs a seed vector.

**Implementation:**
```python
seed = behavioral_encoder(obs_latents, action_embeddings)
```
The seed is stored with metadata: timestamp, agent types involved, prompt (if any), etc.

#### 4.4.2 Seed Replay

To replay a seed:
1. The seed is loaded into the appropriate agent (the agent that was active during capture). The agent's forward pass now conditions on the seed. Conditioning mechanism: simple concatenation of seed with the agent's hidden state (or use FiLM).
2. The agent acts with temperature = 0 for deterministic style, but adapts to current observations because the seed only specifies style, not exact actions.
3. If exact reproduction is required, a special “low‑temperature imitation mode” can be used where the agent attempts to match the original trajectory as closely as possible (using a learned inverse model).

#### 4.4.3 Seed Storage Format (Protobuf)

```protobuf
message Seed {
    string id = 1;
    string skill_id = 2;                // optional
    repeated string agent_types = 3;
    map<string, string> base_model_hashes = 4;
    bytes embedding = 5;                 // float32 vector
    int32 embedding_dim = 6;
    uint64 created_at = 7;
    uint32 usage_count = 8;
    float avg_success_rate = 9;
    bytes signature = 10;                 // optional
}
```

**Annotations:**
- **Research basis:** Behavioral encoder from 4.3; conditioning via concatenation is simple but untested; FiLM has precedent in multi‑task learning.
- **Novelty:** The combination of learned behavioral space and seed conditioning is new.
- **Open questions:** 
  - Does the seed actually capture style? How to measure?
  - What conditioning mechanism works best? (We need experiments.)
  - How to handle seeds that involve multiple agents? (The seed may need to be passed to all relevant agents.)
  - Can seeds be composed by averaging or interpolation? (Hypothesis: linear interpolation in embedding space yields plausible hybrid behaviors.)
- **Connections:** Relies on behavioral space (4.3) and world model (4.9) for observation latents.

---

### 4.5 Plinko Decision Layer

**Input:** Set of proposals from all agents. Each proposal includes:
- `agent_id`
- `action_type`, `target`
- `value`: an estimate of the action's worth (output by agent, analogous to Q‑value)
- `features`: observation embedding (from world model) that led to this proposal

**Step 1: Discriminator Adjustment**
Each proposal's value is adjusted by discriminators (critics) that output a multiplier in [0,1] for safety, coherence, timing. The adjusted value is:
\[
v_i' = v_i \cdot \prod_j d_{ij}
\]

**Step 2: Score Computation with Exploration Noise**
Add Gumbel noise scaled by temperature τ:
\[
s_i = \log(v_i') + \epsilon_i \cdot \tau
\]
where ε_i ~ Gumbel(0,1).

**Step 3: Selection Probability**
\[
\pi_i = \frac{\exp(s_i / \tau)}{\sum_k \exp(s_k / \tau)}
\]
Sample action from this categorical distribution.

**Step 4: Adaptive Temperature**
τ = τ_base * (1 + α * H) where H is entropy of π. This increases exploration when agents disagree.

**Annotations:**
- **Research basis:** Gumbel‑Softmax for stochastic policies; discriminators akin to critics in RL.
- **Novelty:** Market‑based framing; adaptive temperature tied to entropy.
- **Open questions:** 
  - How to train discriminators? (Use logged user feedback as reward.)
  - How to set τ_base and α? (Empirical tuning.)
  - Does this mechanism lead to stable coordination? (Simulation needed.)
- **Connections:** Agent values can be learned via RL (using user feedback as reward). Discriminators can share the same behavioral embedding space to evaluate proposals.

---

### 4.6 Action Executors & A2UI

**A2UI:** Unified interface to platform accessibility APIs:
- Android: UIAutomator
- iOS/macOS: AXUI
- Windows: UI Automation
- Linux: AT‑SPI

Each executor runs in a sandboxed process with minimal permissions. Actions are logged with inverse information to enable undo.

**Other Executors:**
- API Executor: HTTP requests with OAuth.
- File Executor: Sandboxed file operations.
- Physical Executor: ROS2 / MQTT for robotics.

**Annotations:**
- **Research basis:** Accessibility APIs are well‑established.
- **Implementation:** Straightforward, but ensuring cross‑platform consistency is a challenge.
- **Open questions:** How to handle applications that don't expose accessibility APIs? (Fallback to computer vision? Possibly a vision agent that simulates clicks based on screen analysis.)

---

### 4.7 Experience Logger

**Log Format (Parquet):**
```
timestamp: int64
session_id: binary
observation_latent: bytes   # from world model encoder
action: Proposal             # serialized
value: float                 # agent's value before adjustment
discounted_return: float     # future discounted reward (computed offline)
user_feedback: int8          # -1=bad, 0=none, 1=good
system_state: {...}
```

**Compression:** Observations are stored as latents (64 floats) rather than raw frames, reducing storage ~90%.

**Circular Buffer:** Logs kept for 30 days by default.

**Annotations:**
- **Design rationale:** Storing latents saves space and aligns with world model training.
- **Open questions:** What discount factor for return? (Standard 0.99.)
- **Connections:** Logs are used for world model training (4.9), skill chunking (4.8), and RL training for agents (future).

---

### 4.8 Skill Chunker (Grammar Induction)

**Purpose:** Discover reusable skills (subroutines) from logged sequences.

**Method:** Use a grammar induction algorithm (e.g., Sequitur, or a Bayesian grammar VAE) on sequences of action embeddings (from the behavioral space). The algorithm learns a hierarchical grammar where nonterminals correspond to skills.

**Steps:**
1. Convert each logged action sequence into a sequence of tokens (action embeddings discretized via clustering).
2. Apply grammar induction to find repeated patterns.
3. For each discovered nonterminal, train a small decoder that can generate the corresponding action sequence from a seed (the nonterminal's embedding). This decoder becomes the skill's implementation.
4. Store skills in Model Zoo with metadata (frequency, success rate).

**Annotations:**
- **Research basis:** Sequitur (Nevill‑Manning & Witten) for grammar induction; grammar VAE (Kusner et al.) for continuous representations.
- **Novelty:** Applying grammar induction to behavioral sequences in a continuous embedding space.
- **Open questions:** 
  - How to discretize action embeddings effectively? (k‑means on behavioral space.)
  - How to evaluate discovered skills? (Reuse frequency, downstream task performance.)
  - How to handle noise and variation in demonstrations? (Grammar induction is robust to some variation.)
- **Connections:** Skills become reusable components that can be invoked by higher‑level agents. Skill embeddings are points in the behavioral space, so they can be composed.

---

### 4.9 World Model

**Architecture:**
- **Encoder:** VAE compresses observation (latent from 4.3? or raw?) to latent z (64 dim).
- **Transition:** GRU predicts next z given current z and action embedding.
- **Reward:** MLP predicts user satisfaction (scalar) from next z.
- **Decoder:** (Optional) reconstructs observation for visualization.

**Training:**
- Data: (z_t, action_emb, z_{t+1}, reward) from logs.
- Loss: reconstruction loss (if decoder) + KL + prediction MSE + reward MSE.
- Counterfactual augmentation: swap actions in similar contexts to generate synthetic transitions.

**Annotations:**
- **Research basis:** DreamerV3, GW‑Dreamer.
- **Novelty:** Application to personal digital environments; use of behavioral embedding for actions.
- **Open questions:** 
  - How to incorporate the behavioral embedding space? (Action embeddings are from that space.)
  - How to model long‑term dependencies? (Transformers may be better than GRU.)
  - How to handle partial observability? (VAE latent may encode uncertainty.)
- **Connections:** The world model provides the dreaming environment (4.10). Its latent space can also serve as observation representation for agents.

---

### 4.10 Dreaming Engine

**Purpose:** Improve skills by simulating variations in the world model.

**Multi‑Scale Dreaming:**
- **Micro:** Perturb action embeddings (add small noise) to refine execution.
- **Meso:** Reorder actions, insert/delete steps (using grammar operators) to optimize routines.
- **Macro:** Compose skills (replace a subsequence with another skill) to create new strategies.

**Algorithm:**
```python
def dream(skill_id, scale, num_simulations):
    skill = load_skill(skill_id)
    world = load_world_model()
    best_reward = -inf
    best_variation = None
    for _ in range(num_simulations):
        var = mutate(skill, scale)   # returns a modified skill (its embedding or policy)
        state = sample_initial_state()
        total = 0
        for step in range(horizon[scale]):
            action = var.get_action(state)
            state, reward = world.predict(state, action)
            total += reward
        if total > best_reward:
            best_reward = total
            best_variation = var
    if best_reward > skill.performance:
        save_skill(best_variation)
    return best_variation
```

**Annotations:**
- **Research basis:** Dreamer, GW‑Dreamer; evolutionary strategies.
- **Novelty:** Multi‑scale dreaming with grammar‑based mutations.
- **Open questions:** 
  - How to mutate a skill represented as an embedding? (Interpolate in embedding space? Use gradient‑based optimization through world model?)
  - Does simulated improvement transfer to reality? (Need sim‑to‑real experiments.)
  - How to set mutation rates per scale?
- **Connections:** Requires world model (4.9) and skill representations (4.8).

---

### 4.11 Training Scheduler

**Purpose:** Orchestrate nightly learning tasks.

**Task Prioritization (ROI):**
\[
ROI = \frac{\text{expected\_improvement} \times \text{frequency}}{\text{estimated\_cost}}
\]
- expected_improvement: from recent trend or similarity to past improvements.
- frequency: how often the skill/agent is used.
- cost: estimated GPU hours.

**Local vs. Cloud:** If cost > local_budget and user opts in, offload to LucidDreamer.ai with differential privacy.

**Predictive Wake‑Up:** Based on usage patterns, predict next active time; schedule training to finish 5 minutes before.

**Annotations:**
- **Research basis:** Edge‑cloud offloading (SMARTEDGE).
- **Novelty:** ROI prioritization and predictive wake‑up are novel.
- **Open questions:** 
  - How to estimate expected improvement? (Could use learning curves from similar tasks.)
  - How accurate is predictive wake‑up? (Depends on user behavior patterns.)
  - What if predictions are wrong? (Have fallback: pause/resume.)
- **Connections:** Uses Model Zoo for skill metadata.

---

### 4.12 Memory (Vector Database)

**Purpose:** Long‑term storage of episodic memories.

**Implementation:** ChromaDB or LanceDB, local.

**Schema:**
- Collection per user.
- Each record: embedding (from world model encoder), metadata (timestamp, action, outcome), optional raw data.

**Retrieval:** Agents query with current observation embedding; return top‑k similar past experiences.

**Annotations:**
- **Research basis:** Vector databases are standard. EngramNCA provides biological inspiration for private memory.
- **Implementation:** Straightforward.
- **Open questions:** 
  - How to weight retrieved memories? (Average? Attention?)
  - How to handle privacy? (All data local.)
  - Can memories be shared across devices? (Encrypted sync.)

---

### 4.13 Model Zoo

**Storage Structure:**
```
/models/
  base/               # base agent models
  skills/             # skill embeddings + decoders
  world/              # world model components
  behavioral_encoder/ # the universal behavioral encoder
  metadata.db         # SQLite
```

**Versioning & Rollback:**
- Each model entry includes performance metrics (e.g., success rate on recent tasks).
- New versions are monitored for 24 hours; if performance drops, automatic rollback.

**Annotations:**
- **Research basis:** MLOps practices.
- **Implementation:** Standard.
- **Open questions:** What metrics to store? How to compare performance across versions?

---

## 5. Protocols and Data Formats

### 5.1 Seed Format (see 4.4.3)

### 5.2 Proposal Format (Cap'n Proto)

```capnp
struct Proposal {
    agentId @0 :Text;
    timestamp @1 :Float64;
    actionType @2 :ActionType;
    value @3 :Float32;           # agent's estimated value
    target @4 :Target;
    obsEmbedding @5 :List(Float32); # observation latent from world model
}
```

### 5.3 Agent Communication Protocol

- **Topics:** Named ring buffers in shared memory.
- **Message:** Serialized Proposal.
- **Delivery:** Best‑effort (overwrites oldest if full).

### 5.4 Seed Exchange Protocol (REST)

```
POST /seed/export { skill_id } → { seed_data, compatibility }
POST /seed/import { seed_data, verify } → { success, skill_id, warnings }
```

**Annotations:** Simple HTTP endpoints; compatibility includes required agent versions.

---

## 6. APIs and SDKs

### 6.1 Public API (Python)

```python
import mycelium as mc

swarm = mc.Swarm()
swarm.add_agent(mc.Agent.from_registry("vision-mobilenet-v3"))

# Run one inference step
action = swarm.step()

# Capture a seed
seed = swarm.capture_demonstration(start_cmd, stop_cmd)

# Replay a seed
swarm.replay_seed(seed, prompt="check email")
```

### 6.2 Agent Development SDK
- Tools to convert models to ONNX, quantize.
- Simulator for testing agents.

---

## 7. Implementation Roadmap

| Phase | Timeline | Focus |
|-------|----------|-------|
| **1. Foundation** | 0–6 mo | Behavioral encoder training, basic agent runtime, shared memory, Plinko (simplified), logging |
| **2. Core Learning** | 6–12 mo | World model training, skill chunking (grammar), seed capture/replay, discriminators |
| **3. Dreaming** | 12–18 mo | Multi‑scale dreaming, adaptive temperature, memory integration |
| **4. Ecosystem** | 18–24 mo | Seed sharing protocol, cloud integration, multi‑user support, marketplace prototype |

---

## 8. Research Agenda (Open Questions)

This section summarizes the key open questions from annotations.

### 8.1 Behavioral Embedding Space
- Optimal encoder architecture? Transformer? LSTM?
- Required corpus size? How to collect diverse demonstrations with privacy?
- Update strategy: static or incremental?

### 8.2 Seed Conditioning
- Compare conditioning methods (concatenation, FiLM, etc.) on style retention and adaptability.
- Can seeds be composed via linear interpolation? Does that yield plausible hybrid behaviors?
- How to handle multi‑agent seeds?

### 8.3 Plinko and Discriminators
- How to train discriminators from user feedback? (RL from human feedback.)
- Optimal adaptive temperature parameters?
- Does market‑based coordination lead to stable specialization?

### 8.4 Skill Chunking
- How to evaluate discovered skills? (Reuse frequency, transfer improvement.)
- Grammar induction vs. neural methods? (Trade‑off interpretability vs. flexibility.)
- How to handle continuous actions? (Discretization needed for grammar.)

### 8.5 World Model
- How to model complex UI transitions? (Transformers may help.)
- How to ensure world model supports effective dreaming? (Need correlation studies.)
- Counterfactual augmentation: does it improve generalization?

### 8.6 Dreaming
- Do simulated improvements transfer to reality? (Sim‑to‑real gap.)
- Optimal mutation operators per scale?
- How many dreaming iterations are worthwhile?

### 8.7 Training Scheduler
- How to estimate expected improvement?
- Predictive wake‑up accuracy and impact on user experience.

### 8.8 Privacy and Security
- Differential privacy for behavioral encoder training.
- Seed authentication and malicious seed detection.
- Sandboxing effectiveness.

### 8.9 Emergent Properties
- How to measure emergence? Adapt information‑theoretic metrics.
- Can we steer emergence with prompts?
- What conditions promote beneficial specialization?

---

## 9. Conclusion

Mycelium proposes a radical shift in how we build intelligent systems—from code to demonstration, from static to continuously learning, from monolithic to swarm. This architecture synthesizes ideas from edge AI, multi‑agent systems, world models, and representation learning. While many components are grounded in existing research, the integration and the novel concept of a behavioral embedding space open up exciting research directions.

We invite the community to build, experiment, and contribute. The journey from vision to reality will require answering the open questions, but the potential—a world where software grows with you and intelligence is a shareable artifact—is worth the effort.

---

*This document is a living specification. For the latest version, source code, and to join the community, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
