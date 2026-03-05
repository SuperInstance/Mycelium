# Mycelium Architecture Specification: Research-Annotated & Gap-Analyzed

**Version 3.0 — April 2026**  
**SuperInstance Open Source Initiative**

---

## Preface: How to Read This Document

This specification synthesizes multiple architecture versions with rigorous research validation. Each section contains:

- **Specification:** What the component does and how it works
- **Research Alignment:** Published work that supports or extends this design
- **Gap Analysis:** What's missing, unproven, or requires original work
- **Authority Assessment:** Credibility of referenced sources
- **Implementation Readiness:** Whether the component can be built today or requires research

The goal is to provide a complete blueprint while being transparent about what's proven, what's plausible, and what's speculative.

---

## Part I: Foundation and Context

### 1. Introduction

#### 1.1 The Problem with Static Intelligence

**Specification:**
Traditional AI systems are trained once and deployed as static models. They cannot learn from individual users, adapt to changing behavior, or improve after deployment. Cloud dependency creates latency, privacy risks, and single points of failure.

**Research Alignment:**
| Source | Finding | Authority |
|--------|---------|-----------|
| Bio Cognitive Mesh (IEEE 2025)  | Centralized AI has 78× higher latency, 83× more bandwidth than edge-swarm alternatives | High (peer-reviewed) |
| SMARTEDGE Project (EU)  | Identifies edge-cloud continuum as critical for next-gen AI applications | High (EU-funded research consortium) |
| Electronics Letters CFP  | Edge AI requires adaptability, robustness, real-time decision-making | High (peer-reviewed venue) |

**Gap Analysis:** Well-established problem. No significant gaps.

**Implementation Readiness:** ✅ Ready (problem definition only)

#### 1.2 A New Paradigm: Demonstration-Driven Development

**Specification:**
Mycelium enables software where behavior is defined by demonstration, not code. Developers show what they want once; the system captures it as a seed. Later, a prompt plus that seed reproduces the exact behavior. Code becomes optional—used only when mathematical proof or formal verification is required.

**Research Alignment:**
| Source | Finding | Authority |
|--------|---------|-----------|
| SMARTEDGE Project  | "Low-code programming environment" and "human-in-the-loop automation" validate demonstration-driven approach | High |
| Seed AI (Wikipedia)  | "Seed improver" architecture for recursive self-improvement provides conceptual foundation | Medium (cites primary sources) |
| SkillRL (arXiv 2026)  | Recursive skill evolution outperforms monolithic models | Medium (preprint) |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Seed compression validation | 🔴 Critical | No research shows full behaviors compress to single vectors |
| Code replacement claim | 🟠 High | SMARTEDGE validates low-code, not "code optional" |
| Deterministic reproduction | 🔴 Critical | No precedent for exact behavior replay from seeds |

**Implementation Readiness:** ⚠️ Requires original research

#### 1.3 Core Thesis: Behavior as Primary Artifact

**Specification:**
The fundamental unit of software becomes behavior, captured as seeds. Code is a secondary artifact—an implementation detail for when formal verification matters. For most applications, seeds + prompts are sufficient, faster, and more adaptable.

**Research Alignment:** No direct research supports this thesis. It is a synthesis of:
- Low-code programming trends (SMARTEDGE)
- Skill-based learning (SkillRL)
- Recursive self-improvement (Seed AI)

**Gap Analysis:** This is the central hypothesis of Mycelium. It requires extensive empirical validation.

**Implementation Readiness:** ⚠️ Hypothesis stage

---

### 2. Core Concepts

| Concept | Specification | Research Alignment | Gap |
|---------|---------------|-------------------|-----|
| **Agents** | Tiny specialized neural models (1-100M params) | Edge AI architectures (Electronics Letters CFP), SMARTEDGE multi-agent swarms | Well-supported |
| **Prompts & Seeds** | Prompt = initial instruction; Seed = compressed behavior vector | Seed AI conceptual; no direct encoding research | 🔴 Critical |
| **Skills** | Reusable behavior primitives | SkillRL, AutoSkill validate skill discovery | 🟠 High (integration novel) |
| **World Models** | Predictive environment models | DreamerV3, GW-Dreamer (implied) | 🟠 High (citations needed) |
| **Dreaming** | Offline simulation for improvement | Neuromorphic dreaming (arXiv 2024) | 🟠 High (scale novelty) |
| **Memory** | Vector DB for long-term recall | EngramNCA (private memory channels) | 🟢 Medium (implementation) |
| **Plinko Layer** | Stochastic multi-agent decision | No direct research | 🟠 High (novel combination) |
| **A2UI** | Agent-to-UI automation | Accessibility APIs exist | 🟢 Medium (integration) |

