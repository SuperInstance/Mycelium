# Mycelium: A Technical Architecture for Continuously Learning, Demonstration-Driven Intelligence

**Version 1.0**  
*SuperInstance Open Source Initiative*

---

## 1. Introduction

Mycelium is an open‑source platform for building **living agent systems**—software that learns from demonstration, compresses behaviors into reusable **seeds**, and executes them deterministically using a swarm of tiny neural models. Unlike traditional systems where logic is encoded in source code, Mycelium treats behavior as the primary artifact: you show it what to do once; it records the sequence of agent activations and decisions as a seed. Later, a single prompt plus that seed reproduces the exact same behavior, without re‑compilation or re‑learning.

This document provides a complete, implementable architecture for Mycelium. It is intended for engineers, researchers, and hobbyists who want to build, extend, or contribute to the platform. Every component is described in enough detail to be built from scratch, with algorithms, data structures, and interface specifications.

---

## 2. System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         Mycelium System                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  [Sensors] → [Preprocessor] → [Shared Memory]                    │
│                                     │                             │
│                                     ▼                             │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                      Agent Swarm                           │   │
│  │  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐            │   │
│  │  │Vision  │ │ Audio  │ │ Text   │ │Intent  │  ...        │   │
│  │  │Agent   │ │ Agent  │ │ Agent  │ │Agent   │            │   │
│  │  └────────┘ └────────┘ └────────┘ └────────┘            │   │
│  └───────────────────────────────────────────────────────────┘   │
│                                     │                             │
│                                     ▼                             │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                   Plinko Decision Layer                    │   │
│  │  [Discriminators] → [Noise Injection] → [Selection]       │   │
│  └───────────────────────────────────────────────────────────┘   │
│                                     │                             │
│                                     ▼                             │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                     Action Executors                        │   │
│  │  [A2UI] [API] [File] [Physical]                           │   │
│  └───────────────────────────────────────────────────────────┘   │
│                                     │                             │
│                                     ▼                             │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                   Experience Logger                         │   │
│  │  [Compressed Logs] → [Circular Buffer]                    │   │
│  └───────────────────────────────────────────────────────────┘   │
│                                     │                             │
│                                     ▼                             │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                    Overnight Learning                       │   │
│  │  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐         │   │
│  │  │Skill Chunker│ │World Model  │ │Dreaming     │         │   │
│  │  │             │ │Trainer      │ │Engine       │         │   │
│  │  └─────────────┘ └─────────────┘ └─────────────┘         │   │
│  │         │              │              │                   │   │
│  │         └──────────────┴──────────────┘                   │   │
│  │                        │                                   │   │
│  │                        ▼                                   │   │
│  │              ┌─────────────────────┐                       │   │
│  │              │   Training Scheduler │                       │   │
│  │              └─────────────────────┘                       │   │
│  └───────────────────────────────────────────────────────────┘   │
│                        │                                           │
│                        ▼                                           │
│  ┌───────────────────────────────────────────────────────────┐   │
│  │                       Model Zoo                            │   │
│  │  [Base Models] [LoRAs] [Skills] [World Models]           │   │
│  └───────────────────────────────────────────────────────────┘   │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

The system operates in two modes:
- **Daytime (inference):** Sensors feed data into shared memory; agents read, propose actions; Plinko selects one; executors perform it; all events are logged.
- **Nighttime (learning):** Logs are analyzed to discover skills, update the world model, and run dreaming simulations; improved models and skills are stored in the Model Zoo.

---

## 3. Core Concepts

### 3.1 Agents
Agents are small neural models (1–100M parameters) specialized for narrow tasks. Each agent runs continuously, consuming sensor data and producing **proposals**—suggested actions with confidence scores. Agents are loaded lazily and can be hibernated to save memory.

### 3.2 Prompts and Seeds
- A **prompt** is the initial input to a higher‑level agent (e.g., “check email”). 
- A **seed** is a compressed vector (typically 64–256 floats) that encodes a specific behavior—a sequence of agent activations and decisions. Given the same prompt and seed, the system will reproduce the exact behavior every time. Seeds are generated by the skill chunker and can be exported, shared, and imported.

