# Mycelium Architecture Specification

**Version 2.0 — May 2026**  
**SuperInstance Open Source Initiative**  
*Authors: The Mycelium Community*

---

## Executive Summary

Mycelium is an open‑source platform for building **living agent systems**—software that learns from demonstration, compresses behaviors into reusable **seeds**, and executes them deterministically across a swarm of tiny neural models. This document provides a complete, implementable architecture for Mycelium, intended for engineers, researchers, and contributors.

The architecture synthesizes insights from edge AI, multi‑agent systems, world model‑based reinforcement learning, and skill discovery. Where components are well‑supported by published research, we cite that work. Where Mycelium introduces novel concepts—such as seed‑based behavior encoding, the Plinko decision layer, and multi‑scale dreaming—we clearly identify them as open research areas and outline the experiments needed to validate them.

Our goal is to build a system that grows with its users, enables simulation‑first development, and turns AI into a shareable, personal artifact. We invite the community to help close the research gaps and make this vision a reality.

---

## 1. Introduction

### 1.1 The Problem with Static Intelligence

Traditional software and AI models are static. Once deployed, they cannot learn from individual users, adapt to changing environments, or improve over time. They remain tools we operate, not partners we embody. This limitation is fundamental to the current development paradigm: we write code to specify behavior, compile it, and ship it. Any change requires a new release.

The shift to cloud‑based AI has exacerbated the problem. Models are trained once on population data and then frozen. They treat every user as an average, forget everything after each interaction, and require constant connectivity . For real‑time, personal, and private applications, this approach is untenable.

### 1.2 A New Paradigm: Demonstration‑Driven Development

Mycelium inverts the development process. Instead of writing code, you **demonstrate** the desired behavior. The system observes the sequence of actions and decisions, compresses it into a compact **seed**, and later reproduces that exact behavior from a simple prompt. Code becomes optional—used only when mathematical proof or formal verification is required.

This paradigm shift has profound implications:
- **Faster prototyping:** Go from idea to working behavior in minutes.
- **Personalization:** The system learns your unique style, not a population average.
- **Shareability:** Seeds can be exchanged like files, enabling skill transfer without data exposure.
- **Continuous improvement:** Nightly dreaming and learning cycles refine behaviors automatically.

### 1.3 Core Thesis: Behavior as Primary Artifact

In Mycelium, behavior is the source of truth. A seed is a compressed representation of a behavioral sequence that can be deterministically replayed given the same prompt and environmental context. Seeds are small (typically 64–1024 floats), making them easy to store, share, and version. They capture not just low‑level actions but also the decision policies that produced them.

This thesis rests on two claims:
1. **Sufficient compression:** A wide range of useful behaviors can be encoded into compact vectors without significant loss.
2. **Deterministic replay:** Given the same prompt and seed, the system will produce the same behavior every time, even as the underlying agents continue to learn.

Both claims require empirical validation and are the focus of ongoing research (see Section 11).

### 1.4 Document Scope and Audience

This document is a technical blueprint for building Mycelium. It describes every component in sufficient detail to be implemented from scratch, including data structures, algorithms, and interfaces. It also identifies open research questions and outlines a roadmap for validation.

The intended audience includes:
- Developers who want to build applications on Mycelium
- Researchers interested in multi‑agent systems, continual learning, and human‑AI interaction
- Contributors to the open‑source project

---

## 2. Core Concepts

| Concept | Definition |
|---------|------------|
| **Agent** | A tiny neural model (1–100M parameters) specialized for a narrow task. Agents run continuously, consume sensor data, and produce proposals. |
| **Prompt** | A natural‑language or structured instruction that initiates a behavior. Prompts are fed to higher‑level agents to invoke skills. |
| **Seed** | A compact vector (64–1024 floats) that encodes a behavioral sequence. A seed, together with a prompt, deterministically reproduces a demonstrated behavior. |
| **Skill** | A stored, reusable behavior, often represented as a seed plus metadata. Skills can be composed hierarchically. |
| **World Model** | A predictive model that learns how the environment (apps, UI, system) responds to actions. Used for dreaming and simulation. |
| **Dreaming** | Offline simulation where the system uses the world model to explore variations of skills, selecting those that maximize predicted reward. |
| **Memory** | A vector database where agents store and retrieve past experiences to inform future decisions. |
| **Plinko Layer** | A stochastic decision mechanism that selects among competing agent proposals using Gumbel noise and adaptive temperature. |
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
│     │              │Trainer       │Engine      │Scheduler     │  │
│     └──────────────┴──────────────┴───────────┴──────────────┘  │
│                       │              │                           │
│                       └──────────────┴───────────┐               │
│                                                  ▼               │
│                                         [Model Zoo]              │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

