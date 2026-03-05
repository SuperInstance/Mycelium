# Mycelium Research Agenda: Open Questions for Investigation

**Version 1.0 — May 2026**  
**SuperInstance Research Team**  
*A comprehensive collection of research questions to guide our investigation into seed-based, swarm intelligence systems*

---

## How to Use This Document

This agenda organizes research questions by component and theme. Each question is followed by:
- **Research directions**: What to investigate
- **Approaches**: How you might investigate it (methods, experiments, literature to review)
- **Connections**: Links to other questions and components
- **Priority**: Our assessment of importance (High/Medium/Low)

This is a living document. As we answer questions, new ones will emerge. As we build the system, we will discover what we didn't know to ask.

---

## Part I: Foundational Questions

These questions underpin the entire Mycelium architecture. Answering them will shape every design decision.

### 1. The Seed Hypothesis

**Core question**: Can complex behavioral sequences be compressed into compact vectors and deterministically replayed?

#### 1.1 Information-theoretic bounds

**Question**: What is the minimum latent dimension needed to encode a behavioral sequence of length L with acceptable reconstruction error?

**Research directions**:
- Information theory: rate-distortion theory for behavioral sequences
- Empirical scaling laws: measure reconstruction error vs. latent dimension across diverse tasks
- Theoretical lower bounds: what can Kolmogorov complexity tell us about sequence compressibility?

**Approaches**:
- Literature review: sequence compression in NLP (sentence embeddings), video compression, motion capture encoding
- Synthetic experiments: generate sequences of varying complexity, encode/decode, measure fidelity
- Task complexity metrics: develop ways to quantify "behavioral complexity" independent of sequence length

**Priority**: High

---

#### 1.2 Behavioral reconstruction fidelity

**Question**: What does "acceptable reconstruction" mean for different types of behaviors? When is a reconstructed behavior "good enough"?

**Research directions**:
- Task-specific metrics: for UI automation, is exact pixel-level reproduction needed? For robotics, is trajectory matching sufficient?
- Human perception studies: at what point do humans detect differences between original and reconstructed behavior?
- Downstream task performance: does a behavior reconstructed from a seed perform the original task as well?

**Approaches**:
- User studies with reconstructed vs. original behaviors
- Task performance benchmarking across reconstruction quality levels
- Literature: behavioral cloning, imitation learning evaluation metrics

**Priority**: High

---

#### 1.3 Seed vs. policy ambiguity

**Question**: Does a seed encode a specific action sequence or a policy for generating actions? How do we resolve this ambiguity?

**Research directions**:
- Deterministic vs. stochastic environments: what kind of encoding works best where?
- Trade-off analysis: exact sequences are brittle but precise; policies are flexible but may drift
- Hybrid approaches: can seeds encode both a policy and a set of "anchor points" for correction?

**Approaches**:
- Compare seed types (action-sequence vs. policy) on tasks with varying environmental variability
- Literature: policy distillation, behavior cloning, hierarchical RL

**Priority**: High

---

#### 1.4 Sequence length scaling

**Question**: How does required latent dimension scale with sequence length? Is it linear? Logarithmic? Task-dependent?

**Research directions**:
- Empirical measurement across multiple task domains
- Theoretical analysis: what determines compressibility of behavior?
- Role of repetition and structure: are human behaviors more compressible than random sequences?

**Approaches**:
- Generate sequences with known compressibility (e.g., repeating patterns, random walks, structured tasks)
- Measure reconstruction quality vs. latent dimension
- Develop predictive model of required dimension given sequence statistics

**Priority**: Medium

---

### 2. Prompt + Seed Determinism

**Core question**: Can we achieve deterministic behavior reproduction while maintaining environmental adaptability?

#### 2.1 Formal definition of determinism

**Question**: What does "deterministic" mean in a system that interacts with a non-deterministic environment?

**Research directions**:
- Determinism in closed vs. open systems
- Conditional determinism: given same observations, same actions; but observations may differ
- Levels of determinism: action-level, outcome-level, goal-level

**Approaches**:
- Formal methods: define determinism precisely for interactive systems
- Literature: deterministic policies in RL, open systems verification

**Priority**: High

---

#### 2.2 Trade-off characterization

**Question**: What is the precise trade-off between exact reproduction and environmental adaptation? Can we quantify it?

**Research directions**:
- Pareto frontier analysis: plot adaptation vs. fidelity for different seed designs
- Task-dependent trade-offs: when is exact reproduction critical? When is adaptation essential?
- User preference studies: what do users actually want? (Exact repetition? Intelligent adaptation?)

**Approaches**:
- Design experiments with controlled environmental variation
- Measure performance and user satisfaction across seed types
- Literature: multi-objective optimization, human-AI interaction

**Priority**: High

---

#### 2.3 Two-seed type hypothesis validation

**Question**: Is the distinction between "action seeds" and "policy seeds" sufficient and useful? Are there other natural categories?

**Research directions**:
- Empirical clustering: do different tasks naturally fall into distinct seed-type categories?
- Hybrid seeds: can seeds combine both action sequences and policy parameters?
- Meta-seeds: seeds that generate other seeds (recursive composition)

**Approaches**:
- Cluster analysis of task requirements
- Design and evaluate hybrid seed architectures
- Literature: hierarchical RL, program synthesis

**Priority**: Medium

---

## Part II: Seed Capture and Encoding

### 3. Demonstration Capture

#### 3.1 Demonstration sufficiency

**Question**: How many demonstrations are needed to capture a robust seed? Does one demonstration suffice?

**Research directions**:
- Variation in human demonstration: do different people demonstrate the same task differently?
- Intra-person variation: does the same person perform the same task differently on different days?
- Minimum demonstration count: what's the lower bound for reliable seed extraction?

**Approaches**:
- Collect multiple demonstrations of same task from same/different users
- Measure seed consistency and task performance vs. number of demonstrations
- Literature: one-shot learning, few-shot imitation

**Priority**: Medium

---

#### 3.2 Demonstration segmentation

**Question**: When does a demonstration start and end? How do we automatically detect meaningful boundaries?

**Research directions**:
- User-initiated boundaries: natural start/stop signals (voice, gesture, UI)
- Automatic segmentation: can we detect task boundaries from observation stream?
- Hierarchical segmentation: tasks within tasks within tasks

**Approaches**:
- Study user behavior patterns: when do people naturally indicate task boundaries?
- Develop unsupervised segmentation algorithms (change point detection, MDL)
- Literature: event segmentation in psychology, activity recognition

**Priority**: Medium

---

#### 3.3 Noise and errors in demonstrations

**Question**: How do we handle mistakes, hesitations, and inefficiencies in human demonstrations?

**Research directions**:
- Error detection: can we automatically identify likely mistakes?
- Demonstration cleaning: should we filter noise before encoding?
- Learning from imperfect demonstrations: can seeds capture intent despite execution errors?

**Approaches**:
- Collect demonstrations with deliberate errors; test seed quality
- Develop noise filters and error correction algorithms
- Literature: learning from demonstrations, inverse reinforcement learning

**Priority**: High

---

### 4. Seed Encoder Architecture

#### 4.1 Architecture comparison

**Question**: What neural architecture is optimal for encoding behavioral sequences into seeds?

**Research directions**:
- Recurrent architectures (LSTM, GRU) vs. transformers vs. CNNs
- Autoencoder variants: vanilla, variational, adversarial
- Hierarchical encoders for long sequences
- Computational efficiency vs. encoding quality trade-offs