### 3.3 Skills
A skill is a stored, reusable behavior, represented internally as a small neural network (e.g., a tiny RNN) that outputs a sequence of sub‑actions when given a starting state. Skills are built from frequently occurring patterns in the logs.

### 3.4 World Model
The world model is a predictive model of how the environment (apps, UI, system) responds to actions. It consists of an encoder (compressing observations), a transition model (predicting next state), and a reward predictor (estimating user satisfaction). It is trained on logged experience and used for dreaming.

### 3.5 Dreaming
Dreaming is offline simulation where the system uses the world model to explore variations of skills, selecting those that maximize predicted reward. This allows improvement without real‑world interaction.

---

## 4. Component Details

### 4.1 Sensor Layer

**Purpose:** Capture raw input streams and make them available to agents.

**Inputs:**
- Screen frames (downsampled to 224×224 RGB, 30 fps)
- Audio (16 kHz mono, 1‑second rolling window)
- Keyboard/mouse/touch events
- Device sensors (accelerometer, GPS, orientation)
- System state (active app, notifications, battery)

**Implementation:**
- Platform‑specific capture APIs wrapped in a unified interface.
- Each sensor type writes to a lock‑free ring buffer in shared memory (e.g., using `mmap` or a POSIX shared memory object).
- Buffers are sized to hold 60 seconds of data.

**Preprocessing:**
- Frames are normalized to [0,1] and optionally encoded to latent vectors by a lightweight encoder if storage is a concern.
- Audio is converted to MFCCs (13 coefficients, 10 ms windows).
- Events are timestamped and serialized as protocol buffers.

### 4.2 Agent Swarm

**Agent Data Structure:**
```python
@dataclass
class Agent:
    agent_id: str
    agent_type: str  # "vision", "audio", "text", "intent", "context", "safety"
    model_path: str  # path to ONNX/TFLite model
    input_topics: List[str]   # sensor topics to subscribe to
    output_topic: str         # where proposals are written
    state: str  # "active", "idle", "hibernated"
    last_activation: float
    confidence_threshold: float
    temperature_preference: float
```

**Agent Lifecycle Management:**
- **Hibernated → Loading:** Triggered by a request from the Plinko layer or a higher‑level agent. Model is loaded into memory (may take 100–500 ms).
- **Loading → Active:** Model ready; agent begins reading its input topics and writing proposals.
- **Active → Idle:** No activity for `idle_timeout` (default 30 s). Agent stops polling but stays in memory.
- **Idle → Hibernated:** No activity for `hibernate_timeout` (default 5 min). Model unloaded, metadata preserved.
- **Predictive wake‑up:** The Training Scheduler may wake an agent based on time‑of‑day patterns.

**Communication:**
- All agents read from and write to shared memory using lock‑free queues.
- Proposals are serialized in a compact binary format (Cap’n Proto schema, see Appendix A).

**Dynamic Recruitment:**
When the Plinko layer encounters high uncertainty (entropy above threshold), it may request new agents. A recruitment service scans the Model Zoo for agents whose specialization embedding is similar to the current situation embedding (cosine similarity >0.7). If none exist, it may spawn a temporary “helper” agent by cloning a base model and fine‑tuning on recent logs.

### 4.3 Plinko Decision Layer

**Input:** Set of proposals from all agents in the current time window (typically 16 ms). Each proposal contains:
- `agent_id`
- `action_type` (e.g., “click”, “type”, “scroll”)
- `target` (e.g., element ID, coordinates)
- `confidence` (float 0–1)
- `features` (embedding vector of the input that led to this proposal)

**Step 1: Discriminator Pass**
Each proposal is passed through a set of discriminators. Each discriminator is a lightweight binary classifier (e.g., logistic regression or 2‑layer MLP) that outputs a probability in [0,1] that the action is acceptable.
- **Safety discriminator:** trained on human‑labeled harmful actions.
- **Coherence discriminator:** trained to distinguish actions that led to user corrections vs. those that didn’t.
- **Timing discriminator:** prevents rapid‑fire repeated actions.

