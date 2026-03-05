# Mycelium Architecture Specification

**Version 3.0 — May 2026**  
**SuperInstance Open Source Initiative**  
*Authors: The Mycelium Community*

---

## 0. Executive Summary

Mycelium is an open‑source platform for building **living agent systems**—software that learns from demonstration, compresses behaviors into reusable **seeds**, and executes them deterministically across a swarm of tiny neural models. This document provides a complete, implementable architecture for Mycelium, intended for engineers, researchers, and contributors.

The architecture synthesizes insights from edge AI, multi‑agent systems, world model‑based reinforcement learning, skill discovery, and information theory. It introduces novel concepts—**behavioral embedding spaces**, **market‑based Plinko decision layer**, **grammar‑induced skill chunking**, and **multi‑scale dreaming**—while grounding them in established research and intuitive principles.

Key innovations:
- **Universal Behavioral Embedding Space**: All behaviors are mapped to a shared latent space, enabling seed compression, transfer, and privacy.
- **Market‑Based Plinko**: Agents bid for actions; discriminators act as regulators; temperature controls exploration.
- **Grammar Induction for Skills**: Skills are learned as productions in a stochastic action grammar, enabling hierarchical reuse.
- **Differentiable World Model**: A neural simulator that enables dreaming and policy improvement.

This document is a living specification. Open research questions are explicitly noted, and the community is invited to contribute.

---

## 1. Introduction

### 1.1 The Problem with Static Intelligence

Traditional software and AI models are static. Once deployed, they cannot learn from individual users, adapt to changing environments, or improve over time. They remain tools we operate, not partners we embody. This limitation is fundamental to the current development paradigm: we write code to specify behavior, compile it, and ship it. Any change requires a new release.

Cloud‑based AI exacerbates the problem. Models are trained once on population data and then frozen. They treat every user as an average, forget everything after each interaction, and require constant connectivity. For real‑time, personal, and private applications, this approach is untenable.

### 1.2 A New Paradigm: Demonstration‑Driven Development

Mycelium inverts the development process. Instead of writing code, you **demonstrate** the desired behavior. The system observes the sequence of actions and decisions, compresses it into a compact **seed**, and later reproduces that exact behavior from a simple prompt. Code becomes optional—used only when mathematical proof or formal verification is required.

This paradigm shift has profound implications:
- **Faster prototyping:** Go from idea to working behavior in minutes.
- **Personalization:** The system learns your unique style, not a population average.
- **Shareability:** Seeds can be exchanged like files, enabling skill transfer without data exposure.
- **Continuous improvement:** Nightly dreaming and learning cycles refine behaviors automatically.

### 1.3 Core Thesis: Behavior as Primary Artifact

In Mycelium, behavior is the source of truth. A seed is a compact vector (typically 64–1024 floats) that identifies a region in a learned **behavioral embedding space**. Given the same seed and prompt, the system will produce behavior consistent with that region—adaptable to context yet stylistically faithful.

This thesis rests on two claims:
1. **Behavioral Embedding Space:** A low‑dimensional space can capture the essential structure of diverse behaviors.
2. **Seed‑Conditioned Agents:** Agents can be trained to condition their actions on a seed, producing behaviors that match the corresponding region.

Both claims are supported by recent advances in representation learning and multi‑task training.

### 1.4 Document Scope and Audience

This document is a technical blueprint for building Mycelium. It describes every component in sufficient detail to be implemented from scratch, including data structures, algorithms, and interfaces. It also identifies open research questions and outlines a roadmap for validation.

The intended audience includes:
- Developers who want to build applications on Mycelium.
- Researchers interested in multi‑agent systems, continual learning, and human‑AI interaction.
- Contributors to the open‑source project.

---

## 2. Core Concepts