**Approaches**:
- Systematic architecture comparison on benchmark tasks
- Measure reconstruction quality, inference speed, memory usage
- Literature: sequence-to-sequence models, video compression, motion capture encoding

**Priority**: High

---

#### 4.2 Loss function design

**Question**: What loss functions produce seeds that are both reconstructable and useful downstream?

**Research directions**:
- Reconstruction loss alone vs. combined with contrastive loss
- Task-specific losses: can we incorporate downstream task performance into encoder training?
- Regularization: what prevents overfitting to specific demonstration details?

**Approaches**:
- Ablation study: train encoders with different loss components
- Measure seed quality through downstream task performance
- Literature: representation learning, contrastive learning, metric learning

**Priority**: High

---

#### 4.3 Contrastive loss effectiveness

**Question**: Does contrastive learning (pulling same-demonstration seeds together, pushing different-demonstration seeds apart) improve seed quality? By how much?

**Research directions**:
- Optimal margin for contrastive loss
- Negative sampling strategies: how many negatives? How to select them?
- Trade-off: contrastive loss may reduce reconstruction quality

**Approaches**:
- Controlled experiments with/without contrastive loss
- Measure seed discrimination accuracy vs. reconstruction fidelity
- Literature: SimCLR, triplet loss, self-supervised learning

**Priority**: Medium

---

#### 4.4 Seed dimensionality

**Question**: Is there an optimal seed dimension, or does it depend on task complexity?

**Research directions**:
- Empirical scaling: measure required dimension vs. task complexity
- Diminishing returns: at what point does adding dimensions stop improving quality?
- Adaptive dimension: can we learn seeds with variable dimension?

**Approaches**:
- Sweep latent dimension across tasks
- Measure reconstruction quality and downstream performance
- Literature: latent variable models, information bottleneck

**Priority**: Medium

---

### 5. Seed Conditioning Mechanisms

#### 5.1 Conditioning method comparison

**Question**: What is the most effective way to inject a seed into an agent to influence its behavior?

**Research directions**:
- FiLM (Feature-wise Linear Modulation): modulates agent activations
- Latent concatenation: adds seed to agent input or hidden state
- Separate policy network: seed selects among sub-policies
- Hybrid approaches: combinations of the above

**Approaches**:
- Implement all candidate mechanisms; compare on benchmark tasks
- Measure: behavior reproduction fidelity, impact on base capabilities, computational overhead
- Literature: conditional computation, multi-task learning, parameter-efficient fine-tuning

**Priority**: Critical

---

#### 5.2 Base capability preservation

**Question**: How do we ensure that conditioning on a seed doesn't degrade the agent's general capabilities?

**Research directions**:
- Catastrophic forgetting: does seed conditioning overwrite base knowledge?
- Interference: do different seeds conflict with each other?
- Capacity limits: how many seeds can an agent host before performance degrades?

**Approaches**:
- Measure agent performance on held-out tasks before and after seed conditioning
- Test multiple seeds in same agent; look for interference patterns
- Literature: continual learning, elastic weight consolidation, progressive networks

**Priority**: Critical

---

#### 5.3 Multiple seed integration

**Question**: Can an agent simultaneously condition on multiple seeds? How should they be combined?

**Research directions**:
- Seed composition: linear combination, attention-based weighting, hierarchical selection
- Conflict resolution: what happens when seeds suggest conflicting behaviors?
- Emergent behaviors: can combining seeds produce novel, untaught behaviors?

**Approaches**:
- Design and test seed composition operators
- Evaluate on tasks requiring multiple skills (e.g., "email while on phone")
- Literature: mixture of experts, multi-task learning, compositionality

**Priority**: High

---

#### 5.4 Seed-agent compatibility

**Question**: What determines whether a seed is compatible with a given agent? Can seeds transfer across different agent architectures?

**Research directions**:
- Architecture compatibility: can a seed trained for LSTM work with transformer?
- Capacity compatibility: does seed require agent to have certain size/capabilities?
- Representation alignment: do different agents learn compatible internal representations?

**Approaches**:
- Cross-agent seed transfer experiments
- Analyze internal representations (representational similarity analysis)
- Literature: model stitching, representation learning, transfer learning

**Priority**: High

---

## Part III: Plinko Decision Layer

### 6. Discriminator Design

#### 6.1 Discriminator training data

**Question**: What data is needed to train effective discriminators? How do we label it?

**Research directions**:
- Human labeling: what instructions produce reliable labels?
- Implicit feedback: can we infer "good" vs. "bad" from user behavior (corrections, pauses, repeats)?
- Active learning: which examples are most valuable to label?

**Approaches**:
- Collect human-labeled datasets; measure inter-annotator agreement
- Develop implicit feedback models; validate against human judgments
- Literature: reinforcement learning from human feedback (RLHF), active learning

**Priority**: High

---

#### 6.2 Discriminator architecture

**Question**: What architecture is optimal for discriminators? How small can they be while remaining effective?

**Research directions**:
- Logistic regression vs. MLP vs. tiny transformers
- Feature engineering: what inputs do discriminators need?
- Computational cost: latency, memory footprint

**Approaches**:
- Compare architectures on classification accuracy and inference speed
- Feature importance analysis: which proposal features are most predictive?
- Literature: lightweight classifiers, edge ML

**Priority**: Medium

---

#### 6.3 Discriminator ensemble dynamics

**Question**: How do multiple discriminators interact? Is multiplicative combination optimal?

**Research directions**:
- Alternative combination rules: weighted sum, min, max, learned combination
- Discriminator calibration: do they output well-calibrated probabilities?
- Conflict resolution: what happens when discriminators disagree strongly?

**Approaches**:
- Experiment with different combination functions
- Measure calibration (expected vs. actual accuracy)
- Literature: ensemble methods, classifier combination, calibration

**Priority**: Medium

---

### 7. Adaptive Temperature

#### 7.1 Entropy-temperature relationship

**Question**: Is the proposed linear relationship between entropy and temperature optimal? What function works best?

**Research directions**:
- Alternative functions: exponential, piecewise, learned mapping
- Task-dependent tuning: does optimal relationship vary by task type?
- Theoretical grounding: what does information theory suggest?

**Approaches**:
- Sweep temperature functions; measure decision quality and exploration
- Meta-learning: learn temperature policy from experience
- Literature: simulated annealing, exploration-exploitation trade-off

**Priority**: High

---

#### 7.2 Temperature dynamics

**Question**: How quickly should temperature adapt to changing uncertainty? Should it have momentum?

**Research directions**:
- Response time: how many steps to adjust to new uncertainty level?
- Overshoot: does temperature oscillate?
- Hysteresis: should temperature be slower to decrease than increase?

**Approaches**:
- Measure temperature dynamics in controlled uncertainty environments
- Design and test adaptive filters (exponential moving average, PID control)
- Literature: adaptive control, learning rate scheduling

**Priority**: Medium

---

#### 7.3 Exploration vs. exploitation measurement

**Question**: How do we measure whether adaptive temperature is improving the exploration-exploitation trade-off?

**Research directions**:
- Exploration metrics: entropy of actions, diversity of attempted behaviors
- Exploitation metrics: task success rate, convergence speed
- Counterfactual evaluation: what would have happened with fixed temperature?