The final acceptance probability for proposal *i* is:
\[
p_i^{\text{disc}} = \prod_{j} d_{ij}
\]

**Step 2: Score Computation**
\[
s_i = \log(\text{confidence}_i) + \log(p_i^{\text{disc}}) + \epsilon_i \cdot \tau
\]
where \(\epsilon_i\) is Gumbel noise drawn from \(-\log(-\log(U(0,1)))\) and \(\tau\) is temperature.

**Step 3: Selection**
\[
\pi_i = \frac{\exp(s_i / \tau)}{\sum_k \exp(s_k / \tau)}
\]
The action is sampled from this categorical distribution.

**Adaptive Temperature:**
Temperature \(\tau\) is adjusted based on the entropy of the proposal distribution:
\[
\tau = \tau_{\text{base}} \cdot (1 + \alpha \cdot H)
\]
where \(H = -\sum_i \pi_i \log(\pi_i + \epsilon)\) is the entropy, and \(\alpha\) is a scaling factor (e.g., 0.5). This increases exploration when the system is uncertain.

**Output:** The selected proposal is sent to the Action Executors.

### 4.4 Action Executors

**A2UI (Agent‑to‑UI):** Unified interface to platform accessibility APIs.
- **Android:** UIAutomator
- **iOS/macOS:** AXUI
- **Windows:** UI Automation
- **Linux:** AT‑SPI

Each executor runs in a sandboxed process with minimal permissions.

**API Executor:** Makes HTTP requests with OAuth handling. Credentials are stored encrypted.

**File Executor:** Read/write files within user‑specified directories. Tracks undo information.

**Physical Executor:** For robotics, interfaces via ROS2 or MQTT.

**Outcome Logging:** Every execution logs success/failure, latency, and (if available) before/after state.

### 4.5 Experience Logger

**Log Format (Parquet schema):**
```
timestamp: int64
session_id: binary
sensor_data: {
    frames: list<binary> (optional, compressed)
    audio: binary (optional)
    events: list<Event>
}
proposals: list<Proposal>
selected_action: Proposal
discriminator_scores: list<float>
temperature: float
outcome: {
    success: bool
    latency_ms: int32
    user_feedback: int8 ( -1=bad, 0=none, 1=good )
}
system_state: {
    battery: float
    cpu: float
    memory: float
}
```

**Compression:** Sensor frames are optionally encoded to latent vectors using the world model’s encoder, reducing storage by ~90%. The latent vectors are stored instead of raw frames.

**Circular Buffer:** Logs are kept for 30 days by default, oldest deleted first.

### 4.6 Skill Chunker

**Input:** Sequences of logged actions (e.g., `[open_app, scroll, click, type, send]`). Each action is represented by its type and target embedding.

**Step 1: Frequent Subsequence Mining**  
Use PrefixSpan or a similar algorithm to find sequences that occur above a threshold (e.g., 5 times). These are candidate skills.

**Step 2: Temporal Autoencoder**  
Train a sequence autoencoder on the candidate sequences. The encoder compresses the sequence into a latent vector (the seed). The decoder reconstructs the sequence. The autoencoder is trained with reconstruction loss.

**Step 3: MDL‑Based Boundary Detection**  
For each candidate, compute the description length: `L(chunk) = L(model) + L(data|model)`. Chunks that minimize total description length are kept. This automatically determines hierarchical boundaries (e.g., `check_email` might contain `open_app` and `scroll` as sub‑skills).

**Skill Storage:**
```json
{
  "skill_id": "skill_email_check_v3",
  "type": "rnn",
  "weights": [binary data],
  "latent_dim": 64,
  "input_dim": 32,
  "output_dim": 32,
  "version": 3,
  "parent_id": null,
  "children": ["skill_open_app_v2", "skill_scroll_v1"]
}
```

### 4.7 World Model

**Architecture:**
- **Encoder:** 2‑layer MLP with VAE (outputs mean and logvar). Input: observation vector (e.g., 128‑dim after preprocessing). Latent dim: 64.
- **Transition Model:** GRU with hidden state 64. Input: concatenated latent state and action embedding (16‑dim). Output: next latent state.
- **Reward Model:** 2‑layer MLP from latent state to scalar reward (predicts user satisfaction).
- **Decoder:** 2‑layer MLP from latent state to reconstructed observation (optional, for visualization).

