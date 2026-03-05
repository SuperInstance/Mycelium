# Mycelium Architecture Specification: Research-Annotated Outline

**Version 2.0 — April 2026**  
**SuperInstance Open Source Initiative**

---

## Outline Structure & Research Validation Methodology

This outline is organized to follow the logical flow of the Mycelium system: from external context down to implementation details, then outward to deployment and evolution. Each section is annotated with:

- **Research Alignment:** How the proposed design matches or extends published work
- **Implementation Gap:** Areas where additional research or validation is needed
- **Authority Note:** Credibility of referenced sources

The goal is to identify which parts of the architecture are well-supported by existing literature and which require original development or further investigation.

---

## Part I: Foundation and Context

### 1. Introduction
- 1.1 The Problem with Static Intelligence
- 1.2 A New Paradigm: Demonstration-Driven Development
- 1.3 Core Thesis: Behavior as Primary Artifact
- 1.4 Document Scope and Audience

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Problem statement (static models, cloud dependency) | Bio Cognitive Mesh (IEEE 2025)  | High (peer-reviewed conference) | Directly supports latency/bandwidth claims |
| Demonstration-driven paradigm | SMARTEDGE project  | High (EU-funded research) | "Low-code programming environment" aligns with demonstration concept |
| Seed-based behavior encoding | Seed AI / recursive self-improvement  | Medium (Wikipedia, but cites primary research) | Foundational concept of "seed improver" architecture |

**Gap Analysis:** While the problem is well-documented, the specific claim that "seeds can replace traditional code for most use cases" requires original empirical validation. The SMARTEDGE project  suggests low-code approaches are viable but doesn't compress to seed-level representation.

---

### 2. Core Concepts
- 2.1 Agents (Tiny Specialized Models)
- 2.2 Prompts and Seeds
- 2.3 Skills
- 2.4 World Models
- 2.5 Dreaming
- 2.6 Memory
- 2.7 Plinko Decision Layer
- 2.8 A2UI (Agent-to-UI)

**Research Validation:**
| Concept | Source | Authority | Alignment |
|---------|--------|-----------|-----------|
| Tiny specialized agents | Edge AI architectures  | High (CFP from Electronics Letters, peer-reviewed venue) | Confirms need for lightweight models for edge deployment |
| Multi-agent swarms | SMARTEDGE  | High | "Dynamic swarm network" and "autonomous intelligence swarm" directly validates swarm approach |
| Seed-based encoding | Seed AI / recursive self-improvement  | Medium | "Seed improver" architecture provides theoretical foundation |
| Private memory channels | EngramNCA research  | High (arXiv preprint, cellular automata) | "Private, cell-internal memory channels" validates agent memory concept |
| Graph-based model representation | Apple Mycelium  | High (Apple research, SIGCHI 2024) | Directed acyclic graph visualization supports agent network modeling |

**Gap Analysis:**
- **Seeds:** The Wikipedia article  discusses seed AI for recursive self-improvement, not behavior compression. The specific mechanism of encoding demonstrations into compact vectors appears to be novel to Mycelium and requires original implementation and validation.
- **Plinko Layer:** No direct research found on stochastic decision layers with adaptive temperature for multi-agent systems. This appears to be a novel contribution.
- **A2UI:** While UI automation exists (accessibility APIs), the unified agent interface is implementation work, not research.

---

## Part II: System Architecture

### 3. System Overview
- 3.1 High-Level Block Diagram
- 3.2 Two-Mode Operation (Day/Night)
- 3.3 Data Flow Summary
- 3.4 Key Design Decisions

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Edge-cloud continuum | SMARTEDGE  | High | "Cross-layer toolchain for Device-Edge-Cloud Continuum" directly validates hybrid approach |
| Day/night learning cycles | Neuromorphic dreaming research (implied) | - | No direct citation; relates to sleep/wake cycles in biological systems |

**Gap Analysis:** The day/night learning cycle is biologically inspired but not directly validated by the provided research. This is an architectural choice that requires empirical validation of effectiveness.