The system operates in two modes:

- **Daytime (inference):** Sensors feed data into shared memory; agents read from topics and write proposals; the Plinko layer selects an action; executors perform it; all events are logged.
- **Nighttime (learning):** Logs are analyzed to discover new skills, update the world model, and run dreaming simulations; improved models and skills are stored in the Model Zoo.

This edge‑cloud continuum is supported by the SMARTEDGE project , which validates the need for dynamic swarm formation and cross‑layer orchestration.

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
    temperature_preference: float
    specialization_embedding: Optional[np.ndarray]  # for similarity matching
    peer_connections: List[str]                      # agents frequently co-activated
```

**Agent Lifecycle Management:**
- **HIBERNATED → LOADING:** Request from Plinko or higher‑level agent.
- **LOADING → ACTIVE:** Model loaded; agent begins processing.
- **ACTIVE → IDLE:** No activity for `idle_timeout` (30 s). Agent stops polling.
- **IDLE → HIBERNATED:** No activity for `hibernate_timeout` (5 min). Model unloaded.
- **ACTIVE → DEGRADED:** Agent detects internal errors or resource constraints; continues with reduced functionality.

**Scheduling and Parallel Execution:**
- A thread pool (size = CPU cores − 1) runs agents round‑robin. Each agent gets a time slice (e.g., 5 ms) to process its latest input and write a proposal.
- Agents are loaded lazily based on context; frequently used agents remain active.

**Dynamic Agent Recruitment:**
When the Plinko layer’s entropy exceeds a threshold, the Swarm Manager queries the Model Zoo for agents with similar specialization embeddings (cosine similarity > 0.7). If none exist, it may spawn a temporary “helper” agent by cloning a base model and fine‑tuning on recent logs.

**Research Alignment:**
- Dynamic swarm formation is validated by SMARTEDGE .
- Degraded mode is inspired by NeuroMesh , which showed networks with 50% node failure continued operating at 80% capacity.
- Specialization embeddings are a novel concept requiring original research (see Section 11).

---

### 4.3 Seed Capture & Replay Engine

This is the most innovative component of Mycelium and the one with the largest research gap.

#### 4.3.1 Demonstration Capture

The user initiates capture (e.g., voice command “watch me” or UI button). The system records all subsequent **action‑observation pairs** until stop.

- **Observation** is the sensor latent vector produced by the world model encoder (see Section 4.8).
- **Action** is the selected proposal (including action type, target, and parameters).

The sequence of pairs is stored temporarily.

#### 4.3.2 Seed Encoder Architecture

```python
class SeedEncoder(nn.Module):
    def __init__(self, obs_dim, action_dim, latent_dim=256):
        self.obs_encoder = nn.Linear(obs_dim, 128)
        self.action_encoder = nn.Linear(action_dim, 128)
        self.lstm = nn.LSTM(256, 256, batch_first=True)
        self.latent_proj = nn.Linear(256, latent_dim)

    def forward(self, obs_seq, action_seq):
        obs_encoded = self.obs_encoder(obs_seq)
        action_encoded = self.action_encoder(action_seq)
        combined = torch.cat([obs_encoded, action_encoded], dim=-1)
        _, (hidden, _) = self.lstm(combined)
        seed = self.latent_proj(hidden[-1])
        return seed