**Research Authority Summary:**
- **High:** Peer-reviewed conferences/journals, EU-funded projects
- **Medium:** arXiv preprints, Wikipedia (with citations), industry research
- **Low:** GitHub projects with limited adoption

---

## Part II: System Architecture

### 3. System Overview

**Specification:**
Two-mode operation: Day (inference) and Night (learning). Sensors → Agents → Plinko → Executors → Logger → Nightly learning → Model Zoo.

**Research Alignment:**
| Mode | Source | Finding |
|------|--------|---------|
| Day/Night cycle | Neuromorphic dreaming  | Sleep-like phases reduce required real interactions |
| Edge-cloud interplay | SMARTEDGE  | "Swarm elasticity via Edge-Cloud Interplay" validates hybrid approach |

**Gap Analysis:** Day/night cycle is biologically inspired but not empirically validated for this architecture. The neuromorphic dreaming paper  validates dreaming for training, not for skill refinement.

**Implementation Readiness:** ⚠️ Plausible but needs validation

---

## Part III: Component Deep Dive with Research Gaps

### 4. Sensor Layer

**Specification:**
Platform-specific capture → shared memory ring buffers → speculative pre-processing.

**Research Alignment:**
| Element | Source | Finding |
|---------|--------|---------|
| Shared memory | GMV mycelium  | Redis-based agent communication validates in-memory exchange |
| Multi-scale observation | Mycelial networks research  | Biological precedent for diverse sensor inputs |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Speculative pre-processing | 🟢 Low | Performance optimization; can be evaluated empirically |
| Ring buffer sizing | 🟢 Low | Engineering trade-off |

**Implementation Readiness:** ✅ Ready for implementation

---

### 5. Agent Swarm — RESEARCH GAP ANALYSIS

#### 5.1 Agent Data Structure & Lifecycle

**Specification:**
Agents have states: HIBERNATED, LOADING, ACTIVE, IDLE, DEGRADED. Lifecycle managed by swarm controller.

**Research Alignment:**
| State | Source | Finding |
|-------|--------|---------|
| DEGRADED | NeuroMesh (Devpost 2025)  | 50% node failure → 80% capacity in self-healing swarm |

**Gap Analysis:** DEGRADED state definition and transition logic need specification. NeuroMesh validates concept but doesn't provide implementation.

**Implementation Readiness:** ⚠️ Needs design work

#### 5.2 Dynamic Agent Recruitment

**Specification:**
When uncertainty high, recruit agents via specialization embedding similarity. If none exist, spawn temporary helper.

**Research Alignment:**
| Element | Source | Finding |
|---------|--------|---------|
| Dynamic swarm formation | SMARTEDGE  | "Automatic discovery and dynamic network swarm formation" |
| Peer recommendations | NeuroMesh  | Validates multi-agent coordination |
| Specialization matching | No direct research | - |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Specialization embedding definition | 🔴 Critical | What is it? How computed? |
| Similarity threshold | 🟠 High | No guidance on optimal values |
| Helper agent spawning | 🟠 High | How to create? What architecture? |

**Implementation Readiness:** ⚠️ Requires research

#### 5.3 Communication Protocol

**Specification:** Topics in shared memory, Cap'n Proto serialization.

**Research Alignment:**
| Protocol | Source | Finding |
|----------|--------|---------|
| SPORE | MyceliumWebServer  | ActivityPub-based agent communication |
| Harmony extensions | NeuroMesh  | Routing guarantees, versioning |

**Gap Analysis:** SPORE designed for federated learning, not real-time coordination. Harmony protocol needs adaptation.

**Implementation Readiness:** 🟢 Medium (implementation work)

---

### 6. Seed Capture & Replay Engine — CRITICAL GAP CLUSTER

This is the most novel and least validated component of Mycelium.

#### 6.1 Demonstration Capture

**Specification:**
Record (observation_latent, action) pairs during user demonstration.

**Research Alignment:** Standard imitation learning data collection.

**Gap:** None significant.

#### 6.2 Seed Encoder Architecture

**Specification:**
LSTM encoder → latent vector. Trained with reconstruction + contrastive loss.

**Research Alignment:**
| Technique | Source | Finding |
|-----------|--------|---------|
| Sequence autoencoders | ML literature | Well-established for reconstruction |
| Contrastive learning | ML literature | Well-established for separation |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Behavior encoding capacity | 🔴 Critical | No research on compressing full behaviors to single vectors |
| Sequence length scaling | 🟠 High | Unknown relationship between sequence length and required latent dim |
| Loss weighting | 🟠 High | No guidelines for balancing reconstruction vs. contrastive |