**Training:**
- Data: (obs_t, action, obs_{t+1}, reward) from logs.
- Loss: reconstruction loss (if decoder used) + KL divergence + prediction loss for next latent + MSE for reward.
- Optimizer: Adam, learning rate 1e-4.

**Counterfactual Augmentation:**  
During training, generate synthetic transitions by swapping actions in similar contexts, improving generalization to unseen actions.

### 4.8 Dreaming Engine

**Purpose:** Improve skills by simulating variations in the world model.

**Multi‑Scale Dreaming:**
- **Micro‑dreams:** Perturb low‑level parameters (e.g., timing, pressure). Horizon: 10–100 steps. Used for motor skill refinement.
- **Meso‑dreams:** Vary sequence order or insert pauses. Horizon: 100–1000 steps. Used for routine optimization.
- **Macro‑dreams:** Recombine skills (e.g., merge “check email” and “check calendar”). Horizon: 1000–10000 steps. Used for strategic planning.

**Dreaming Algorithm:**
```python
def dream(skill_id, scale='meso', num_simulations=1000):
    skill = load_skill(skill_id)
    world = load_world_model()
    best_reward = -inf
    best_variation = None
    for _ in range(num_simulations):
        var = skill.mutate(scale)   # returns a modified skill
        state = sample_initial_state()
        total = 0
        for step in range(horizon(scale)):
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

**Mutation Operators:**
- **Micro:** add Gaussian noise to action parameters.
- **Meso:** swap two adjacent actions, insert delay, delete redundant action.
- **Macro:** replace a sub‑sequence with another skill, concatenate skills.

### 4.9 Training Scheduler

**Purpose:** Orchestrate nightly learning tasks.

**Input:** Day’s logs, current model zoo, user preferences (e.g., budget for cloud).

**Task Prioritization:**  
For each candidate task (skill chunking, world model update, skill dreaming, model fine‑tuning), compute:
\[
ROI = \frac{\text{expected\_improvement} \times \text{frequency}}{\text{estimated\_cost}}
\]
- expected_improvement: estimated from recent performance trends.
- frequency: how often the skill/agent is used.
- cost: estimated GPU hours.

**Local vs. Cloud:**  
If `cost > local_budget` and user has enabled cloud, offload to LucidDreamer.ai (or compatible service). Otherwise, run locally.

**Predictive Wake‑Up:**  
Based on historical usage, predict when the user will next use the device. Schedule training to finish 5 minutes before that time.

### 4.10 Memory & Databases

**Long‑Term Memory:** Agents can store and retrieve experiences using a vector database. Each memory entry consists of:
- `embedding`: vector from world model encoder
- `metadata`: JSON (e.g., app, time, outcome)
- `timestamp`

**Retrieval:** Agents issue queries with a current state embedding; database returns top‑k most similar past experiences.

**Implementation:** ChromaDB or LanceDB, running locally. Optional cloud sync (encrypted) for cross‑device memory.

### 4.11 Seed Serialization

**Seed Format:**  
A seed is a JSON object containing:
```json
{
  "seed_id": "uuid",
  "skill_id": "skill_email_check_v3",
  "agent_chain": ["intent_agent", "vision_agent", "text_agent"],
  "parameters": {
    "app": "gmail",
    "target": "inbox"
  },
  "latent": [0.12, -0.34, ...],  // 64 floats
  "version": 3,
  "signature": "rsa:..."  // optional, for authenticity
}
```

**Export/Import:** Seeds can be exported as a compact binary (message pack) or base64‑encoded string for sharing.

---

## 5. Data Flows

### 5.1 Daytime Inference Loop
1. Sensors write data to shared memory ring buffers.
2. Each active agent reads its subscribed topics every `poll_interval` (e.g., 16 ms for vision, 100 ms for intent).
3. Agent runs inference, produces a proposal, and writes it to its output topic.
4. Every `decision_interval` (e.g., 33 ms), the Plinko layer collects all proposals written since last interval.
5. Plinko computes scores and selects an action.
6. Action is dispatched to appropriate executor.
7. Executor performs action and logs outcome.
8. Experience logger records all data (compressed).

### 5.2 Nightly Training Cycle
1. At scheduled time (user idle, device charging), Training Scheduler wakes.
2. Reads logs from circular buffer.
3. Computes ROI for all pending tasks.
4. For each task (in priority order):
   - If local, spawn training process.
   - If cloud, package anonymized data and call LucidDreamer API.
5. After tasks complete, validate new models on held‑out recent data.
6. Deploy improved models/skills to Model Zoo (atomic swap).
7. Update performance metrics.

### 5.3 Seed Sharing
1. User A’s Mycelium exports a seed for a skill (e.g., custom calendar routine).
2. Seed is shared via any medium (file, link, QR code).
3. User B imports seed into their Mycelium.
4. Mycelium verifies compatibility (agent versions, etc.) and instantiates the skill.
5. Skill is available for use without any training or data exposure.

---

## 6. APIs and Interfaces

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
Tools to convert PyTorch/TensorFlow models to the required format (ONNX, quantized). Includes a simulator to test agents in a controlled environment.

### 6.3 Seed API
- `POST /seed/export` – get a seed for a skill.
- `POST /seed/import` – instantiate a seed.
- `GET /seed/verify` – check compatibility.

---

## 7. Implementation Roadmap

**Phase 1: Prototype (0–3 months)**
- Implement core agent runtime with shared memory.
- Basic Plinko layer (random noise, no discriminators).
- Simple skill chunking (PrefixSpan).
- Local logging to files.
- Command‑line interface.

**Phase 2: On‑Device Learning (4–9 months)**
- Add discriminators and adaptive temperature.
- Implement world model trainer.
- Basic dreaming (micro only).
- Training scheduler with local execution.
- A2UI for one platform (Android).

**Phase 3: Advanced Features (10–15 months)**
- Multi‑scale dreaming.
- Hierarchical skill chunking with MDL.
- Vector database integration.
- Seed serialization and sharing.
- Cloud integration (LucidDreamer client).

**Phase 4: Ecosystem (16–24 months)**
- Cross‑platform A2UI (iOS, Windows, Linux).
- Federated learning (opt‑in).
- Skill marketplace.
- Hardware acceleration for common agents.

---

## 8. Appendices

### Appendix A: Cap’n Proto Schema for Proposals
```capnp
@0x8a1b4c3d5e6f7890;