| Concept | Definition |
|---------|------------|
| **Agent** | A tiny neural model (1–100M parameters) specialized for a narrow task. Agents run continuously, consume sensor data, and produce proposals. |
| **Prompt** | A natural‑language or structured instruction that initiates a behavior. Prompts are fed to higher‑level agents to invoke skills. |
| **Seed** | A compact vector (64–1024 floats) that identifies a region in the behavioral embedding space. A seed, together with a prompt, yields behavior consistent with that region. |
| **Behavioral Embedding Space** | A learned latent space where similar behaviors cluster. Trained on a large corpus of demonstrations. |
| **Skill** | A named, reusable seed, possibly with metadata (e.g., required agent types). |
| **World Model** | A predictive model that learns how the environment responds to actions. Used for dreaming and simulation. |
| **Dreaming** | Offline simulation where the system uses the world model to explore variations of skills, selecting those that maximize predicted reward. |
| **Memory** | A vector database where agents store and retrieve past experiences to inform future decisions. |
| **Plinko Layer** | A market‑based decision mechanism: agents bid with value estimates; discriminators adjust bids; Gumbel noise adds exploration; temperature adapts to uncertainty. |
| **A2UI** | Agent‑to‑UI – a unified interface for agents to perform UI automation across platforms. |

---

## 3. System Architecture Overview

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
│     │(Grammar Ind.)│Trainer       │Engine      │Scheduler     │  │
│     └──────────────┴──────────────┴───────────┴──────────────┘  │
│                       │              │                           │
│                       └──────────────┴───────────┐               │
│                                                  ▼               │
│                                         [Model Zoo]              │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

The system operates in two modes:

- **Daytime (inference):** Sensors feed data into shared memory; agents read from topics and write proposals (value estimates); Plinko selects an action; executors perform it; all events are logged.
- **Nighttime (learning):** Logs are analyzed to discover new skills (via grammar induction), update the world model, and run dreaming simulations; improved models and skills are stored in the Model Zoo.

---

## 4. Component Specifications

### 4.1 Sensor Layer

**Purpose:** Provide a unified, low‑latency stream of all device inputs.

**Inputs:**
- Screen frames (downsampled to 224×224 RGB, 30 fps)
- Audio (16 kHz mono, 1‑second rolling window, MFCC features)
- Keyboard/mouse/touch events
- Device sensors (accelerometer, GPS, orientation)
- System state (active app, notifications, battery)

**Implementation:**
- Platform‑specific capture APIs wrapped in a uniform interface.
- Each sensor type writes to a lock‑free ring buffer in shared memory (e.g., using `mmap` or POSIX shared memory). Ring buffers are sized to hold 60 seconds of data.
- Preprocessing: frames normalized to [0,1]; audio converted to MFCCs; events serialized as protocol buffers.

**Speculative Pre‑processing (Experimental):**  
A lightweight predictor (e.g., linear model) estimates which sensors will be needed in the next 16 ms and pre‑fetches them, reducing effective latency by 15–20%. This optimization is not yet validated and should be considered experimental.

**Research Alignment:** Shared memory for agent communication is used in the GMV mycelium project . The SMARTEDGE project  confirms the need for efficient sensor fusion in edge environments.

**Open Questions:**
- What is the optimal ring buffer size for typical usage?
- How to handle sensor dropout gracefully?

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
    value_offset: float       # learned bias for its bids (see Plinko)
    specialization_embedding: Optional[np.ndarray]  # for similarity matching
    peer_connections: List[str]   # agents frequently co-activated