**Approaches**:
- A/B tests comparing adaptive vs. fixed temperature
- Measure both short-term and long-term performance
- Literature: multi-armed bandits, reinforcement learning evaluation

**Priority**: High

---

### 8. Gumbel Noise Properties

#### 8.1 Noise distribution

**Question**: Is Gumbel noise optimal? What about other noise distributions (Gaussian, logistic, uniform)?

**Research directions**:
- Theoretical properties: Gumbel yields unbiased samples from categorical
- Empirical comparison: does distribution affect decision quality?
- Computational efficiency: which is cheapest to sample?

**Approaches**:
- Compare noise distributions on benchmark tasks
- Measure: decision quality, sampling speed, gradient properties (if used in training)
- Literature: Gumbel-Softmax, reparameterization tricks

**Priority**: Low

---

#### 8.2 Temperature-noise interaction

**Question**: How do temperature and noise interact? Is the multiplicative formulation correct?

**Research directions**:
- Alternative formulations: additive noise before temperature, noise on logits vs. probabilities
- Theoretical analysis: what does each formulation imply about decision probabilities?
- Empirical comparison: which produces better exploration?

**Approaches**:
- Derive implied probability distributions for each formulation
- Experimentally compare on tasks requiring exploration
- Literature: stochastic decision processes, simulated annealing

**Priority**: Medium

---

## Part IV: Skill Chunking

### 9. Frequent Subsequence Mining

#### 9.1 Threshold selection

**Question**: What minimum frequency threshold produces useful skill candidates? Does it vary by task?

**Research directions**:
- Statistical significance: what frequency indicates non-random pattern?
- Task complexity: do complex tasks require lower thresholds?
- User variation: does optimal threshold vary across users?

**Approaches**:
- Sweep thresholds; measure quality of discovered skills
- Develop adaptive threshold based on sequence statistics
- Literature: pattern mining, association rule learning

**Priority**: Medium

---

#### 9.2 Algorithm comparison

**Question**: Is PrefixSpan optimal? How do other sequence mining algorithms compare?

**Research directions**:
- PrefixSpan vs. SPADE vs. GSP vs. custom algorithms
- Time complexity vs. pattern quality trade-offs
- Scalability to long sequences and many patterns

**Approaches**:
- Implement and benchmark multiple algorithms
- Measure: runtime, memory usage, pattern quality
- Literature: sequence mining, pattern discovery

**Priority**: Low

---

### 10. Temporal Autoencoder

#### 10.1 Architecture for sequences

**Question**: What autoencoder architecture best captures temporal structure in action sequences?

**Research directions**:
- LSTM autoencoders vs. transformer autoencoders vs. TCNs
- Importance of bidirectional encoding
- Hierarchical autoencoders for long sequences

**Approaches**:
- Systematic architecture comparison
- Measure reconstruction quality and downstream skill utility
- Literature: sequence autoencoders, video prediction models

**Priority**: High

---

#### 10.2 Action representation

**Question**: How should actions be represented for encoding? One-hot? Learned embeddings? Combined with observations?

**Research directions**:
- Action-only vs. action+observation encoding
- Discrete action embeddings vs. continuous parameters
- Impact of action representation on skill transfer

**Approaches**:
- Compare action representation schemes
- Measure reconstruction accuracy and transfer performance
- Literature: action representation learning, skill discovery

**Priority**: Medium

---

#### 10.3 Variable-length sequences

**Question**: How should the autoencoder handle sequences of varying lengths?

**Research directions**:
- Fixed-length encoding (LSTM last state) vs. length-agnostic (attention pooling)
- Length information: should length be encoded separately?
- Padding strategies: how to handle variable-length batches?

**Approaches**:
- Compare variable-length handling methods
- Measure: encoding quality, computational efficiency
- Literature: sequence-to-sequence models, variable-length processing

**Priority**: Medium

---

### 11. MDL-Based Boundary Detection

#### 11.1 Model cost definition

**Question**: How should we measure "model cost" for an action sequence chunk?

**Research directions**:
- Parameter count: number of parameters to store chunk as skill
- Compression-based: size of compressed representation
- Information-theoretic: description length of chunk model

**Approaches**:
- Experiment with different model cost definitions
- Measure: chunk quality, computational efficiency
- Literature: minimum description length, Kolmogorov complexity

**Priority**: High

---

#### 11.2 Data cost definition

**Question**: How should we measure "data cost" (reconstruction error) for a chunk?

**Research directions**:
- Reconstruction error metrics: MSE, cross-entropy, task-specific loss
- Per-step vs. cumulative error
- Weighting: should errors early in sequence matter more?

**Approaches**:
- Compare error metrics on downstream task performance
- Literature: loss functions for sequence modeling

**Priority**: High

---

#### 11.3 Optimization algorithm

**Question**: How to efficiently find MDL-optimal chunk boundaries in long sequences?

**Research directions**:
- Dynamic programming: O(n²) is too slow for long sequences
- Approximate algorithms: greedy, beam search, hierarchical
- Online vs. offline segmentation

**Approaches**:
- Implement and benchmark optimization algorithms
- Measure: optimality gap, runtime, scalability
- Literature: change point detection, sequence segmentation

**Priority**: High

---

#### 11.4 Hierarchical boundary detection

**Question**: How to detect hierarchical structure (chunks within chunks) efficiently and accurately?

**Research directions**:
- Recursive MDL: apply MDL recursively to chunks
- Grammar induction: learn hierarchical grammar of actions
- Evaluation: how to measure correctness of discovered hierarchy?

**Approaches**:
- Implement recursive MDL; test on artificially hierarchical sequences
- Compare with grammar induction algorithms
- Literature: hierarchical reinforcement learning, grammar induction

**Priority**: Medium

---

### 12. Skill Evaluation

#### 12.1 Skill quality metrics

**Question**: How do we measure whether a discovered skill is "good"?

**Research directions**:
- Reusability: how often is the skill used in new contexts?
- Compositionality: does the skill combine well with others?
- Robustness: does the skill work in varying conditions?
- Interpretability: can humans understand what the skill does?

**Approaches**:
- Develop multi-faceted skill quality metrics
- Validate metrics against human judgments
- Literature: skill discovery evaluation, transfer learning metrics

**Priority**: High

---

#### 12.2 Skill vs. no-skill comparison

**Question**: Do skills actually improve performance over using raw sequences?

**Research directions**:
- Learning speed: do skills accelerate acquisition of new tasks?
- Memory efficiency: do skills reduce storage?
- Transfer: do skills help in novel situations?

**Approaches**:
- Controlled experiments: with vs. without skill chunking
- Measure: task completion time, success rate, sample efficiency
- Literature: transfer learning, hierarchical RL evaluation

**Priority**: Critical

---

## Part V: World Model

### 13. World Model Architecture

#### 13.1 Architecture comparison for personal environments

**Question**: What world model architecture works best for personal digital environments (apps, UI, system)?

**Research directions**:
- VAE vs. deterministic autoencoder
- Recurrent vs. transformer transition models
- Discrete vs. continuous latent spaces
- Incorporation of domain knowledge (UI structure, app behaviors)

**Approaches**:
- Compare architectures on logged interaction data
- Measure: prediction accuracy, dreaming effectiveness, computational cost
- Literature: world models (Dreamer, PlaNet), environment modeling

**Priority**: High

---

#### 13.2 Latent dimension