**Research Needed:**
1. Empirical study on benchmark tasks (e.g., Minecraft, ALFRED)
2. Measure reconstruction accuracy vs. latent dimension
3. Test generalization to novel contexts

#### 6.3 Seed Conditioning

**Specification:** "Load seed into agent" via FiLM, concatenation, or separate policy. No implementation specified.

**Research Alignment:**
| Method | Source | Finding |
|--------|--------|---------|
| FiLM | Multimodal ML | Used for conditioning on auxiliary inputs |
| Latent concatenation | Common practice | Simple but may be ignored |
| Separate policy | SkillRL | Validated but not seed-based |

**Gap Analysis:** **CRITICAL GAP.** No research on injecting behavior vectors into agents while preserving base capabilities.

**Research Needed:**
1. Systematic comparison of conditioning methods
2. Measure interference with base agent performance
3. Test robustness to distribution shift

#### 6.4 Determinism Guarantees

**Specification:** Same prompt + seed = same behavior every time.

**Logical Contradiction:** The architecture also claims seeds adapt to environment. Both cannot be true.

**Resolution Needed:** Define hierarchy:
- **Action seeds:** Exact sequence (deterministic, brittle)
- **Policy seeds:** Behavioral policy (adaptive, non-deterministic)

**Research Needed:** Empirical comparison of both approaches.

#### 6.5 Seed Storage Format

**Specification:** Protobuf with metadata.

**Gap:** None significant (implementation detail).

**Overall Seed Engine Readiness:** 🔴 **Requires substantial research before implementation**

---

### 7. Plinko Decision Layer — NOVEL COMBINATION

#### 7.1 Mathematical Formulation

**Specification:**
```
score = log(confidence × Π discriminator_probs) + Gumbel_noise × τ
τ = τ_base × (1 + α × entropy)
```

**Research Alignment:**
| Element | Source | Finding |
|---------|--------|---------|
| Gumbel-Softmax | Jang et al. (2016) | Differentiable sampling |
| Entropy-based adaptation | RL literature | Common for exploration |
| Discriminator ensemble | No direct research | Novel combination |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Discriminator training | 🟠 High | How to train in real-time? Class imbalance? |
| Temperature scaling factor α | 🟢 Low | Can be tuned empirically |
| Multi-discriminator aggregation | 🟢 Low | Product assumption may be suboptimal |

**Implementation Readiness:** ⚠️ Needs experimentation but plausible

---

### 8. Skill Chunker — RESEARCH GAP ANALYSIS

#### 8.1 Sequence Mining

**Specification:** PrefixSpan to find frequent subsequences.

**Research Alignment:** Established algorithm.

**Gap:** None.

#### 8.2 Temporal Autoencoder

**Specification:** Encode sequences to skill embeddings.

**Research Alignment:** Standard technique.

**Gap:** Requires validation on action sequences (vs. sensor data).

#### 8.3 MDL-Based Boundary Detection

**Specification:** Use Minimum Description Length to find optimal chunk boundaries.

**Research Alignment:**
| Aspect | Source | Finding |
|--------|--------|---------|
| MDL principle | Rissanen (1978) | Information-theoretically sound |
| Sequence segmentation | ML literature | Established for time series |

**Gap Analysis:**
| Gap | Severity | Explanation |
|-----|----------|-------------|
| Model cost computation | 🟠 High | How to measure "parameters to store chunk"? |
| Hierarchical MDL complexity | 🟢 Medium | NP-hard; need approximations |
| Validation on action data | 🟠 High | No studies on action sequence segmentation |

**Implementation Readiness:** ⚠️ Requires algorithm development

---

### 9. World Model — GAP DUE TO MISSING CITATIONS

**Specification:** VAE encoder + GRU transition + reward predictor.

**Research Alignment:**
| Component | Source | Finding |
|-----------|--------|---------|
| VAE + GRU architecture | DreamerV3 (Hafner et al.) | Validated for world modeling |
| Reward prediction | Standard RL | Well-established |

**Gap Analysis:** The search results lack direct citations. The architecture should cite:
- Hafner et al., "Dream to Control" (Dreamer)
- Hafner et al., "Mastering Atari with Discrete World Models" (DreamerV2)
- GW-Dreamer (if available)

**Implementation Readiness:** ✅ Ready with proper citations

---