```

**Agent Lifecycle Management:**
- **HIBERNATED → LOADING:** Request from Plinko or higher‑level agent.
- **LOADING → ACTIVE:** Model loaded; agent begins processing.
- **ACTIVE → IDLE:** No activity for `idle_timeout` (30 s). Agent stops polling.
- **IDLE → HIBERNATED:** No activity for `hibernate_timeout` (5 min). Model unloaded.
- **ACTIVE → DEGRADED:** Agent detects internal errors or resource constraints; continues with reduced functionality (e.g., lower confidence, skipping non‑critical tasks).

**Scheduling and Parallel Execution:**
- A thread pool (size = CPU cores − 1) runs agents round‑robin. Each agent gets a time slice (e.g., 5 ms) to process its latest input and write a proposal.
- Agents are loaded lazily based on context; frequently used agents remain active.

**Dynamic Agent Recruitment:**
When the Plinko layer’s entropy exceeds a threshold, the Swarm Manager queries the Model Zoo for agents with similar specialization embeddings (cosine similarity > 0.7). If none exist, it may spawn a temporary “helper” agent by cloning a base model and fine‑tuning on recent logs.

**Specialization Embedding:**  
Each agent has an embedding that summarizes its function. This is learned by training a small network to predict agent identity from its input‑output behavior. The embedding space can then be used for similarity matching and recruitment.

**Research Alignment:**
- Dynamic swarm formation is validated by SMARTEDGE .
- Degraded mode is inspired by NeuroMesh , which showed networks with 50% node failure continued operating at 80% capacity.
- Specialization embeddings are a novel concept requiring original research (see Section 10).

---

### 4.3 Behavioral Embedding Space (BES)

**Purpose:** Provide a shared latent space for all behaviors, enabling seed compression, transfer, and privacy.

**Training:**
- Collect a large corpus of demonstrations (from many users, with consent).
- Train a **behavioral autoencoder**:
  - Encoder maps a sequence of (state, action) pairs to a latent vector (the seed).
  - Decoder reconstructs the sequence from the latent.
  - Contrastive loss pulls embeddings of similar behaviors together, pushes different behaviors apart.
- The resulting latent space is the BES.

**Properties:**
- Dimension: 64–1024 (empirically determined).
- Behaviors that are semantically similar (e.g., "check email" and "read messages") should be close.
- The space is continuous, allowing interpolation between behaviors.

**Usage:**
- Seeds are vectors in this space.
- Agents are trained to condition on a seed: given current state and seed, they produce actions consistent with that region.

**Research Alignment:** This idea draws from universal sentence embeddings and multi‑task representation learning. It is a foundational component that addresses seed compression, conditioning, transfer, and privacy.

**Open Questions:**
- What is the optimal training objective (reconstruction + contrastive)?
- How to handle variable‑length demonstrations?
- How to ensure the space is smooth and interpolatable?

---

### 4.4 Seed Engine

#### 4.4.1 Seed Capture

When the user initiates a demonstration, the system records a sequence of (state_latent, action) pairs. This sequence is fed into the BES encoder to produce a seed vector.

**State Latent:** The state is encoded by the world model's encoder (see Section 4.7) to a fixed‑dimensional vector. This provides a compact, semantically rich representation.

**Action Representation:** Actions are also embedded (e.g., learned action embeddings). The combination of state and action at each step forms a vector that the BES encoder processes.

**Seed Output:** The resulting seed vector is stored along with metadata (timestamp, agent types involved, etc.).

#### 4.4.2 Seed Replay

To replay a seed:
1. Load the seed into the appropriate agent(s). The agent conditions on the seed via a simple mechanism: concatenation of seed with state, or FiLM modulation.
2. The agent acts with temperature = 0 (deterministic) or a low temperature for slight variation.
3. Because the seed only identifies a region in BES, the agent's behavior will adapt to the current environment while remaining faithful to the demonstrated style.

**Seed Types:**
- **Style seeds:** Encode a behavioral style (e.g., "polite email"). The agent adapts to context.
- **Action seeds:** Encode a fixed sequence (rare, for tasks requiring exact reproduction). Achieved by using a very low temperature and possibly a specialized decoder that reproduces the exact trajectory.

#### 4.4.3 Seed Storage Format (Protobuf)

```protobuf
message Seed {
    string id = 1;
    bytes embedding = 2;                 // float32 vector
    int32 embedding_dim = 3;
    uint64 created_at = 4;
    repeated string agent_types = 5;     // compatible agent types
    map<string, string> base_model_hashes = 6;
    uint32 usage_count = 7;
    float avg_success_rate = 8;
    bytes signature = 9;                  // optional
}
```

**Research Alignment:** The seed engine is novel; it relies on the BES. Key research questions are listed in Section 10.

---

### 4.5 Plinko Decision Layer (Market‑Based)

**Input:** Set of proposals from all active agents. Each proposal contains:
- `agent_id`
- `action_type`, `target`
- `value` – the agent's estimate of the action's worth (learned via RL)
- `features` – embedding of current state (for discriminators)

**Step 1: Discriminator Adjustment**
Discriminators (safety, coherence, timing) output a multiplier in [0,1] for each proposal. The adjusted value is:
\[
v_i^{\text{adj}} = v_i \cdot \prod_j d_{ij}
\]

**Step 2: Add Gumbel Noise**
\[
\epsilon_i = -\log(-\log(U(0,1)))
\]
\[
\tilde{v}_i = \log(v_i^{\text{adj}}) + \epsilon_i \cdot \tau
\]

**Step 3: Softmax Selection**
\[
\pi_i = \frac{\exp(\tilde{v}_i / \tau)}{\sum_k \exp(\tilde{v}_k / \tau)}
\]
Action sampled from this distribution.

**Step 4: Adaptive Temperature**
\[
\tau = \tau_{\text{base}} \cdot (1 + \alpha \cdot H)
\]
where \(H = -\sum_i \pi_i \log(\pi_i + \epsilon)\) is the entropy. Higher temperature when agents disagree.

**Discriminators:** Small MLPs trained on logged data (positive = actions that led to success, negative = failures). They output probabilities.

**Agent Value Learning:** Agents learn to estimate the value of their proposed actions through reinforcement learning (reward = user satisfaction). This makes the bidding process meaningful.

**Research Alignment:** Market‑based coordination is inspired by multi‑agent economics. Gumbel noise is standard. Adaptive temperature is novel but plausible.

**Open Questions:**
- How to stabilize value learning across agents?
- How to prevent agents from colluding (bidding low to let another win)?
- What is the optimal temperature adaptation function?

---

### 4.6 Action Executors & A2UI

**A2UI (Agent‑to‑UI):** A unified interface to platform accessibility APIs:
- **Android:** UIAutomator
- **iOS/macOS:** AXUI
- **Windows:** UI Automation
- **Linux:** AT‑SPI

Each executor runs in a sandboxed process with minimal permissions. Actions are logged with inverse information to enable undo.

**Other Executors:**
- **API Executor:** HTTP requests with OAuth. Credentials stored encrypted.
- **File Executor:** Sandboxed file operations within user‑specified directories.
- **Physical Executor:** ROS2 / MQTT for robotics.

**Outcome Logging:** Every execution logs success/failure, latency, and before/after state (if available).

---

### 4.7 World Model

**Purpose:** Predict environment dynamics for dreaming.

**Architecture:**
- **Encoder:** CNN + MLP (for screen) + other modalities → latent `z` (64‑dim). Trained as VAE.
- **Transition Model:** GRU that takes `(z, action_embedding)` and outputs next latent `z'`.
- **Reward Model:** MLP from `z'` to scalar reward (user satisfaction predictor).
- **Decoder:** MLP from `z` to reconstructed observation (optional, for visualization).