```

**Training:** The encoder is trained with a combination of:
- **Reconstruction loss:** A decoder (mirroring the encoder) attempts to reconstruct the sequence from the seed.
- **Contrastive loss:** Seeds from different demonstrations should be dissimilar; seeds from the same demonstration should be similar under perturbations.

**Research Gap:** No existing work demonstrates that full behavioral sequences can be compressed into compact vectors and deterministically replayed. This is the central hypothesis of Mycelium and requires extensive validation (see Section 11).

#### 4.3.3 Seed Replay

To replay a seed:
1. The seed is loaded into the target agent (the agent that was active during capture). The conditioning mechanism is an open research problem; options include:
   - **Feature‑wise Linear Modulation (FiLM):** The seed modulates the agent’s internal activations.
   - **Latent concatenation:** The seed is concatenated to the agent’s input or hidden state.
   - **Separate policy network:** The seed selects a sub‑policy within the agent.
2. The agent acts with temperature = 0 (deterministic inference), producing actions step‑by‑step. Because the agent’s parameters are fixed, the same seed should produce the same action sequence given the same observations. However, observations may differ in a new environment, so the behavior will adapt—this contradicts “exact reproduction.” We resolve this by defining two seed types (see Section 11).

#### 4.3.4 Seed Storage Format (Protobuf)

```protobuf
message Seed {
    string id = 1;
    string skill_id = 2;                // if associated with a named skill
    repeated string agent_types = 3;     // which agent types this works with
    map<string, string> base_model_hashes = 4; // required base model versions
    bytes embedding = 5;                 // float32 vector
    int32 embedding_dim = 6;
    uint64 created_at = 7;
    uint32 usage_count = 8;
    float avg_success_rate = 9;
    bytes signature = 10;                 // optional cryptographic signature
}
```

---

### 4.4 Plinko Decision Layer

**Input:** Set of proposals from all active agents in the current time window (typically 16 ms). Each proposal contains `agent_id`, `action_type`, `target`, `confidence` (0–1), and `features` (embedding of input).

**Step 1: Discriminator Pass**  
Each proposal is scored by a set of discriminators (small MLPs). They output a probability in [0,1] that the action is acceptable.

- **Safety discriminator:** Trained on human‑labeled harmful actions.
- **Coherence discriminator:** Trained to distinguish actions that led to user corrections vs. those that didn’t.
- **Timing discriminator:** Prevents rapid‑fire repeats.

The combined acceptance probability is:
\[
p_i^{\text{disc}} = \prod_{j} d_{ij}
\]

**Step 2: Score Computation**
\[
s_i = \log(\text{confidence}_i) + \log(p_i^{\text{disc}})
\]
Add Gumbel noise for stochasticity:
\[
\epsilon_i = -\log(-\log(U(0,1)))
\]
\[
\tilde{s}_i = s_i + \epsilon_i \cdot \tau
\]

**Step 3: Selection**
\[
\pi_i = \frac{\exp(\tilde{s}_i / \tau)}{\sum_k \exp(\tilde{s}_k / \tau)}
\]
Action sampled from this categorical distribution.

**Step 4: Adaptive Temperature**
\[
\tau = \tau_{\text{base}} \cdot (1 + \alpha \cdot H)
\]
where \(H = -\sum_i \pi_i \log(\pi_i + \epsilon)\) is the entropy of the proposal distribution. Higher temperature when uncertain, promoting exploration.

**Research Alignment:** Gumbel‑Softmax is a standard technique for differentiable sampling. The adaptive temperature mechanism is novel and requires empirical validation.

---

### 4.5 Action Executors & A2UI

**A2UI (Agent‑to‑UI):** A unified interface to platform accessibility APIs:
- **Android:** UIAutomator
- **iOS/macOS:** AXUI
- **Windows:** UI Automation
- **Linux:** AT‑SPI

Each executor runs in a sandboxed process with minimal permissions. Actions are logged with inverse information to enable undo.

**Other Executors:**
- **API Executor:** HTTP requests with OAuth.
- **File Executor:** Sandboxed file operations.
- **Physical Executor:** ROS2 / MQTT for robotics.

**Research Alignment:** UI automation is well‑established; the novelty lies in the agent‑facing abstraction.

---

### 4.6 Experience Logger

**Log Format (Parquet):**
```
timestamp: int64
session_id: binary
sensor_latent: bytes          # from world model encoder
proposals: list<Proposal>     # serialized
selected_action: Proposal
discriminator_scores: list<float>
temperature: float
outcome: {
    success: bool
    latency_ms: int32
    user_feedback: int8        # -1=bad, 0=none, 1=good
}
system_state: {
    battery: float
    cpu: float
    memory: float
}
```

**Compression:** Sensor frames are optionally encoded to latent vectors using the world model’s encoder, reducing storage by ~90%.

**Circular Buffer:** Logs kept for 30 days by default, oldest deleted first.

---

### 4.7 Skill Chunker

**Purpose:** Discover reusable skills from logged sequences.

**Input:** Sequences of (observation_latent, action_embedding) from logs.

**Algorithm:**

1. **Frequent Subsequence Mining:** Use PrefixSpan to find sequences occurring above a threshold (e.g., 5 times).
2. **Temporal Autoencoder:** Train an LSTM autoencoder to compress each candidate sequence into a fixed‑dimensional vector (the skill embedding).
3. **MDL‑Based Boundary Detection:** For each candidate, compute description length: `L(chunk) = L(model) + L(data|model)`. Chunks that minimize total description length are kept. This automatically discovers hierarchical boundaries (sub‑skills).
4. **Skill Storage:** Skills are stored as embeddings plus metadata; they can be invoked as atomic units by higher‑level agents.

**Research Alignment:** PrefixSpan and temporal autoencoders are standard. The combination with MDL for unsupervised segmentation is novel and requires validation.

---

### 4.8 World Model

**Architecture:**
- **Encoder:** VAE (MLP) compresses observation to latent `z` (64‑dim).
- **Transition Model:** GRU predicts next latent given current latent and action.
- **Reward Model:** MLP predicts user satisfaction (scalar) from latent.
- **Decoder:** MLP reconstructs observation from latent (optional, for visualization).

**Training:**
- Data: (obs_t, action, obs_{t+1}, reward) from logs.
- Loss: reconstruction loss + KL divergence + prediction MSE + reward MSE.
- Counterfactual augmentation: swap actions in similar contexts to generate synthetic transitions, improving generalization.

**Research Alignment:** World models for dreaming are inspired by DreamerV3 (Hafner et al.) and GW‑Dreamer . However, those works focus on training policies from scratch, not refining existing skills. The application to skill dreaming is novel.

---

### 4.9 Dreaming Engine

**Purpose:** Improve skills via simulation in the world model.

**Multi‑Scale Dreaming:**
| Scale | Horizon | Mutation Operators |
|-------|---------|--------------------|
| Micro | 10–100 steps | Gaussian noise on action parameters |
| Meso | 100–1000 steps | Swap adjacent actions, insert pauses, delete redundant |
| Macro | 1000–10000 steps | Replace sub‑sequence with another skill, concatenate skills |

**Algorithm:**
```python
def dream(skill_id, scale, num_simulations=1000):
    skill = load_skill(skill_id)
    world = load_world_model()
    best_reward = -inf
    best_variation = None
    for _ in range(num_simulations):
        var = mutate(skill, scale)
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