struct Proposal {
    agentId @0 :Text;
    timestamp @1 :Float64;
    actionType @2 :ActionType;
    enum ActionType {
        click @0;
        type @1;
        scroll @2;
        apiCall @3;
        fileOp @4;
        skillInvoke @5;
        noop @6;
    }
    confidence @3 :Float32;
    target @4 :Target;
    struct Target {
        union {
            element @0 :Text;
            coordinates @1 :List(Float32, 2);
            url @2 :Text;
            filePath @3 :Text;
            skillId @4 :Text;
        }
    }
    features @5 :List(Float32);
}
```

### Appendix B: World Model Training Pseudocode
```python
for epoch in range(10):
    for batch in dataloader(logs):
        obs, action, next_obs, reward = batch
        z, mean, logvar = world.encode(obs)
        next_z = world.transition(z, action)
        pred_reward = world.reward(next_z)
        loss = (
            mse_loss(next_z, world.encode(next_obs)[0]) +
            mse_loss(pred_reward, reward) +
            kl_loss(mean, logvar)
        )
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
```

### Appendix C: Glossary
- **Seed:** A compressed vector that encodes a specific behavior.
- **Skill:** A stored, reusable behavior (may consist of sub‑skills).
- **Plinko:** Stochastic decision layer.
- **A2UI:** Agent‑to‑UI, the module that performs UI automation.
- **World Model:** Predictive model of environment dynamics.
- **Dreaming:** Offline simulation to improve skills.

---

*This document is a living specification. For the latest version, source code, and contribution guidelines, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