**Training:**
- Data: (obs_t, action, obs_{t+1}, reward) from logs.
- Loss: reconstruction loss + KL divergence + next latent prediction MSE + reward MSE.
- Counterfactual augmentation: swap actions in similar contexts to generate synthetic transitions, improving generalization.

**Research Alignment:** This is a standard world model architecture (Dreamer‑style). The novelty is its application to personal digital environments.

**Open Questions:**
- How to handle partially observable environments (e.g., background processes)?
- What is the optimal latent dimension for UI dynamics?
- How to incorporate counterfactual augmentation effectively?

---

### 4.8 Dreaming Engine

**Purpose:** Improve skills via simulation in the world model.

**Multi‑Scale Dreaming:**
| Scale | Horizon | Mutation Operators |
|-------|---------|--------------------|
| Micro | 10–100 steps | Gaussian noise on action parameters |
| Meso | 100–1000 steps | Swap adjacent actions, insert pauses, delete redundant |
| Macro | 1000–10000 steps | Replace sub‑sequence with another skill (seed interpolation) |

**Algorithm:**
```python
def dream(skill_seed, scale, num_simulations=1000):
    skill = load_skill(skill_seed)
    world = load_world_model()
    best_reward = -inf
    best_variation = skill
    for _ in range(num_simulations):
        var = mutate(skill, scale)   # returns a modified seed
        state = sample_initial_state()
        total = 0
        for step in range(horizon[scale]):
            action = agent.act(state, seed=var)  # agent conditioned on var
            state, reward = world.predict(state, action)
            total += reward
        if total > best_reward:
            best_reward = total
            best_variation = var
    if best_reward > skill.performance:
        save_skill(best_variation)
    return best_variation
```