**Research Gap:** No existing work validates that multi‑scale dreaming with heuristic mutation operators improves real‑world performance. This is a core area for empirical research.

---

### 4.10 Training Scheduler

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

**Research Alignment:** Edge‑cloud interplay is validated by SMARTEDGE . ROI prioritization and predictive wake‑up are novel optimizations requiring validation.

---

### 4.11 Memory (Vector Database)

**Purpose:** Long‑term storage of episodic memories.

**Implementation:** ChromaDB or LanceDB, running locally.

**Schema:**
- Collection per user or domain.
- Each record: `embedding` (from world model encoder), `metadata` (timestamp, app, action, outcome), optional raw data.

**Retrieval:** Agents query with current observation embedding; database returns top‑k similar past experiences. Retrieved memories are appended to agent context.

**Research Alignment:** Vector databases are industry standard. The concept of agent memory is supported by EngramNCA research  on private, cell‑internal memory channels.

---

### 4.12 Model Zoo

**Storage Structure:**
```
/models/
  base/
    vision_v3.onnx
    text_v2.onnx
  skills/
    skill_abc123.seed
    skill_def456.seed
  world/
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
    metrics TEXT,        -- JSON of accuracy, latency
    parent_id TEXT,
    usage_count INT
);
```

**Automatic Rollback:** New models are monitored for 24 hours; if performance drops below previous version, revert.

---

## 5. Data Formats & Protocols

### 5.1 Seed Format (see 4.3.4)

### 5.2 Proposal Format (Cap'n Proto)