**Question**: What latent dimension captures sufficient information about personal digital environments?

**Research directions**:
- Empirical scaling: measure prediction accuracy vs. dimension
- Task dependence: do different tasks require different resolution?
- Compression ratio: what's the trade-off between compression and accuracy?

**Approaches**:
- Sweep latent dimension; measure prediction accuracy
- Analyze information content of latent representations
- Literature: latent variable models, information bottleneck

**Priority**: Medium

---

#### 13.3 Observation representation

**Question**: How should observations (screen, audio, events) be represented for the world model?

**Research directions**:
- Raw vs. preprocessed inputs
- Modality-specific encoders vs. unified representation
- Temporal context: how much history to include?

**Approaches**:
- Compare representation schemes on prediction accuracy
- Measure: computational cost, memory usage
- Literature: multimodal representation learning, sensor fusion

**Priority**: High

---

### 14. World Model Training

#### 14.1 Training data requirements

**Question**: How much logged interaction is needed to train a useful world model? Does it scale with environment complexity?

**Research directions**:
- Learning curves: prediction accuracy vs. amount of training data
- Data efficiency: can we augment with synthetic data?
- Personalization: how much user-specific data is needed vs. transfer from population?

**Approaches**:
- Measure world model accuracy as function of training data size
- Experiment with data augmentation techniques
- Literature: sample efficiency, few-shot learning

**Priority**: High

---

#### 14.2 Counterfactual augmentation effectiveness

**Question**: Does counterfactual augmentation (swapping actions in similar contexts) actually improve world model generalization?

**Research directions**:
- Augmentation strategies: random swaps, guided swaps, learned interventions
- Impact on rare event prediction
- Risk of introducing impossible transitions

**Approaches**:
- Controlled experiments with/without augmentation
- Measure prediction accuracy on held-out transitions
- Literature: data augmentation for RL, counterfactual reasoning

**Priority**: Medium

---

#### 14.3 Online vs. batch training

**Question**: Should world model be trained online (continuous update) or in nightly batches? What are the trade-offs?

**Research directions**:
- Stability: does online training cause catastrophic forgetting?
- Freshness: how quickly can model adapt to environment changes?
- Computational cost: online vs. batch efficiency

**Approaches**:
- Compare online and batch training on same data stream
- Measure: prediction accuracy over time, computational cost
- Literature: online learning, continual learning

**Priority**: Medium

---

#### 14.4 Model forgetting

**Question**: Does the world model forget rarely encountered situations? How do we prevent this?

**Research directions**:
- Forgetting measurement: track accuracy on rare events over time
- Mitigation strategies: replay buffers, elastic weight consolidation, periodic retraining
- Importance weighting: should rare events be weighted higher?

**Approaches**:
- Long-term studies of world model accuracy on rare events
- Experiment with forgetting mitigation techniques
- Literature: catastrophic forgetting, continual learning

**Priority**: High

---

### 15. World Model Evaluation

#### 15.1 Prediction accuracy metrics

**Question**: How should we measure world model prediction accuracy? What errors matter most for dreaming?

**Research directions**:
- Next-step prediction accuracy
- Multi-step rollout error (compounding error)
- Task-relevant prediction: do errors in unimportant dimensions matter less?

**Approaches**:
- Develop task-weighted prediction metrics
- Correlate prediction accuracy with dreaming improvement
- Literature: model-based RL evaluation, predictive modeling

**Priority**: High

---

#### 15.2 Dreaming utility correlation

**Question**: How well does world model accuracy predict dreaming utility? Can we have accurate models that don't help dreaming, or inaccurate models that do?

**Research directions**:
- Disentangle model accuracy and dreaming effectiveness
- Identify properties that make a model good for dreaming (smoothness, uncertainty calibration, etc.)
- Develop dreaming-specific evaluation metrics

**Approaches**:
- Correlate various model properties with dreaming improvement
- Design experiments with deliberately flawed models to isolate important properties
- Literature: model-based RL, simulation-to-real transfer

**Priority**: Critical

---

## Part VI: Dreaming Engine

### 16. Multi-Scale Dreaming

#### 16.1 Scale definition validation

**Question**: Is the micro/meso/macro distinction natural and useful? Are these the right scales?

**Research directions**:
- Empirical clustering: do learned skills naturally fall into these temporal scales?
- Task analysis: what scales matter for different tasks?
- Continuous vs. discrete scales: should scale be a continuous parameter?

**Approaches**:
- Cluster discovered skills by temporal extent
- Analyze task requirements across scales
- Literature: temporal abstraction, hierarchical RL

**Priority**: Medium

---

#### 16.2 Scale interaction

**Question**: How do improvements at different scales interact? Does improving micro skills help meso skills? Vice versa?

**Research directions**:
- Cross-scale transfer: measure impact of micro-dreaming on meso performance
- Interference: could optimizing at one scale harm performance at another?
- Hierarchical dreaming: should we dream at multiple scales simultaneously?

**Approaches**:
- Controlled experiments with selective dreaming at each scale
- Measure performance at all scales after each intervention
- Literature: hierarchical RL, transfer learning

**Priority**: High

---

#### 16.3 Optimal dreaming schedule

**Question**: How much dreaming at each scale is optimal? Should it be fixed or adaptive?

**Research directions**:
- Diminishing returns: do gains from additional dreaming decrease?
- Scale prioritization: which scale yields highest ROI for a given skill?
- Adaptive scheduling: can we learn when to dream at which scale?

**Approaches**:
- Sweep dreaming allocation across scales; measure improvement
- Develop meta-learning for dreaming schedule
- Literature: multi-task learning, resource allocation

**Priority**: Medium

---

### 17. Mutation Operators

#### 17.1 Micro mutation effectiveness

**Question**: What mutation operators effectively improve low-level motor skills? Gaussian noise on parameters? Something else?

**Research directions**:
- Noise distribution: Gaussian vs. uniform vs. correlated noise
- Noise magnitude: optimal scale for exploration
- Structured mutations: do we need task-specific operators?

**Approaches**:
- Compare mutation operators on simulated motor tasks
- Measure: improvement rate, sample efficiency, final performance
- Literature: evolution strategies, policy gradient

**Priority**: High

---

#### 17.2 Meso mutation effectiveness

**Question**: What mutation operators effectively optimize routine sequences? Swap? Insert? Delete? Combinations?

**Research directions**:
- Operator effectiveness ranking: which help most?
- Operator combinations: do they interact positively or negatively?
- Sequence constraints: how to ensure mutated sequences are valid?

**Approaches**:
- Test each operator in isolation and combination
- Measure: success rate of mutated sequences, diversity of generated sequences
- Literature: genetic programming, sequence optimization

**Priority**: High

---

#### 17.3 Macro mutation effectiveness

**Question**: What mutation operators effectively recombine skills at the strategic level? How do we ensure meaningful recombination?

**Research directions**:
- Skill composition operators: concatenation, interleaving, substitution
- Interface matching: how to ensure composed skills connect properly?
- Novelty vs. validity: balancing exploration and plausibility

**Approaches**:
- Design and test composition operators
- Evaluate on tasks requiring multiple skills
- Literature: program synthesis, hierarchical RL

**Priority**: High

---

#### 17.4 Mutation rate adaptation

**Question**: How should mutation rates adapt over the course of dreaming? Should they decrease as skills improve?