**Mutation Operators:**
- **Micro:** Add small noise to seed in BES space (since seeds are continuous).
- **Meso:** Apply grammar mutations (insert/delete/swap) to the skill's underlying sequence representation (if available) and re‑encode.
- **Macro:** Interpolate between two seeds in BES space, or concatenate sequences from two skills.

**Research Alignment:** Dreaming is inspired by GW‑Dreamer and neuromorphic dreaming. Multi‑scale dreaming and BES‑based mutation are novel.

**Open Questions:**
- How to ensure mutated seeds stay within the manifold of valid behaviors?
- Does dreaming in BES space transfer better to real environments?
- What is the optimal number of simulations per skill?

---

### 4.9 Skill Chunker (Grammar Induction)

**Purpose:** Discover reusable skills from logged sequences.

**Approach:** Induce a stochastic context‑free grammar (SCFG) from action sequences.

**Algorithm (Sequitur‑inspired):**
1. Start with a sequence of atomic actions (each with a type and parameters).
2. Iteratively find the most frequent digram (pair of consecutive symbols) and replace it with a new nonterminal (skill). Record the rule.
3. Continue until no digram occurs more than a threshold.
4. The resulting grammar has productions that represent skills at multiple levels of abstraction.

**Skill Representation:** Each nonterminal (skill) can be represented by its expansion sequence and also by a seed (embedding) from the BES encoder applied to that sequence.

**Storage:** Skills stored as grammar rules plus optional seed embedding.

**Research Alignment:** Grammar induction is a classic technique; applying it to action sequences for skill discovery is novel.

**Open Questions:**
- How to handle continuous action parameters (not just discrete types)?
- How to incorporate the BES into grammar learning?
- How to evaluate the quality of discovered skills?

---

### 4.10 Memory (Vector Database)

**Purpose:** Long‑term storage of episodic memories.

**Implementation:** ChromaDB or LanceDB, running locally.

**Schema:**
- Collection per user or domain.
- Each record: `embedding` (from world model encoder), `metadata` (timestamp, app, action, outcome), optional raw data (e.g., screenshot hash).

**Retrieval:** Agents query with current observation embedding; database returns top‑k similar past experiences. Retrieved memories are appended to agent context (e.g., as additional tokens in transformer input).

**Research Alignment:** Vector databases are industry standard. The concept of agent memory is supported by EngramNCA research on private, cell‑internal memory channels.

---

### 4.11 Model Zoo

**Storage Structure:**
```
/models/
  base/                          # base agent models
    vision_v3.onnx
    text_v2.onnx
  skills/                        # skill seeds and grammar rules
    skill_abc123.seed
    skill_def456.grammar
  world/                         # world model versions
    world_model_v5/
      encoder.onnx
      transition.onnx
      reward.onnx
  metadata.db
```

**Metadata Schema (SQLite):**
```sql
CREATE TABLE models (
    id TEXT PRIMARY KEY,
    type TEXT,           -- 'base', 'skill', 'world'
    version INT,
    hash TEXT,
    created DATE,
    metrics TEXT,        -- JSON of accuracy, latency, usage
    parent_id TEXT,
    usage_count INT
);
```

**Automatic Rollback:** New models are monitored for 24 hours; if performance drops below previous version, revert.

---

### 4.12 Training Scheduler

**Purpose:** Orchestrate nightly learning tasks.

**ROI‑Based Prioritization:**
\[
ROI = \frac{\text{expected\_improvement} \times \text{frequency}}{\text{estimated\_cost}}
\]
- expected_improvement: estimated from recent performance trends.
- frequency: how often the skill/agent is used.
- cost: estimated GPU hours.