```capnp
@0x8a1b4c3d5e6f7890;

struct Proposal {
    agentId @0 :Text;
    timestamp @1 :Float64;
    actionType @2 :ActionType;
    confidence @3 :Float32;
    target @4 :Target;
    features @5 :List(Float32);

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

### 5.3 Log Format (Parquet) – see 4.6

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
| **1. Prototype** | 0–3 months | Core agent runtime with shared memory; basic Plinko (random noise); local logging; CLI |
| **2. On‑Device Learning** | 4–9 months | Discriminators + adaptive temperature; world model trainer; micro‑dreaming; training scheduler; A2UI (Android) |
| **3. Advanced Features** | 10–15 months | Multi‑scale dreaming; hierarchical skill chunking with MDL; vector database integration; seed serialization |
| **4. Ecosystem** | 16–24 months | Cross‑platform A2UI; federated learning (opt‑in); skill marketplace; hardware acceleration |

---

## 8. Research Agenda (Open Problems)

The following components are novel to Mycelium and require original research and empirical validation:

| Component | Research Question | Proposed Experiments |
|-----------|-------------------|----------------------|
| **Seed Encoding** | Can complex behavioral sequences be compressed into 64–1024‑dim vectors with sufficient fidelity for deterministic replay? | Benchmark on diverse tasks (UI automation, robotics, text editing). Measure reconstruction accuracy and downstream task success. |
| **Seed Conditioning** | What mechanism best injects a seed into an agent to influence behavior without disrupting base capabilities? | Compare FiLM, latent concatenation, separate policy networks on held‑out tasks. |
| **Determinism vs. Adaptation** | How to reconcile exact replay with environmental variation? | Define and evaluate two seed types: *action seeds* (exact) and *policy seeds* (adaptive). Measure trade‑offs. |
| **Plinko Adaptive Temperature** | Does entropy‑based temperature improve decision quality over fixed temperature? | A/B test in simulated environments with varying uncertainty. |
| **Skill Chunking MDL** | Does MDL‑based boundary detection discover more reusable skills than fixed‑window methods? | Compare skill reuse rates and downstream task performance. |
| **Dreaming for Skill Refinement** | Do multi‑scale dreaming and heuristic mutations produce skills that transfer to real environments? | Sim‑to‑real experiments: refine skills in world model, then test in real environment. Measure improvement correlation. |
| **Training Scheduler ROI** | Does ROI‑based prioritization lead to faster learning than round‑robin? | Longitudinal study with multiple users, measuring skill acquisition rates. |

We invite researchers and practitioners to collaborate on these open problems.

---

## 9. Conclusion

Mycelium offers a radical new approach to building intelligent systems—one where behavior is demonstrated, compressed into seeds, and shared like digital artifacts. The architecture synthesizes proven techniques from edge AI, multi‑agent systems, and world model‑based learning, while introducing novel components that require validation.

This document provides a complete blueprint for implementation. We encourage the community to build, experiment, and contribute. The future of AI is not monolithic; it is a swarm.

---

## 10. References

1. SMARTEDGE project. "Low-code Toolchain for Edge Intelligence." EU Horizon 2020. [Online]. Available: https://smart-edge.eu
2. Bio Cognitive Mesh. "Harnessing Swarm Intelligence for Self-Organizing AI at the Network Edge." IEEE STCR 2025.
3. NeuroMesh. "Self-healing Distributed AI Swarm." Devpost 2025. [Online]. Available: https://devpost.com/software/neuromesh
4. MyceliumWebServer. "Federated learning based on ActivityPub." GitHub, 2025. [Online]. Available: https://github.com/bluebbberry/MyceliumWebServer
5. GMV mycelium. "Service-Oriented Architecture for Robot Swarms." GitHub, 2025. [Online]. Available: https://github.com/GMV-centrum/mycelium
6. Apple Mycelium. "Visualizing Agent Networks." SIGCHI 2024.
7. EngramNCA. "Private Memory Channels in Cellular Automata." arXiv preprint, 2025.
8. Hafner, D. et al. "Dream to Control: Learning Behaviors by Latent Imagination." ICLR 2020.
9. Maytié, L. et al. "Multimodal Dreaming: A Global Workspace Approach to World Model-Based Reinforcement Learning." arXiv 2502.21142, 2025.

---

*This document is a living specification. For the latest version, source code, and contribution guidelines, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