**Research directions**:
- Annealing schedules: linear, exponential, adaptive
- Rate adaptation based on improvement velocity
- Per-operator rates: different operators need different rates

**Approaches**:
- Compare mutation rate schedules
- Measure: convergence speed, final performance
- Literature: evolutionary algorithms, simulated annealing

**Priority**: Medium

---

### 18. Dreaming Validation

#### 18.1 Sim-to-real transfer

**Question**: Do improvements from dreaming in the world model transfer to real-world performance? What's the correlation?

**Research directions**:
- Transfer measurement: compare simulated improvement with real improvement
- Factors affecting transfer: world model accuracy, mutation types, task type
- Negative transfer: can dreaming hurt real performance?

**Approaches**:
- Extensive sim-to-real experiments across tasks
- Develop predictive model of transfer success
- Literature: simulation-to-real transfer, domain adaptation

**Priority**: Critical

---

#### 18.2 Dreaming vs. real experience

**Question**: How many dreaming steps are equivalent to one real interaction in terms of learning?

**Research directions**:
- Exchange rate: dreaming steps per real step for equivalent improvement
- Task dependence: does exchange rate vary by task?
- Diminishing returns: does exchange rate change with skill level?

**Approaches**:
- Controlled experiments: compare learning curves with different dreaming/real ratios
- Literature: model-based RL sample efficiency

**Priority**: High

---

#### 18.3 Dreaming diversity

**Question**: How many dreaming simulations are needed to find meaningful improvements? Does diversity matter more than quantity?

**Research directions**:
- Diversity metrics: how to measure diversity of generated variations?
- Quantity vs. quality trade-off: is it better to dream many variations or few high-quality ones?
- Adaptive dreaming: can we focus dreaming on promising regions?

**Approaches**:
- Vary number of simulations and measure improvement
- Analyze relationship between diversity and improvement
- Literature: quality-diversity algorithms, novelty search

**Priority**: Medium

---

#### 18.4 Dreaming failure modes

**Question**: When does dreaming fail? What are the common failure modes?

**Research directions**:
- World model exploitation: does dreaming find loopholes that don't work in reality?
- Local optima: does dreaming converge to suboptimal behaviors?
- Destabilization: can dreaming cause previously good skills to degrade?

**Approaches**:
- Document failure cases from experiments
- Develop diagnostic tools to detect failure modes
- Literature: model-based RL pitfalls, safe exploration

**Priority**: High

---

## Part VII: Multi-Agent Emergent Properties

### 19. Measuring Emergence

#### 19.1 Adapting emergence metrics

**Question**: How can we adapt information-theoretic emergence metrics (from ) to Mycelium's continuous, real-time setting?

**Research directions**:
- Practical criterion adaptation: macro-level predictive information beyond individuals
- Emergence capacity: pairwise synergy measurement
- Coalition tests: higher-order coordination detection

**Approaches**:
- Implement metrics from  in Mycelium context
- Validate on controlled multi-agent experiments
- Literature: information decomposition, emergence quantification

**Priority**: High

---

#### 19.2 Real-time emergence detection

**Question**: Can we detect emergent properties in real-time as the swarm operates?

**Research directions**:
- Online information estimation: can we approximate emergence metrics without full history?
- Early warning signs: are there precursors to beneficial (or harmful) emergence?
- Visualization: how to make emergence visible to developers/users?

**Approaches**:
- Develop streaming approximations of emergence metrics
- Test on controlled emergence scenarios
- Literature: online learning, anomaly detection

**Priority**: Medium

---

#### 19.3 Emergence benchmarks

**Question**: What benchmark tasks can we design to reliably test for emergence in multi-agent systems?

**Research directions**:
- Tasks requiring coordination (like group guessing game from )
- Tasks with phase transitions (simple rules → complex behavior)
- Tasks with measurable synergy (joint information > sum of individuals)

**Approaches**:
- Design and validate benchmark tasks
- Share with research community for standardization
- Literature: multi-agent benchmarks, emergence evaluation

**Priority**: High

---

### 20. Steering Emergence

#### 20.1 Prompt-based steering

**Question**: Can we steer emergent properties through agent prompts, as demonstrated in ? What prompts work?

**Research directions**:
- Theory of Mind prompts: instructing agents to model others
- Persona prompts: assigning distinct identities/roles
- Goal articulation: how explicitly to state the shared goal

**Approaches**:
- Replicate  experiments in Mycelium context
- Test prompt variations; measure impact on emergence metrics
- Literature: prompt engineering, multi-agent coordination

**Priority**: High

---

#### 20.2 Architecture for emergence

**Question**: How does agent architecture affect emergence? What architectural choices promote beneficial emergence?

**Research directions**:
- Network complexity correlation (from ): more non-linearity → more complex emergence?
- Memory and recurrence: do agents need memory to coordinate?
- Communication channels: how does inter-agent communication affect emergence?

**Approaches**:
- Systematically vary agent architectures; measure emergence metrics
- Analyze relationship between architecture properties and emergence
- Literature: neural evolution, multi-agent systems

**Priority**: Medium

---

#### 20.3 Detecting harmful emergence

**Question**: How do we detect when emergent properties are harmful (e.g., agents colluding against user interests)?

**Research directions**:
- Alignment monitoring: can emergence metrics detect misalignment?
- Peer pressure detection (from ): when does group influence override individual judgment?
- Red teaming: what failure modes emerge in multi-agent systems?

**Approaches**:
- Design adversarial scenarios; measure emergence during failure
- Develop monitoring tools for harmful emergence
- Literature: AI safety, multi-agent alignment

**Priority**: High

---

### 21. Agent Differentiation

#### 21.1 Specialization emergence

**Question**: Under what conditions do agents naturally specialize into different roles?

**Research directions**:
- Environmental factors: what tasks promote specialization?
- Initialization: does diversity in initial agents matter?
- Feedback: what reward structures encourage differentiation?

**Approaches**:
- Long-term studies of agent behavior in stable environments
- Manipulate factors hypothesized to affect specialization
- Literature: division of labor, role emergence

**Priority**: Medium

---

#### 21.2 Measuring specialization

**Question**: How can we quantify how specialized an agent has become?

**Research directions**:
- Behavioral diversity: how different is this agent from others?
- Task focus: does agent succeed primarily on specific tasks?
- Representation analysis: do specialized agents develop distinct internal representations?

**Approaches**:
- Develop specialization metrics
- Validate against human judgment
- Literature: neural specialization, modularity

**Priority**: Medium

---

#### 21.3 Optimal specialization

**Question**: Is there an optimal level of specialization? Too little and agents are redundant; too much and they can't cover for each other.

**Research directions**:
- Trade-off analysis: specialization vs. robustness
- Adaptive specialization: should specialization increase or decrease over time?
- Task-dependent optimum: what level works best for different environments?

**Approaches**:
- Measure system performance across specialization levels
- Literature: multi-agent optimization, division of labor

**Priority**: Medium

---

## Part VIII: Training and Optimization

### 22. ROI-Based Prioritization

#### 22.1 ROI formula validation

**Question**: Does the proposed ROI formula (expected_improvement × frequency / cost) effectively prioritize the most valuable training tasks?

**Research directions**:
- Alternative formulations: weighted combinations, non-linear terms
- Empirical validation: compare ROI-prioritized training with alternatives
- Dynamic adjustment: should ROI weights change over time?