---

### 4. Sensor Layer
- 4.1 Capture Interfaces
- 4.2 Preprocessing Pipeline
- 4.3 Shared Memory Ring Buffers
- 4.4 Speculative Pre-processing
- 4.5 Latency Budget

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Shared memory for agent communication | GMV mycelium (Redis-based)  | Medium (GitHub project, low stars) | Validates in-memory data exchange approach |
| Speculative pre-processing | No direct research | - | Novel optimization technique |

**Gap Analysis:** Speculative pre-processing (predicting which sensors will be needed) is a performance optimization without research backing. It should be clearly labeled as an experimental feature.

---

## Part III: Agent Layer

### 5. Agent Swarm
- 5.1 Agent Data Structure
- 5.2 Agent Types and Model Specifications
- 5.3 Agent Lifecycle Management
- 5.4 Scheduling and Parallel Execution
- 5.5 Dynamic Agent Recruitment
- 5.6 Communication Protocol (Topics)

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Dynamic swarm formation | SMARTEDGE  | High | "Automatic discovery and dynamic network swarm formation" directly validates recruitment |
| Agent communication protocols | GMV mycelium  | Medium | Redis-based exchange provides implementation precedent |
| Graph-based agent visualization | Apple Mycelium  | High | DAG visualization supports monitoring agent networks |

**Gap Analysis:** The specific recruitment algorithm (cosine similarity on specialization embeddings) is not research-validated. The SMARTEDGE project  mentions "semantic-based interplay" but doesn't specify the mechanism.

---

### 6. Seed Capture & Replay Engine
- 6.1 Demonstration Capture Process
- 6.2 Seed Encoder Architecture
- 6.3 Training the Seed Encoder
- 6.4 Seed Replay Mechanism
- 6.5 Determinism Guarantees
- 6.6 Seed Storage Format

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Seed-based architecture | Seed AI / recursive self-improvement  | Medium | Foundational concept, though applied to AGI development |
| Autoencoder compression | Implied by ML literature | - | Standard technique, not Mycelium-specific |

**Gap Analysis:** **SIGNIFICANT GAP.** This is the core innovation of Mycelium, and the provided research contains minimal direct validation:
- No research found on encoding full behavior sequences into compact vectors for deterministic replay
- No validation that seeds can replace code for "most use cases"
- No precedent for the seed + prompt = exact behavior claim

**Action Required:** This component requires original research and extensive empirical validation. The architecture should present it as a hypothesis with planned experiments, not as an established technique.

---

### 7. Plinko Decision Layer
- 7.1 Proposal Collection
- 7.2 Discriminator Design and Training
- 7.3 Gumbel-Softmax Formulation
- 7.4 Adaptive Temperature Mechanism
- 7.5 Selection Algorithm
- 7.6 Mathematical Properties

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Gumbel-Softmax | Standard ML technique | High | Well-established for differentiable sampling |
| Multi-agent coordination | SMARTEDGE  | High | "Adaptive coordination and optimization" validates need |
| Discriminator-based filtering | No direct research | - | Novel combination |

**Gap Analysis:** The discriminator ensemble and adaptive temperature mechanism are novel combinations of existing techniques. While each piece (Gumbel noise, entropy-based adaptation) is established, their integration into a multi-agent decision layer lacks research validation.

---

## Part IV: Learning Systems

### 8. Skill Chunker
- 8.1 Sequence Mining
- 8.2 Temporal Autoencoder
- 8.3 MDL-Based Boundary Detection
- 8.4 Hierarchical Skill Composition
- 8.5 Skill Storage Format

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Sequence mining (PrefixSpan) | Established algorithm | High | Well-documented in data mining literature |
| Temporal autoencoders | ML literature | High | Standard technique |
| MDL principle | Information theory | High | Established for model selection |
| Hierarchical composition | No direct research | - | Novel application |

**Gap Analysis:** While each technique is established, their combination for autonomous skill discovery in a personal AI system lacks research validation. This is another area requiring original empirical work.

