# Mycelium Architecture Outline: Research-Annotated Specification

## Purpose
This outline synthesizes two existing architecture documents with current research to create a complete, implementable specification. Each section is annotated with research findings, gaps, and cross-references to relevant work.

---

## 1. Introduction & Philosophy

### Core Thesis
Mycelium enables a shift from code-defined to demonstration-defined software. Behaviors are captured as **seeds**—compact vectors that, when combined with prompts, deterministically reproduce actions across any compatible agent swarm.

### Research Anchors
| Concept | Supporting Research | Gap/Note |
|---------|---------------------|----------|
| Demonstration learning | SkillRL (arXiv 2026): recursive skill evolution outperforms monolithic models | Seed compression specifics not addressed |
| Decentralized agent collaboration | NeuroMesh (Devpost 2025): self-healing distributed AI swarm with coordinator/edge nodes  | Validates swarm approach; lacks seed concept |
| Bio-inspired distribution | Mycelial_Net (Minerals 2025): fungal networks as model for distributed intelligence  | Theoretical framework, not implementation |

### Key Distinctions from v1
- **Seed as first-class artifact** (stronger emphasis than v1)
- **Prompt + seed = deterministic behavior** (clarifies relationship)
- **Code becomes optional**—used only for proof/rigor, not function

---

## 2. System Overview

### High-Level Architecture (Synthesized)

```
[Sensors] → [Sensor Layer] → [Shared Memory] → [Agent Swarm] → [Plinko Layer] → [Action Executors]
    ↑              ↑              ↑                  ↑                ↑                ↓
    └── [Memory] ←─┴── [Seed Engine] ←── [Experience Logger] ←─── [Outcome] ───────┘
                           ↓
                    [Skill Chunker] ←── [World Model] ←── [Dreaming Engine]
                           ↓
                    [Training Scheduler] → [Model Zoo] ←── [Seed Exchange]
```

### Research Validation

| Component Cluster | Supporting Work | Notes |
|-------------------|-----------------|-------|
| Agent swarm + shared memory | NeuroMesh: asyncio + WebSocket mesh networking  | Real-time peer-to-peer validated |
| Federated learning layer | MyceliumWebServer: ActivityPub + SPORE protocol  | MIT-licensed reference implementation |
| Multi-agent coordination | AICUBE: 73 agents, 100% knowledge reuse, sub-50ms latency  | Commercial validation of scale |

### Research Gap: Seed Exchange Protocol
While MyceliumWebServer demonstrates ActivityPub-based agent communication , no existing work specifies a seed serialization format or exchange protocol. This is an original contribution area.

---

## 3. Core Data Structures

### 3.1 Seed Format (Synthesized)

```python
@dataclass
class Seed:
    seed_id: UUID
    skill_id: Optional[str]          # if derived from a named skill
    agent_chain: List[str]            # which agent types this works with
    base_model_hashes: Dict[str, str] # per agent, which base model version
    embedding: bytes                   # float32 vector (64-1024 dim)
    parameters: Dict[str, Any]         # prompt parameters
    metadata: {
        created_at: timestamp
        usage_count: int
        avg_success: float
        signature: Optional[bytes]     # for authenticity
    }
```

### 3.2 Proposal Format (from v1, validated)

```capnp
struct Proposal {
    agentId @0 :Text;
    timestamp @1 :Float64;
    actionType @2 :ActionType;
    confidence @3 :Float32;
    target @4 :Target;
    features @5 :List(Float32);   # embedding for discriminators
}
```

### 3.3 Agent Data Structure (Synthesized)

| Field | v1 | v2 | Research Basis |
|-------|----|----|----------------|
| agent_id | ✅ | ✅ | Standard |
| agent_type | ✅ | ✅ | NeuroMesh: coordinator vs edge roles  |
| model_path | ✅ | ✅ | - |
| input_topics | ✅ | ✅ | MyceliumWebServer: SPORE topics  |
| output_topic | ✅ | ✅ | - |
| specialization_embedding | ❌ | ✅ | SkillRL: skill similarity matching |
| temperature_pref | ✅ | ✅ | Plinko adaptive temp |
| peer_connections | ❌ | ✅ | NeuroMesh: self-healing network  |