**Approaches**:
- Simulated training environments with known improvement potential
- Measure: overall learning rate, user satisfaction
- Literature: multi-armed bandits, resource allocation

**Priority**: High

---

#### 22.2 Expected improvement estimation

**Question**: How to accurately estimate expected improvement from training a skill or agent?

**Research directions**:
- Historical trend analysis: extrapolate from past improvements
- Similarity-based: use improvement of similar skills as proxy
- Uncertainty estimation: confidence intervals on improvement

**Approaches**:
- Develop and compare improvement predictors
- Validate against actual improvement after training
- Literature: learning curves, performance prediction

**Priority**: High

---

#### 22.3 Frequency measurement

**Question**: How to measure "frequency" in a way that captures both current and potential future usage?

**Research directions**:
- Recent frequency vs. all-time frequency
- Time-of-day patterns: should we weight by expected future usage?
- Context-dependent frequency: skill may be used only in certain contexts

**Approaches**:
- Analyze usage patterns; develop frequency models
- Test different frequency metrics in ROI formula
- Literature: time series analysis, predictive modeling

**Priority**: Medium

---

### 23. Local vs. Cloud Decision

#### 23.1 Cost estimation

**Question**: How to accurately estimate training cost (time, energy, cloud expense) for different tasks?

**Research directions**:
- Task-specific cost models: what predicts training cost?
- Hardware variation: how does cost vary across devices?
- Cloud provider dynamics: how to predict spot instance availability/price?

**Approaches**:
- Collect training cost data across tasks and hardware
- Develop predictive cost models
- Literature: cloud cost modeling, performance prediction

**Priority**: High

---

#### 23.2 Threshold determination

**Question**: What cost threshold should trigger cloud offloading? Should it be fixed or dynamic?

**Research directions**:
- User preferences: willingness to pay vs. wait
- Device state: battery, thermal, other usage
- Network conditions: bandwidth, latency, cost

**Approaches**:
- User studies on cloud offloading preferences
- Adaptive threshold algorithms
- Literature: edge-cloud offloading, computational offloading

**Priority**: Medium

---

#### 23.3 Privacy-cost trade-off

**Question**: How much privacy are users willing to trade for faster/better training? How to measure and communicate this trade-off?

**Research directions**:
- User valuation of privacy vs. performance
- Differential privacy parameters: what ε values are acceptable?
- Transparency: how to explain trade-offs to users?

**Approaches**:
- User studies with informed consent
- Measure willingness to enable cloud features at different privacy levels
- Literature: privacy economics, differential privacy

**Priority**: High

---

### 24. Predictive Wake-Up

#### 24.1 Prediction accuracy

**Question**: How accurately can we predict when a user will next use their device?

**Research directions**:
- Feature engineering: what predicts next use? (time of day, day of week, recent activity)
- Model comparison: simple heuristics vs. ML models
- Personalization: do prediction models need to be user-specific?

**Approaches**:
- Collect usage data; develop and compare prediction models
- Measure: prediction error, impact on training completion
- Literature: time series forecasting, human activity prediction

**Priority**: Medium

---

#### 24.2 Impact of missed predictions

**Question**: What happens when predictions are wrong? How to handle early or late wake-ups?

**Research directions**:
- Early wake-up: user returns before training complete → interrupt or continue?
- Late wake-up: training finishes too early → wasted idle time?
- Graceful degradation: can system continue training while user works?

**Approaches**:
- Simulate prediction errors; measure impact
- Design fallback strategies
- Literature: interruptible learning, progressive updates

**Priority**: Medium

---

#### 24.3 Learning improvement

**Question**: Does predictive wake-up actually improve user experience compared to fixed schedules?

**Research directions**:
- User satisfaction: do users notice/ appreciate timely updates?
- Training effectiveness: does completing training just before use improve performance?
- Battery impact: does predictive scheduling affect battery life?

**Approaches**:
- A/B test predictive vs. fixed schedule
- Measure: user satisfaction, task performance, battery drain
- Literature: user experience evaluation, scheduling algorithms

**Priority**: Medium

---

## Part IX: Privacy and Security

### 25. Seed Privacy

#### 25.1 Information leakage

**Question**: How much personal information can be inferred from a seed? Can seeds be reverse-engineered to reveal private data?

**Research directions**:
- Membership inference: can we tell if a specific user contributed to a seed?
- Attribute inference: can we extract personal characteristics from seeds?
- Reconstruction attacks: can we recover demonstration sequences from seeds?

**Approaches**:
- Design and execute privacy attacks on seeds
- Measure information leakage quantitatively
- Literature: privacy attacks on ML models, differential privacy

**Priority**: Critical

---

#### 25.2 Differential privacy for seeds

**Question**: Can we train seed encoders with differential privacy to limit information leakage? What privacy budget is feasible?

**Research directions**:
- DP-SGD for seed encoder training: implementation challenges
- Privacy-utility trade-off: how much does DP hurt seed quality?
- Per-instance DP: can we provide stronger guarantees for sensitive demonstrations?

**Approaches**:
- Implement differentially private seed encoder training
- Measure: privacy guarantees vs. seed quality
- Literature: differential privacy, private machine learning

**Priority**: High

---

#### 25.3 Seed anonymization

**Question**: Can seeds be anonymized post-hoc to remove identifying information while preserving functionality?

**Research directions**:
- Anonymization techniques: noise addition, dimension reduction, feature suppression
- Utility preservation: how much anonymization can seeds tolerate?
- Re-identification risk: can anonymized seeds be linked back to individuals?

**Approaches**:
- Develop and test anonymization methods
- Measure: privacy gain vs. functionality loss
- Literature: data anonymization, k-anonymity, l-diversity

**Priority**: Medium

---

### 26. Seed Security

#### 26.1 Seed authentication

**Question**: How can users verify that a seed came from a trusted source and hasn't been tampered with?

**Research directions**:
- Cryptographic signatures: feasibility of signing seeds
- Key management: how to distribute and verify public keys
- Trust chains: can seeds be signed by trusted third parties?

**Approaches**:
- Design seed signing and verification system
- Evaluate: computational overhead, usability
- Literature: digital signatures, public key infrastructure

**Priority**: High

---

#### 26.2 Malicious seeds

**Question**: What damage could a malicious seed cause? How to detect and prevent malicious seeds?

**Research directions**:
- Threat modeling: what attacks are possible? (data theft, system damage, privacy violation)
- Detection methods: can we automatically identify suspicious seeds?
- Sandboxing: can we safely test untrusted seeds in isolation?

**Approaches**:
- Develop threat models and attack scenarios
- Design seed vetting pipeline
- Literature: malware detection, sandboxing, threat modeling

**Priority**: Critical

---

#### 26.3 Seed provenance

**Question**: Can we track where a seed came from and how it has been modified?

**Research directions**:
- Provenance metadata: what information to track?
- Tamper-evident provenance: how to prevent forgery?
- Privacy-preserving provenance: can we track without revealing sensitive information?

**Approaches**:
- Design seed provenance system
- Evaluate: storage overhead, security properties
- Literature: provenance tracking, blockchain, supply chain security

**Priority**: Medium

---

### 27. System Security

#### 27.1 Agent isolation

**Question**: How to ensure that agents cannot harm the system or access unauthorized data?

**Research directions**:
- Sandboxing techniques: containers, virtual machines, capability-based security
- Permission systems: what granularity of permissions is needed?
- Resource limits: how to prevent DoS from buggy agents?