**Local vs. Cloud Decision:** If `cost > local_budget` and user has enabled cloud, offload to LucidDreamer.ai (or compatible service) with differential privacy. Otherwise, run locally.

**Predictive Wake‑Up:** Based on historical usage, predict when the user will next use the device. Schedule training to finish 5 minutes before that time.

**Research Alignment:** Edge‑cloud interplay validated by SMARTEDGE . ROI prioritization and predictive wake‑up are novel but plausible.

**Open Questions:**
- How to accurately estimate expected improvement?
- How to measure frequency in a way that captures future potential?

---

## 5. Data Formats & Protocols

### 5.1 Seed Format (Protobuf) – see 4.4.3

### 5.2 Proposal Format (Cap'n Proto)

```capnp
@0x8a1b4c3d5e6f7890;

struct Proposal {
    agentId @0 :Text;
    timestamp @1 :Float64;
    actionType @2 :ActionType;
    value @3 :Float32;                 # agent's estimated value
    target @4 :Target;
    features @5 :List(Float32);        # state embedding for discriminators

    enum ActionType {
        click @0;
        type @1;
        scroll @2;
        apiCall @3;
        fileOp @4;
        skillInvoke @5;
        noop @6;
    }

    struct Target {
        union {
            element @0 :Text;
            coordinates @1 :List(Float32, 2);
            url @2 :Text;
            filePath @3 :Text;
            skillId @4 :Text;
        }
    }
}
```

### 5.3 Log Format (Parquet) – see 4.6 outcome logging

### 5.4 Agent Communication Protocol