### Research Gap: Agent Specialization Embedding
No existing work defines how to generate or match specialization embeddings. This requires original development.

---

## 4. Component Specifications

### 4.1 Sensor Layer

**Implementation (from v1):**
- Platform-specific capture APIs
- Lock-free ring buffers in shared memory
- Speculative pre-processing

**Research Support:**
- Microfluidic mycelium studies  demonstrate importance of multi-scale observation—validates need for diverse sensor inputs

**Enhancements from v2:**
- Explicit latent encoding for storage efficiency
- Clearer spec on buffer sizes and data types

### 4.2 Agent Swarm

#### 4.2.1 Agent Lifecycle (Synthesized)

| State | v1 | v2 | Notes |
|-------|----|----|-------|
| HIBERNATED | ✅ | ✅ | - |
| LOADING | ✅ | ✅ | - |
| ACTIVE | ✅ | ✅ | - |
| IDLE | ✅ | ✅ | - |
| DEGRADED | ❌ | ✅ | NeuroMesh: graceful degradation at 50% node failure  |

**Research Support for DEGRADED state:**
NeuroMesh demonstrated networks with 50% node failures continued operating at 80% capacity . This requires explicit degraded modes where agents provide reduced but functional service.

#### 4.2.2 Dynamic Recruitment (Enhanced)

v1 algorithm + v2 similarity matching + research validation:

```python
def recruit_agents(situation_embedding, required_capability):
    # Phase 1: Check active agents
    for agent in active_agents:
        if cosine_similarity(situation_embedding, agent.specialization) > THRESHOLD:
            candidates.append(agent)
    
    # Phase 2: Check hibernated agents
    # Phase 3: Spawn helper if needed
    # Phase 4: Consider peer recommendations (new from NeuroMesh)
    peer_recommendations = get_peer_recommendations(situation_embedding)
```

**Research Basis:**
- AICUBE: 73 agents broadcasting discoveries  validates peer recommendations
- NeuroMesh: hierarchical coordination  validates coordinator/edge distinction

### 4.3 Plinko Decision Layer (Mathematically Complete)

#### Mathematical Formulation (v1 + v2 synthesis)

**Step 1: Discriminator Pass**
```
p_disc = Π d_j(proposal_features)   # j discriminators
```

**Step 2: Raw Score**
```
s = log(confidence) + log(p_disc)
```

**Step 3: Gumbel Noise**
```
ε = -log(-log(U(0,1)))
final = s + ε·τ
```

**Step 4: Selection Probability**
```
π_i = exp(final_i / τ) / Σ exp(final_k / τ)
```

**Step 5: Adaptive Temperature**
```
τ = τ_base · (1 + α·H)
H = -Σ π_i log(π_i + ε)  # entropy
```

#### Discriminator Types

| Discriminator | Training Data | Research Basis |
|---------------|---------------|----------------|
| Safety | Human-labeled harmful actions | Standard RLHF approach |
| Coherence | User corrections vs. accepted | SkillRL: outcome prediction |
| Timing | Rapid-fire detection | Heuristic + learned |
| Privacy | PII detection rules | Regulatory requirement |

#### Research Validation for Stochastic Selection

| Aspect | Supporting Work | Notes |
|--------|-----------------|-------|
| Gumbel-Softmax | Standard in RL | - |
| Adaptive temperature | SkillRL: dynamic exploration | Implemented |
| Multi-discriminator | NeuroMesh: harmony protocol extensions  | Communication-layer validation |

### 4.4 Seed Engine (New in v2, Requires Original Work)

#### 4.4.1 Seed Capture

**Input:** Sequence of (observation_latent, action) pairs from demonstration
**Output:** Seed embedding