---

### 9. World Model
- 9.1 Architecture (Encoder, Transition, Reward, Decoder)
- 9.2 Training Procedure
- 9.3 Counterfactual Augmentation
- 9.4 Validation Metrics
- 9.5 Update Frequency

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| World models for dreaming | GW-Dreamer (implied) | - | Not directly provided in search results |
| VAE-based encoders | ML literature | High | Standard technique |

**Gap Analysis:** The search results do not contain the GW-Dreamer paper or other world model research. This component relies on external literature not provided. The architecture should cite specific papers (e.g., Hafner et al., "Dream to Control") for validation.

---

### 10. Dreaming Engine
- 10.1 Multi-Scale Dreaming (Micro, Meso, Macro)
- 10.2 Mutation Operators
- 10.3 Simulation Loop
- 10.4 Skill Selection and Storage
- 10.5 Computational Requirements

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Neuromorphic dreaming | Implied | - | Not directly provided |
| Multi-scale simulation | No direct research | - | Novel concept |

**Gap Analysis:** **SIGNIFICANT GAP.** The dreaming engine is central to Mycelium's claim of continuous improvement, but the search results lack validation:
- No research on multi-scale dreaming (micro/meso/macro)
- No validation that simulated improvements transfer to real performance
- Mutation operators are heuristic, not researched

---

### 11. Training Scheduler
- 11.1 ROI-Based Prioritization
- 11.2 Local vs. Cloud Decision
- 11.3 Predictive Wake-Up
- 11.4 Validation and Rollback
- 11.5 Resource Management

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Edge-cloud interplay | SMARTEDGE  | High | "Swarm elasticity via Edge-Cloud Interplay" validates hybrid approach |
| Predictive scheduling | No direct research | - | Novel optimization |

**Gap Analysis:** ROI-based prioritization and predictive wake-up are novel optimizations without research backing. The SMARTEDGE project  validates the need for edge-cloud coordination but not the specific algorithms.

---

## Part V: Data and Persistence

### 12. Memory (Vector Database)
- 12.1 Schema Design
- 12.2 Embedding Generation
- 12.3 Retrieval Interface
- 12.4 Privacy Considerations
- 12.5 Cross-Device Sync (Optional)

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Vector databases (Chroma, LanceDB) | Industry tools | High | Well-established |
| Private memory channels | EngramNCA  | High | "Private, cell-internal memory channels" validates agent memory concept |
| Embedding-based retrieval | ML literature | High | Standard technique |

**Gap Analysis:** The specific integration of vector databases with agent memory is implementation work, not research. The EngramNCA paper  provides biological inspiration but not implementation guidance.

---

### 13. Model Zoo
- 13.1 Storage Structure
- 13.2 Versioning Strategy
- 13.3 Metadata Schema
- 13.4 Automatic Rollback
- 13.5 Seed Registry

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Model versioning | Industry practice | High | Standard DevOps/MLOps |
| Automatic rollback | No direct research | - | Implementation choice |

**Gap Analysis:** This component is standard practice, not requiring research validation.

---

## Part VI: Interfaces and Protocols

### 14. APIs and SDKs
- 14.1 Public API for Developers
- 14.2 Agent Development SDK
- 14.3 Seed API (Export/Import/Verify)
- 14.4 LucidDreamer.ai Integration

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Low-code toolchain | SMARTEDGE  | High | "Low-code Toolchain for Edge Intelligence" validates developer tools approach |

**Gap Analysis:** API design is implementation work. The SMARTEDGE project  validates the need but doesn't prescribe the interface.

---