- **Topics:** Named ring buffers in shared memory (lock‑free MPSC queues).
- **Message:** Serialized Proposal (Cap'n Proto).
- **Delivery:** Best‑effort; if buffer full, oldest message is overwritten (real‑time requirement).

### 5.5 Seed Exchange Protocol (Proposed)

```
POST /seed/export
{
  "skill_id": "skill_email_check_v3",
  "format": "binary"
}
Response:
{
  "seed_id": "uuid",
  "data": "base64_encoded_seed",
  "compatibility": {
    "required_agents": ["intent_v2", "vision_v3"],
    "min_version": "1.2.0"
  }
}

POST /seed/import
{
  "seed_data": "base64_encoded_seed",
  "verify": true
}
Response:
{
  "success": true,
  "skill_id": "imported_skill_uuid",
  "warnings": []
}
```

---

## 6. APIs and Developer Interfaces

### 6.1 Public API for Developers

```python
import mycelium as mc

# Create a swarm
swarm = mc.Swarm()

# Add a pre‑trained agent
swarm.add_agent(mc.Agent.from_registry("vision-mobilenet-v3"))

# Register a custom agent
my_agent = mc.Agent(
    model_path="my_model.onnx",
    input_topics=["/sensors/camera"],
    output_topic="/proposals/custom"
)
swarm.add_agent(my_agent)

# Run one step (processes new sensor data)
action = swarm.step()

# Export a seed from a logged skill
seed = swarm.export_skill("skill_email_check_v3")

# Import and use a seed
swarm.import_skill(seed)
swarm.invoke_skill("skill_email_check_v3", parameters={"app": "outlook"})
```

### 6.2 Agent Development SDK

- Tools to convert PyTorch/TensorFlow models to ONNX with quantization.
- Simulator to test agents in a controlled environment.
- Profiler to measure latency and memory usage.

### 6.3 LucidDreamer.ai Integration (Optional)

- Client library to send anonymized training jobs.
- API for on‑demand inference with large models.

---

## 7. Implementation Roadmap

| Phase | Timeline | Milestones |
|-------|----------|------------|
| **1. Prototype** | 0–3 months | Core agent runtime with shared memory; basic Plinko (random noise); local logging; CLI; simple BES prototype |
| **2. On‑Device Learning** | 4–9 months | Discriminators + adaptive temperature; world model trainer; micro‑dreaming; training scheduler; A2UI (Android); BES integration |
| **3. Advanced Features** | 10–15 months | Multi‑scale dreaming; grammar‑based skill chunking; vector database integration; seed serialization; privacy mechanisms |
| **4. Ecosystem** | 16–24 months | Cross‑platform A2UI; federated learning (opt‑in); skill marketplace; hardware acceleration |

---

## 8. Research Agenda (Open Questions)

### 8.1 Behavioral Embedding Space

1. **What is the optimal training objective?** (Reconstruction + contrastive? Add adversarial?)
2. **How to handle variable‑length demonstrations?** (Padding, attention, or recurrent encoder?)
3. **How to ensure smooth interpolation?** (Is linear interpolation meaningful? Should we use spherical interpolation?)
4. **What dimension balances compression and expressiveness?** (Empirical scaling studies needed.)

### 8.2 Seed Conditioning

5. **What conditioning mechanism works best?** (Concatenation, FiLM, cross‑attention?)
6. **How many seeds can an agent handle without forgetting base capabilities?**
7. **Can seeds be composed?** (Linear combination? Attention over multiple seeds?)

### 8.3 Plinko Market

8. **How to stabilize value learning across agents?** (Shared critic? Opponent modeling?)
9. **How to prevent collusion?** (Is it a real risk? Can discriminators detect?)
10. **What temperature function optimizes exploration?** (Linear? Exponential? Learned?)

### 8.4 Skill Chunking via Grammar Induction

11. **How to handle continuous action parameters?** (Discretize? Parameterized grammar?)
12. **How to integrate BES with grammar?** (Each nonterminal gets a seed embedding.)
13. **How to evaluate skill quality?** (Reusability, transfer, human judgment.)

### 8.5 World Model & Dreaming

14. **What is the optimal latent dimension for UI dynamics?**
15. **How to incorporate counterfactual augmentation effectively?**
16. **Does dreaming in BES space transfer better than raw action space?**
17. **How many dreaming simulations per skill are optimal?**

### 8.6 Privacy & Security

18. **How much information can be extracted from a seed?** (Membership inference, attribute inference.)
19. **Can differential privacy protect seeds without destroying utility?**
20. **How to design a secure seed exchange protocol?** (Signatures, provenance, sandboxing.)

### 8.7 Emergent Properties

21. **How to measure emergence in Mycelium?** (Information‑theoretic metrics from [citation].)
22. **Can we steer emergence with prompts?** (Theory of Mind prompting experiments.)
23. **How does agent diversity affect specialization?**

### 8.8 Human‑AI Interaction

24. **What mental models do users form of Mycelium?**
25. **How to calibrate user trust?**
26. **What explanation interfaces are most effective?**

---

## 9. Conclusion

Mycelium offers a radical new approach to building intelligent systems—one where behavior is demonstrated, compressed into seeds in a shared embedding space, and shared like digital artifacts. The architecture synthesizes proven techniques from edge AI, multi‑agent systems, and representation learning, while introducing novel components that require validation.

This document provides a complete blueprint for implementation. We encourage the community to build, experiment, and contribute. The future of AI is not monolithic; it is a swarm.

---

## 10. References

1. SMARTEDGE project. "Low-code Toolchain for Edge Intelligence." EU Horizon 2020.
2. Bio Cognitive Mesh. "Harnessing Swarm Intelligence for Self-Organizing AI at the Network Edge." IEEE STCR 2025.
3. NeuroMesh. "Self-healing Distributed AI Swarm." Devpost 2025.
4. MyceliumWebServer. "Federated learning based on ActivityPub." GitHub, 2025.
5. GMV mycelium. "Service-Oriented Architecture for Robot Swarms." GitHub, 2025.
6. Apple Mycelium. "Visualizing Agent Networks." SIGCHI 2024.
7. EngramNCA. "Private Memory Channels in Cellular Automata." arXiv preprint, 2025.
8. Hafner, D. et al. "Dream to Control: Learning Behaviors by Latent Imagination." ICLR 2020.
9. Maytié, L. et al. "Multimodal Dreaming: A Global Workspace Approach to World Model-Based Reinforcement Learning." arXiv 2502.21142, 2025.
10. [Emergence metrics paper] – to be added.

---

*This document is a living specification. For the latest version, source code, and contribution guidelines, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