**Proposed Architecture:**
```python
class SeedEncoder(nn.Module):
    def __init__(self, obs_dim, action_dim, latent_dim=256):
        self.obs_encoder = nn.Linear(obs_dim, 128)
        self.action_encoder = nn.Linear(action_dim, 128)
        self.lstm = nn.LSTM(256, 256, batch_first=True)
        self.latent_proj = nn.Linear(256, latent_dim)
    
    def forward(self, obs_seq, action_seq):
        # Encode each timestep
        obs_encoded = self.obs_encoder(obs_seq)
        action_encoded = self.action_encoder(action_seq)
        combined = torch.cat([obs_encoded, action_encoded], dim=-1)
        
        # LSTM over sequence
        _, (hidden, _) = self.lstm(combined)
        
        # Project to seed
        seed = self.latent_proj(hidden[-1])
        return seed
```

**Training:** Autoencoder reconstruction loss + contrastive loss to separate different behaviors.

#### 4.4.2 Seed Replay

**Process:**
1. Load seed into target agent (concatenate to agent's internal state)
2. Agent acts conditioned on seed + current observations
3. Deterministic inference (temperature = 0) ensures reproducibility

**Research Gap:** No existing work defines seed conditioning mechanism. Options:
- Feature-wise Linear Modulation (FiLM)
- Additional input to agent's LSTM
- Latent concatenation

### 4.5 Skill Chunker (Synthesized)

#### Algorithm (v1 PrefixSpan + v2 temporal autoencoder + MDL)

**Step 1: Frequent Subsequence Mining**
- PrefixSpan or equivalent
- Threshold: minimum occurrences (e.g., 5)

**Step 2: Temporal Autoencoder**
```python
class SkillAutoencoder(nn.Module):
    # Encodes action sequences to skill embeddings
    # Decodes back to sequences
    # Training: reconstruction loss
```

**Step 3: MDL Boundary Detection**
```
cost(chunk) = model_cost + data_cost
model_cost = parameters to store chunk as skill
data_cost = reconstruction error
```
Minimize total cost over sequence to find optimal chunk boundaries.

**Step 4: Hierarchical Composition**
- Skills can contain sub-skills (detected via recursive MDL)
- Stored as DAG in Model Zoo

#### Research Support

| Technique | Supporting Work | Notes |
|-----------|-----------------|-------|
| Sequence mining | Standard | - |
| Temporal autoencoder | SkillRL: recursive evolution | Validated approach |
| MDL | Information theory | Theoretically sound |
| Hierarchy | AutoSkill: hierarchical open-ended acquisition [citation from v1 refs] | Robotic validation |

### 4.6 World Model (Architecture Complete)

#### Components (from v1 + v2)

| Component | Input | Output | Architecture |
|-----------|-------|--------|--------------|
| Encoder | observation | latent (z) | VAE (MLP) |
| Transition | (z, action) | next_z | GRU |
| Reward | next_z | scalar | MLP |
| Decoder | z | reconstructed obs | MLP (optional) |

#### Training (from v2 pseudocode)

```python
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
    optimizer.step()
```

#### Counterfactual Augmentation (v2)
Generate synthetic transitions by swapping actions in similar contexts.

#### Research Validation

| Aspect | Supporting Work | Notes |
|--------|-----------------|-------|
| VAE + GRU architecture | GW-Dreamer (arXiv 2025) | Validated for dreaming |
| Counterfactual augmentation | Standard data augmentation | - |
| Reward prediction | SkillRL: outcome prediction | Validated |

### 4.7 Dreaming Engine (Enhanced)

#### Multi-Scale Dreaming (from v2)

| Scale | Horizon | Purpose | Mutation Operators |
|-------|---------|---------|-------------------|
| Micro | 10-100 steps | Motor refinement | Gaussian noise on actions |
| Meso | 100-1000 steps | Routine optimization | Swap, insert, delete |
| Macro | 1000-10000 steps | Strategic planning | Recombine skills |

#### Algorithm (v2 + research)

```python
def dream(skill_id, scale='meso', num_simulations=1000):
    skill = load_skill(skill_id)
    world = load_world_model()
    best_reward = -inf
    best_variation = None
    
    for _ in range(num_simulations):
        var = mutate(skill, scale)  # scale-specific operators
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

#### Research Validation

| Aspect | Supporting Work | Notes |
|--------|-----------------|-------|
| Dreaming reduces real interactions | Neuromorphic dreaming (arXiv 2024) | Foundational |
| Multi-scale | Biological sleep stages | Theoretical |
| Latent-space dreaming | GW-Dreamer | Validated |

### 4.8 Training Scheduler (Synthesized)

#### ROI Calculation (v2)
```
ROI = (expected_improvement × frequency) / estimated_cost
```

#### Local vs. Cloud Decision (v1 + v2)

| Task Type | Typical Duration | Default Location | Research Basis |
|-----------|------------------|------------------|----------------|
| LoRA fine-tune | 5-30 min | Local | - |
| Skill chunking | 10-60 min | Local | - |
| World model update | 20-120 min | Local | - |
| Distillation | 1-8 hours | Cloud | NeuroMesh: edge vs coordinator  |
| Federated averaging | Variable | Cloud | MyceliumWebServer: ActivityPub-based  |

#### Predictive Wake-Up (v2)
- Analyze usage patterns
- Predict next active period
- Schedule completion 5 minutes before

### 4.9 Model Zoo (Complete)

#### Storage Structure (from v2)
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

#### Metadata Schema (from v2)
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

#### Automatic Rollback (v2)
Monitor new model performance for 24h; revert if below previous version.

### 4.10 Memory (Vector Database)

#### Implementation Options
- **ChromaDB**: Local, lightweight
- **LanceDB**: Columnar, efficient
- **Redis**: If already using (from GMV mycelium)

#### Schema
```
Collection: memories
- embedding: float[] (from world model encoder)
- metadata: {
    timestamp: int,
    app: str,
    action: str,
    outcome: str,
    user_feedback: int
}
- raw_data: optional (for debugging)
```

#### Query Pattern
```python
def retrieve_similar(current_obs, k=5):
    obs_embedding = world_model.encode(current_obs)
    results = memory.query(
        embedding=obs_embedding,
        n_results=k,
        where={"outcome": "success"}  # optional filter
    )
    return results
```

---

## 5. Protocols

### 5.1 SPORE Protocol (from MyceliumWebServer)

**Reference Implementation:** 

```json
{
  "protocol": "spore/v1",
  "sender": "agent_vision_3f7a",
  "recipient": "agent_swarm",
  "message_id": "msg_9k2m4n",
  "content": {
    "type": "proposal",
    "action": {...},
    "context": {...}
  }
}
```

### 5.2 Agent Discovery (from v2)

```
ANNOUNCE:
  agent_id: vision_ui_2b
  capabilities: [ui_detection, ocr]
  models: [mobilenet_v3]

ACKNOWLEDGE:
  assigned_id: agent_47
  input_topic: /sensors/vision
  output_topic: /proposals/vision

HEARTBEAT:
  agent_id: agent_47
  status: active
  load: 0.3
```

### 5.3 Seed Exchange Protocol (Original Contribution)

**Proposed Format:**
```
POST /seed/export
{
  "skill_id": "skill_email_check_v3",
  "format": "binary"  # or "base64"
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
  "verify": true  # check compatibility
}

Response:
{
  "success": true,
  "skill_id": "imported_skill_uuid",
  "warnings": []  # if compatibility issues
}
```

### 5.4 Harmony Protocol Extension (from NeuroMesh)

**Reference:**  describes extended Harmony protocol for mesh communication with routing guarantees.

**Relevant Features:**
- Message versioning
- Compatibility handling
- Intelligent routing algorithms
- Delivery guarantees

---

## 6. Implementation Procedures

### 6.1 Building a Minimal Agent (from v1)

```python
from mycelium import Agent

agent = Agent(
    model_path="mobilenet_v3_int8.onnx",
    input_topics=["/sensors/camera"],
    output_topic="/proposals/vision",
    agent_type="vision"
)
swarm.add_agent(agent)
```

### 6.2 Capturing a Seed (from v2)

```python
def capture_seed(start_trigger, stop_trigger):
    actions = []
    observations = []
    
    while not stop_trigger:
        obs = get_current_sensor_latent()
        action = plinko.selected_action  # or user override
        actions.append(action)
        observations.append(obs)
    
    seed = seed_encoder.encode(actions, observations)
    save_seed(seed)
```

### 6.3 Replaying a Seed (from v2)

```python
def replay_seed(seed_id, prompt):
    agent = load_agent_for_seed(seed_id)
    agent.set_seed(seed_id)  # conditioning mechanism
    
    while task_not_complete:
        obs = get_current_sensor_latent()
        action = agent.act(obs, prompt)
        executor.execute(action)
```

### 6.4 Chaining Seeds (from v2)

Workflow = directed graph of seeds. Meta-agent decides next seed based on current state.

### 6.5 Training World Model (from v2)

See Section 4.6 pseudocode.

### 6.6 Running Dreaming Engine (from v2)

See Section 4.7 pseudocode.

### 6.7 Integrating Memory (from v2)

```python
# During inference
similar = memory.retrieve_similar(current_obs)
context = augment_with_similar(similar)

# During logging
memory.store(obs_embedding, {
    "action": action,
    "outcome": outcome,
    "timestamp": now()
})
```

---

## 7. Example Workflows (Enhanced)

### 7.1 Personal Automation: Email Triage (from v2)

1. User: "watch me handle email"
2. Capture sequence: open app → sort → reply to boss → archive
3. Seed created
4. Next day: "do email" → replay with adaptation to today's inbox

### 7.2 Simulation-First Development (from v2)

1. Developer describes app in natural language
2. Mycelium spawns simulation using world model
3. Developer interacts, gives corrections
4. After refinement, export seed or generate code

### 7.3 Sharing a Seed (from v2)

1. Alice captures skill
2. Exports seed file
3. Bob imports → new skill, no data exposure

### 7.4 Self-Healing Swarm (New from NeuroMesh)

**Scenario:** Network with 10 agents loses 5 nodes
**Expected behavior:**
- Remaining nodes detect failures via heartbeat timeout
- Workload redistributed automatically
- System continues at reduced but functional capacity
- When nodes reconnect, network heals

**Implementation requirements:**
- Heartbeat monitoring (from v2)
- Graceful degradation states (new)
- Work redistribution logic

### 7.5 Federated Skill Learning (New from MyceliumWebServer)

**Scenario:** Multiple users opt to share anonymized skill improvements
**Process:**
1. Each instance logs skill usage and outcomes
2. Periodically, instances exchange updates via ActivityPub
3. Global model improves without central data collection
4. Individual instances retain personalization layers

---

## 8. Research Gaps Summary

| Area | Current State | Needed Work | Priority |
|------|---------------|-------------|----------|
| **Seed encoding** | Conceptual only | Architecture and training procedure | High |
| **Seed conditioning** | Not specified | Mechanism for injecting seed into agent | High |
| **Specialization embeddings** | Not specified | Generation and matching algorithms | Medium |
| **Seed exchange protocol** | Not specified | API design, serialization, compatibility | Medium |
| **Graceful degradation** | Mentioned but not specified | State definitions, transition logic | Low |
| **Multi-scale dreaming operators** | Listed but not defined | Precise mutation algorithms | Medium |
| **Peer recommendations** | Concept from NeuroMesh | Protocol and trust mechanism | Low |

---

## 9. References

### Academic Papers
1. SkillRL (arXiv 2026) - Recursive skill-augmented reinforcement learning
2. GW-Dreamer (arXiv 2025) - Global workspace + world model dreaming
3. Neuromorphic dreaming (arXiv 2024) - Dreaming reduces real interactions
4. AutoSkill (IEEE TCDS 2025) - Hierarchical skill acquisition
5. Mycelial_Net (Minerals 2025) - Bio-inspired distributed AI 

### Open Source Implementations
6. MyceliumWebServer - ActivityPub-based federated learning 
7. NeuroMesh - Self-healing distributed AI swarm 
8. GMV mycelium - Redis-based agent communication

### Industry Research
9. AICUBE TECHNOLOGY - 73-agent network, 100% knowledge reuse 

### Foundational Biology
10. Microfluidic mycelium studies - Multi-scale observation importance 
11. Living mycelium architecture - Self-healing, growth-based systems 

---

*This outline is a living document. For the latest version, visit [github.com/superinstance/mycelium](https://github.com/superinstance/mycelium).*