### 10. Dreaming Engine — CRITICAL GAP CLUSTER

#### 10.1 Multi-Scale Dreaming

**Specification:**
- Micro (10-100 steps): motor refinement
- Meso (100-1000 steps): routine optimization
- Macro (1000-10000 steps): strategic planning

**Research Alignment:**
| Scale | Source | Finding |
|-------|--------|---------|
| Dreaming generally | Neuromorphic dreaming (arXiv 2024) | Dreaming reduces real interactions |
| Multi-scale specifically | No research | Novel concept |

**Gap Analysis:** **CRITICAL GAP.** No validation that multi-scale dreaming works or that scales are appropriate.

#### 10.2 Mutation Operators

**Specification:**
- Micro: Gaussian noise on actions
- Meso: swap, insert, delete
- Macro: recombine skills

**Research Alignment:** No research on mutation operators for skill refinement.

**Gap Analysis:** **CRITICAL GAP.** Operators may create invalid behaviors. No validation that mutations produce improvements.

#### 10.3 Simulation-to-Reality Transfer

**Specification:** Improvements from dreaming transfer to real performance.

**Research Alignment:** Sim-to-real gap is well-documented in robotics. No evidence dreaming avoids it.

**Gap Analysis:** **CRITICAL GAP.** Requires extensive validation.

**Overall Dreaming Engine Readiness:** 🔴 **Requires substantial research**

---

### 11. Training Scheduler

#### 11.1 ROI-Based Prioritization

**Specification:** `ROI = (expected_improvement × frequency) / estimated_cost`

**Research Alignment:** Common in project management, not validated for ML training scheduling.

**Gap:** No research on effectiveness.

#### 11.2 Predictive Wake-Up

**Specification:** Analyze usage patterns to finish training before user wakes.

**Research Alignment:** Time-series prediction is well-studied.

**Gap:** Application to training scheduling is novel.

**Implementation Readiness:** 🟢 Medium (can be implemented and tested)

---

## Part IV: Cross-Cutting Research Gaps

### 12. Emergent Properties — UNVALIDATED

| Property | Claim | Research Support | Gap |
|----------|-------|------------------|-----|
| Resilience | System degrades gracefully | NeuroMesh (50% failure → 80% capacity) | Validated for network, not intelligence |
| Adaptive specialization | Agents tune to user patterns | SkillRL shows specialization emergence | Single-agent only |
| Progressive personalization | Learns user style over time | ALAS shows self-updating | Knowledge, not behavior |
| Hierarchical abstraction | Skills compose into higher-level | AutoSkill shows hierarchy | Robotic domain only |

**Conclusion:** Properties are plausible but require validation in Mycelium context.

### 13. Scaling Laws — UNKNOWN

| Question | Importance |
|----------|------------|
| How many agents on consumer hardware? | Critical for deployment |
| Memory footprint of 100 agents? | Critical for edge devices |
| Seed retrieval latency vs. library size? | Critical for real-time |
| Plinko entropy scaling? | Performance bound |

**Research Needed:** Empirical measurement.

### 14. Privacy Guarantees — UNEXPLORED

| Risk | Explanation |
|------|-------------|
| Seed leakage | Seeds may encode distinctive user patterns |
| Membership inference | Can attacker tell if user data was used? |
| Differential privacy | No specification of privacy budget |

**Research Needed:** Privacy analysis of seed encoding.

---

## Part V: Research Authority Assessment

| Authority Level | Sources |
|-----------------|---------|
| **High (Peer-Reviewed)** | Bio Cognitive Mesh (IEEE 2025), Electronics Letters CFP, SMARTEDGE Project (EU-funded) |
| **Medium (Preprint/Academic)** | SkillRL (arXiv 2026), GW-Dreamer (arXiv 2025), Neuromorphic dreaming (arXiv 2024), AutoSkill (IEEE TCDS 2025), EngramNCA (arXiv) |
| **Medium (Industry)** | Apple Mycelium (SIGCHI 2024), NeuroMesh (Devpost 2025) |
| **Low (Open Source)** | GMV mycelium (3 stars), MyceliumWebServer (activitypub-based) |

---

## Part VI: Prioritized Research Agenda

### Tier 1: Must Validate Before Implementation

| Gap | Component | Suggested Approach |
|-----|-----------|-------------------|
| Seed encoding capacity | Seed Engine | Benchmark on standard tasks (Minecraft, ALFRED) |
| Seed conditioning | Seed Engine | Compare FiLM, concatenation, separate policy |
| Dreaming transfer | Dreaming Engine | Sim-to-real correlation study |
| Determinism vs. adaptation | Core Architecture | Formalize hierarchy: action seeds vs. policy seeds |