### 15. Data Formats and Protocols
- 15.1 Seed Format (Protobuf)
- 15.2 Proposal Format (Cap'n Proto)
- 15.3 Log Format (Parquet)
- 15.4 Agent Communication Protocol
- 15.5 Seed Exchange Protocol

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Cap'n Proto for proposals | No direct research | - | Performance choice |
| Parquet for logs | Industry standard | High | Well-established for columnar storage |

**Gap Analysis:** Format choices are implementation decisions, not research.

---

## Part VII: Implementation and Deployment

### 16. Implementation Roadmap
- 16.1 Phase 1: Prototype (0–3 months)
- 16.2 Phase 2: On-Device Learning (4–9 months)
- 16.3 Phase 3: Advanced Features (10–15 months)
- 16.4 Phase 4: Ecosystem (16–24 months)

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Phased approach | Industry practice | High | Standard for open-source projects |

**Gap Analysis:** The roadmap reflects engineering milestones, not research.

---

### 17. Deployment Scenarios
- 17.1 Personal Automation
- 17.2 Simulation-First Development
- 17.3 Seed Sharing
- 17.4 Adaptive UI
- 17.5 Continuous Learning Systems

**Research Validation:**
| Component | Source | Authority | Alignment |
|-----------|--------|-----------|-----------|
| Edge AI applications | SMARTEDGE  | High | Validates automotive, city, factory, health domains |
| Multi-agent systems | SMARTEDGE  | High | "Cooperative robotics" and "multi-agent systems" in  |
| Adaptive systems | Electronics Letters CFP  | High | "Adaptability, robustness, and real-time decision-making" |

**Gap Analysis:** The specific use cases (email triage, to-do app simulation) are illustrative. The research validates the general categories (personal automation, multi-agent systems) but not the specific implementations.

---

## Part VIII: Appendices

### 18. Glossary
### 19. Mathematical Derivations
- 19.1 Plinko Score Derivation
- 19.2 Adaptive Temperature
- 19.3 MDL for Skill Chunking
### 20. References

---

## Summary of Gaps Requiring Original Research

| Component | Gap Severity | Research Needed |
|-----------|--------------|------------------|
| **Seed Capture & Replay** | **CRITICAL** | Can full behavior sequences be compressed into compact vectors and deterministically replayed? Does seed + prompt actually reproduce exact behavior across contexts? |
| **Dreaming Engine** | **CRITICAL** | Does multi-scale simulation (micro/meso/macro) improve real-world performance? Do mutation operators produce valid improvements? |
| **Plinko Layer** | High | Does adaptive temperature based on entropy improve decision quality? How do discriminators compare to learned vs. hand-crafted? |
| **Skill Chunker** | High | Does MDL-based boundary detection discover optimal skill hierarchies? How does temporal autoencoder performance compare to simpler methods? |
| **Training Scheduler** | Medium | Does ROI-based prioritization improve learning efficiency? Does predictive wake-up provide measurable benefit? |
| **Speculative Pre-processing** | Low | Does predicting sensor needs reduce latency? By how much? |

**Research Authority Summary:**

| Authority Level | Sources |
|-----------------|---------|
| **High (Peer-Reviewed)** | SMARTEDGE project  (EU-funded), Electronics Letters CFP , Bio Cognitive Mesh (implied, 2025 IEEE) |
| **Medium (Preprint/Academic)** | Seed AI Wikipedia  (cites primary sources), EngramNCA  (arXiv) |
| **Medium (Industry Research)** | Apple Mycelium  (SIGCHI 2024) |
| **Low (GitHub Projects)** | GMV mycelium  (3 stars, limited adoption) |

---

## Next Steps

Based on this annotated outline, the following actions are recommended before finalizing the architecture document:

1. **Research seed compression literature:** Investigate whether existing work on behavior cloning, imitation learning, or skill discovery can inform the seed encoder design.

2. **Design experiments for validation:** The architecture should include planned experiments to validate each novel component, especially the seed engine and dreaming engine.

3. **Add citations to established world model papers:** Replace implied references with specific citations (e.g., Hafner et al., DreamerV3).

4. **Clearly label speculative components:** Components without research backing should be labeled as "experimental" or "proposed" with validation plans.

5. **Consider simplifying the initial scope:** Focus on well-validated components first, adding novel elements incrementally as research confirms their effectiveness.