**Approaches**:
- Survey and adapt existing sandboxing technologies
- Design permission system for agents
- Literature: operating system security, capability-based security

**Priority**: Critical

---

#### 27.2 Inter-agent communication security

**Question**: How to secure communication between agents? Can malicious agents eavesdrop or inject messages?

**Research directions**:
- Encryption: should agent communication be encrypted?
- Authentication: how to verify agent identities?
- Access control: which agents can talk to which?

**Approaches**:
- Design secure communication protocol
- Evaluate: performance overhead, security guarantees
- Literature: secure multi-party communication, message authentication

**Priority**: High

---

#### 27.3 Update security

**Question**: How to securely update agents, world models, and other components? How to prevent malicious updates?

**Research directions**:
- Code signing: verifying authenticity of updates
- Update channels: secure distribution mechanisms
- Rollback protection: preventing downgrade attacks

**Approaches**:
- Design secure update pipeline
- Literature: software update security, code signing

**Priority**: High

---

## Part X: Evaluation and Metrics

### 28. System-Level Evaluation

#### 28.1 End-to-end benchmarks

**Question**: What benchmark tasks can evaluate the complete Mycelium system? How to measure success?

**Research directions**:
- Task suite: personal automation, development assistance, adaptive UI, etc.
- Metrics: task completion, speed, user satisfaction, learning rate
- Standardization: can we create benchmarks shared across research community?

**Approaches**:
- Design benchmark tasks covering key use cases
- Collect baseline performance data
- Literature: AI benchmarks, user studies

**Priority**: High

---

#### 28.2 Longitudinal studies

**Question**: How does Mycelium perform over months of use? Does it continue to improve? Does it plateau?

**Research directions**:
- Learning curves: measure performance over time
- Adaptation to changing user behavior: can system keep up?
- User retention: do users continue using the system?

**Approaches**:
- Long-term deployment studies with real users
- Measure: performance metrics, user engagement, satisfaction
- Literature: longitudinal HCI studies, continual learning evaluation

**Priority**: High

---

#### 28.3 Comparative evaluation

**Question**: How does Mycelium compare to alternative approaches (static software, traditional AI assistants, etc.)?

**Research directions**:
- Task performance comparison on common tasks
- User experience comparison: satisfaction, trust, perceived intelligence
- Resource comparison: computational cost, privacy, etc.

**Approaches**:
- Controlled experiments comparing Mycelium with alternatives
- Literature: comparative evaluation methodology

**Priority**: Medium

---

### 29. Component-Level Evaluation

#### 29.1 Ablation studies

**Question**: What is the contribution of each component to overall system performance? Which are essential?

**Research directions**:
- Systematic ablation: remove each component, measure performance drop
- Component interaction: do components interact positively or negatively?
- Minimal viable system: what's the smallest set that works?

**Approaches**:
- Perform ablation experiments on benchmark tasks
- Literature: ablation studies, feature importance

**Priority**: High

---

#### 29.2 Component replacement

**Question**: Can components be replaced with simpler alternatives without significant performance loss?

**Research directions**:
- Simpler alternatives: rule-based vs. learned, heuristics vs. optimization
- Performance gap: how much does simplicity cost?
- When complexity pays off: are there tasks where sophisticated components are necessary?

**Approaches**:
- Implement simpler alternatives for each component
- Compare performance across tasks
- Literature: simplicity vs. complexity trade-offs

**Priority**: Medium

---

#### 29.3 Parameter sensitivity

**Question**: How sensitive is system performance to component parameters? Which parameters need careful tuning?

**Research directions**:
- Sensitivity analysis: vary parameters, measure performance
- Robustness: can system work with poorly tuned parameters?
- Auto-tuning: can parameters be learned automatically?

**Approaches**:
- Systematic parameter sweeps
- Develop auto-tuning mechanisms
- Literature: sensitivity analysis, hyperparameter optimization

**Priority**: Medium

---

## Part XI: Human-AI Interaction

### 30. User Understanding

#### 30.1 Mental models

**Question**: What mental models do users form of Mycelium? Do they understand how it works?

**Research directions**:
- User interviews: how do users describe the system?
- Misconceptions: what do users get wrong?
- Training needs: what do users need to know to use it effectively?

**Approaches**:
- User studies with think-aloud protocols
- Surveys and interviews
- Literature: mental models, human-AI interaction

**Priority**: High

---

#### 30.2 Trust calibration

**Question**: Do users trust Mycelium appropriately? Over-trust? Under-trust?

**Research directions**:
- Trust measurement: questionnaires, behavioral measures
- Trust factors: what affects trust? (transparency, reliability, etc.)
- Trust calibration: can we help users develop appropriate trust?

**Approaches**:
- Longitudinal trust measurement
- Experiments manipulating system behavior, measuring trust
- Literature: trust in automation, human-AI trust

**Priority**: High

---

#### 30.3 Feedback effectiveness

**Question**: How effectively do users provide feedback to improve the system? What feedback mechanisms work best?

**Research directions**:
- Explicit feedback: thumbs up/down, corrections, demonstrations
- Implicit feedback: what user behaviors indicate satisfaction/dissatisfaction?
- Feedback fatigue: how much feedback are users willing to provide?

**Approaches**:
- Compare feedback mechanisms in controlled studies
- Measure: feedback quality, user effort, system improvement
- Literature: user feedback, interactive learning

**Priority**: High

---

### 31. Demonstration Interface

#### 31.1 Demonstration initiation

**Question**: How should users start and stop demonstrations? What's most natural?

**Research directions**:
- Voice commands: "watch me", "stop watching"
- UI controls: buttons, gestures
- Implicit boundaries: can system detect when demonstration starts/stops?

**Approaches**:
- User studies comparing initiation methods
- Measure: ease of use, error rate, user preference
- Literature: human-computer interaction, gesture interfaces

**Priority**: Medium

---

#### 31.2 Correction during demonstration

**Question**: How should users correct mistakes during demonstration? Undo? Override?

**Research directions**:
- Correction mechanisms: undo, redo, override, insert
- Learning from corrections: should system treat corrections as training data?
- User interface for correction: how to make it intuitive?

**Approaches**:
- Design and test correction interfaces
- Measure: correction accuracy, user effort
- Literature: interactive machine learning, correction interfaces

**Priority**: Medium

---

#### 31.3 Demonstration editing

**Question**: Can users edit demonstrations after capture? How?

**Research directions**:
- Timeline editing: trim, delete segments
- Parameter adjustment: modify action parameters
- Composition: combine multiple demonstrations

**Approaches**:
- Design demonstration editor
- User testing with editing tasks
- Literature: video editing, macro recording

**Priority**: Low

---

### 32. Transparency and Explanation

#### 32.1 Explanation generation

**Question**: How can Mycelium explain its decisions and behavior to users?

**Research directions**:
- Plinko path explanations: show what was considered and why
- Skill explanations: describe what a skill does
- Uncertainty communication: how to convey when system is uncertain

**Approaches**:
- Design explanation interfaces
- Evaluate: user understanding, trust, satisfaction
- Literature: explainable AI, interpretable ML

**Priority**: High

---

#### 32.2 Explanation effectiveness

**Question**: What kinds of explanations help users understand and trust the system?

**Research directions**:
- Explanation types: textual, visual, interactive
- Explanation depth: how much detail?
- Personalization: do different users need different explanations?