### Tier 2: Needed for v1.0

| Gap | Component | Suggested Approach |
|-----|-----------|-------------------|
| Specialization embeddings | Agent Swarm | Compare model hash, architecture embedding, learned from usage |
| MDL chunking algorithm | Skill Chunker | Develop and test approximations |
| Discriminator training | Plinko Layer | Online learning with class imbalance |
| ROI prioritization | Training Scheduler | A/B test vs. round-robin |

### Tier 3: v2.0 and Beyond

| Gap | Component | Suggested Approach |
|-----|-----------|-------------------|
| Privacy guarantees | All | Differential privacy for seed training |
| Scaling laws | System | Empirical measurement |
| Emergent properties | System | Long-term deployment studies |
| Cross-user skill transfer | Ecosystem | Federated learning + seeds |

---

## Part VII: Implementation Readiness Summary

| Component | Readiness | Notes |
|-----------|-----------|-------|
| Sensor Layer | ✅ Ready | Implementation work |
| Agent Swarm (basic) | ✅ Ready | Lifecycle, scheduling |
| Agent Swarm (recruitment) | ⚠️ Needs research | Specialization embeddings |
| Plinko Layer | ⚠️ Needs experimentation | Discriminator training |
| Seed Engine | 🔴 Requires research | Core innovation unproven |
| Skill Chunker | ⚠️ Needs algorithm dev | MDL approximations |
| World Model | ✅ Ready (with citations) | Use Dreamer architecture |
| Dreaming Engine | 🔴 Requires research | Multi-scale unproven |
| Training Scheduler | 🟢 Medium | Can implement, tune |
| Memory | ✅ Ready | Vector DB integration |
| Model Zoo | ✅ Ready | Standard practice |
| APIs/Protocols | 🟢 Medium | Implementation work |

---

## Part VIII: References

### Peer-Reviewed
1. Bio Cognitive Mesh: Harnessing Swarm Intelligence for Self-Organizing AI at the Network Edge. *IEEE Fourth International Conference on Smart Technologies, Communication and Robotics (STCR)*, 2025.
2. SMARTEDGE Project: Cross-layer Toolchain for Device-Edge-Cloud Continuum. *EU Horizon Europe Research and Innovation Programme*, 2025.
3. Electronics Letters Call for Papers: Special Issue on Edge AI Architectures. *IET*, 2026.

### Preprints
4. SkillRL: Evolving Agents via Recursive Skill-Augmented Reinforcement Learning. *arXiv:2602.08234*, 2026.
5. GW-Dreamer: Multimodal Dreaming with Global Workspace Theory. *arXiv:2502.21142*, 2025.
6. Neuromorphic dreaming: A pathway to efficient learning in artificial agents. *arXiv:2405.15616*, 2024.
7. AutoSkill: Hierarchical Open-Ended Skill Acquisition. *IEEE Transactions on Cognitive and Developmental Systems*, 2025.
8. EngramNCA: Private Memory Channels in Neural Cellular Automata. *arXiv*, 2025.

### Industry/Open Source
9. Apple Mycelium: Graph-Based Agent Visualization. *SIGCHI 2024*.
10. NeuroMesh: Self-Healing Distributed AI Swarm. *Devpost 2025*.
11. MyceliumWebServer: ActivityPub-Based Federated Learning. *GitHub*, 2025.
12. GMV mycelium: Redis-Based Agent Communication. *GitHub*, 2025.

### Foundational
13. Seed AI. *Wikipedia* (cites Yudkowsky, 2001; Schmidhuber, 2006-2009).
14. Hafner et al. Dream to Control (Dreamer). *ICLR 2020*.
15. Hafner et al. Mastering Atari with Discrete World Models (DreamerV2). *ICLR 2021*.

---

## Appendix: Research Validation Checklist

Use this when reading research papers to validate against Mycelium claims:

| Claim | What to Look For |
|-------|------------------|
| Behavior compression | Sequence → latent vector, reconstruction accuracy |
| Deterministic replay | Same seed + context → same actions |
| Dreaming improves skills | Simulated improvement correlates with real |
| Multi-agent coordination | Swarm performance with/without central control |
| Skill discovery | Automatic segmentation of action sequences |
| Personalization | Model adapts to individual user over time |

---

*This document is a living research roadmap. For updates or to contribute to gap resolution, visit [github.com/superinstance/mycelium/research](https://github.com/superinstance/mycelium/research).*