**Approaches**:
- Controlled experiments with explanation variations
- Measure: comprehension, trust, task performance
- Literature: XAI evaluation, user studies

**Priority**: Medium

---

#### 32.3 When to explain

**Question**: When should the system offer explanations? Proactively? On demand? Only when asked?

**Research directions**:
- Explanation timing: before action, after action, on request
- Explanation interruption: when do explanations disrupt workflow?
- Learn when to explain: can system predict when explanation is needed?

**Approaches**:
- Vary explanation timing; measure user experience
- Develop models of explanation need
- Literature: adaptive interfaces, interruption science

**Priority**: Medium

---

## Part XII: Deployment and Scaling

### 33. Resource Requirements

#### 33.1 Hardware requirements

**Question**: What hardware is needed to run Mycelium effectively? How does it scale with number of agents?

**Research directions**:
- CPU requirements: cores, speed
- Memory requirements: RAM for agents, buffers, models
- GPU requirements: when is acceleration needed?
- Storage requirements: logs, models, seeds

**Approaches**:
- Profile system on various hardware configurations
- Develop scaling models
- Literature: performance profiling, systems benchmarking

**Priority**: High

---

#### 33.2 Power consumption

**Question**: How much power does Mycelium consume? Can it run continuously on battery?

**Research directions**:
- Power profiling: measure consumption in different modes
- Optimization: can we reduce power without sacrificing performance?
- Adaptive power management: when to throttle?

**Approaches**:
- Measure power consumption on mobile devices
- Develop power optimization strategies
- Literature: green computing, mobile power management

**Priority**: High

---

#### 33.3 Scaling limits

**Question**: What are the scaling limits of the architecture? How many agents? How many skills? How much memory?

**Research directions**:
- Agent count scaling: performance vs. number of agents
- Skill library scaling: retrieval time vs. library size
- Memory scaling: memory usage vs. active agents and skills

**Approaches**:
- Stress testing: push system to limits
- Develop scaling models
- Literature: distributed systems scaling, performance engineering

**Priority**: Medium

---

### 34. Deployment Models

#### 34.1 Single-user deployment

**Question**: What's the optimal deployment for a single user on their personal device?

**Research directions**:
- Installation: how to make installation easy?
- Configuration: what should be configurable?
- Updates: how to handle updates without disruption?

**Approaches**:
- Design deployment package
- User testing with installation and setup
- Literature: software deployment, user onboarding

**Priority**: High

---

#### 34.2 Multi-user deployment

**Question**: Can Mycelium support multiple users on the same device? How to handle user separation?

**Research directions**:
- User profiles: separate agent swarms per user?
- Shared vs. private skills: which skills can be shared?
- Privacy: ensuring users can't access each other's data

**Approaches**:
- Design multi-user architecture
- Security and privacy analysis
- Literature: multi-user systems, access control

**Priority**: Medium

---

#### 34.3 Server deployment

**Question**: Can Mycelium be deployed on servers to serve multiple clients? What changes are needed?

**Research directions**:
- Client-server architecture: how to partition functionality?
- Scaling: handling many concurrent users
- Privacy: what data must stay on client vs. can go to server?

**Approaches**:
- Design server deployment architecture
- Load testing
- Literature: client-server systems, cloud computing

**Priority**: Low

---

## Part XIII: Long-Term Evolution

### 35. Self-Improvement

#### 35.1 Recursive self-improvement

**Question**: Can Mycelium improve its own architecture? Could it design better agents, skills, or dreaming strategies?

**Research directions**:
- Meta-learning: learning to learn
- Architecture search: can system discover better architectures?
- Recursive improvement: what prevents runaway improvement?

**Approaches**:
- Design meta-learning experiments
- Literature: meta-learning, neural architecture search, recursive self-improvement

**Priority**: Low (long-term)

---

#### 35.2 Skill evolution over generations

**Question**: How do skills evolve as they are shared, modified, and recombined across users?

**Research directions**:
- Skill lineages: track skill ancestry
- Innovation: do recombinations produce novel, useful skills?
- Convergence: do skills converge to optimal forms?

**Approaches**:
- Simulate skill evolution in multi-user environment
- Analyze skill lineages
- Literature: cultural evolution, genetic algorithms

**Priority**: Low (long-term)

---

#### 35.3 Emergent protocols

**Question**: Will agents develop their own communication protocols or conventions over time?

**Research directions**:
- Communication emergence: under what conditions do agents develop language?
- Protocol evolution: can communication protocols become more efficient?
- Human understanding: can humans understand emergent protocols?

**Approaches**:
- Long-term multi-agent experiments with communication channels
- Analyze emergent communication
- Literature: emergent communication, language evolution

**Priority**: Low (long-term)

---

### 36. Ecosystem

#### 36.1 Skill marketplace dynamics

**Question**: If a skill marketplace emerges, what economic dynamics will it have? How to design for healthy ecosystem?

**Research directions**:
- Pricing: how should skills be priced?
- Quality signals: how to communicate skill quality?
- Discovery: how do users find useful skills?
- Incentives: how to reward skill creators?

**Approaches**:
- Simulate marketplace dynamics
- Literature: platform economics, two-sided markets

**Priority**: Low (long-term)

---

#### 36.2 Skill composability

**Question**: Will users naturally compose skills to create new behaviors? What makes skills composable?

**Research directions**:
- Composability factors: interface standardization, modularity
- Composition patterns: what compositions are common?
- Emergent complexity: do compositions lead to unforeseen behaviors?

**Approaches**:
- Analyze skill usage in multi-user deployment
- Design for composability
- Literature: modular design, component-based software

**Priority**: Low (long-term)

---

#### 36.3 Community knowledge

**Question**: Can a community of users collectively build knowledge that exceeds any individual's?

**Research directions**:
- Collective skill library: does shared skill repository improve over time?
- Diversity benefits: do diverse user bases produce more robust skills?
- Coordination: how to coordinate collective skill development?

**Approaches**:
- Community platform design and study
- Literature: collective intelligence, open source communities

**Priority**: Low (long-term)

---

## Appendix: Research Methods Reference

### Recommended methodologies by question type

| Question Type | Recommended Methods |
|---------------|---------------------|
| **Architecture comparison** | Controlled experiments with multiple implementations; measure performance metrics |
| **Parameter optimization** | Grid search, Bayesian optimization, random search |
| **User behavior** | User studies, surveys, interviews, log analysis |
| **Theoretical limits** | Information theory, complexity theory, mathematical analysis |
| **Emergent properties** | Longitudinal observation, information-theoretic measurement, controlled perturbations |
| **Privacy/security** | Attack simulations, threat modeling, formal verification |
| **Scaling** | Load testing, performance profiling, modeling |
| **Long-term evolution** | Simulation, agent-based modeling, field studies |

---

## Conclusion

This research agenda represents the questions we must answer to make Mycelium a reality. Some questions have clear paths to answers through existing literature and well-designed experiments. Others open entirely new research directions that may occupy us for years.

The agenda is intentionally ambitious. We will not answer all questions—certainly not before our first release. But by identifying what we don't know, we can make informed decisions about where to focus, what to simplify, and what to leave for future work.

As we build, we will discover questions we haven't thought to ask. This document will evolve with us.

---

*This research agenda is a living document. To contribute, visit [github.com/superinstance/mycelium/research](https://github.com/superinstance/mycelium/research).*
