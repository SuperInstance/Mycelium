# The Mycelium Lexicon

## A Vocabulary for Living Intelligence

**Version 7.0 — June 2026**  
**SuperInstance Open Source Initiative**

*A complete guide to the concepts, terms, and language of agent‑native, self‑optimizing systems built on the Learned Optimization Graph (LOG) architecture.*

---

## Prologue: The Garden of Thought

Before you read this document, consider how you learned language.

You didn't start with dictionaries. You started with stories. Someone pointed at a tree and said "tree." You saw it, you heard it, you understood. Later you learned that trees have roots, trunks, branches, leaves. Each new word built on the last, and soon you could talk about forests.

This lexicon works the same way.

We're going to build an understanding of Mycelium layer by layer. Each term introduces one idea, and later terms build on it. By the end, you'll have a complete mental model—not just a list of definitions, but a connected understanding of how this system works and why it matters.

The language we've created is designed to be:
- **Intuitive enough** that you can guess meanings from context.
- **Precise enough** that engineers can implement from these descriptions.
- **Inspiring enough** that you'll want to be part of what comes next.

If you're new here, start at the beginning and read straight through. The story unfolds in order.

If you're returning, use the quick reference at the end. But even then, I encourage you to reread the explanations. Words change as systems grow, and the latest version may surprise you.

Let's begin.

---

## Part I: The Soil — Foundational Concepts

Every forest needs soil. These are the basic ideas everything else grows from.

---

### Mycelium
*Noun.* /mīˈsēlēəm/

**The overarching architecture and open‑source project.** Named for the hidden fungal networks that connect trees into a single, intelligent organism.

**What it is:** Mycelium is a complete system for building, running, and continuously improving agent‑native applications. It provides the runtime, the learning mechanisms, the communication protocols, and the vocabulary for creating software that grows with its users.

**The metaphor:** In a forest, fungal mycelia weave between tree roots, creating a network that shares water, nutrients, and warnings. The forest functions as a unified intelligence without a central brain. Damage one part; the rest adapts. Most of the work is invisible; what we see—mushrooms—are just the fruiting bodies.

Mycelium.ai embodies this. Your personal swarm of agents operates mostly invisibly, learning from your behavior, sharing insights across the network, and fruiting only when it has something to show you—a suggestion, an automation, a new capability.

**Why this name:** It's a constant reminder that intelligence need not be monolithic. The most robust, adaptive systems in nature are decentralized networks. Your Mycelium instance is a forest, and you are its gardener.

**Research note:** Fungal networks have been studied as models for distributed intelligence in fields from ecology to computer science. Work by Fricker et al. (2017) on decision-making in mycelial networks shows how local rules produce global optimization, directly inspiring our approach to emergent agent coordination.

**Competitive landscape:** While other platforms use terms like "ecosystem" or "orchestration," "mycelium" uniquely captures the hidden, connective, and resilient nature of our architecture. It's not just a network; it's a living network.

---

### Agent
*Noun.* /ˈājənt/

**A specialized, autonomous process that performs a narrow function within the larger swarm.** Agents are the nodes of the Mycelium network.

**What it is:** An agent is not intelligent by itself. It does one thing well. A **vision agent** identifies objects in images. A **text agent** understands intent from language. A **context agent** tracks time, location, and state. An **executor agent** performs actions in the world.

Each agent contains a tiny neural model—typically 1 to 100 million parameters, small enough to run continuously on your device. It consumes information from specific sources (topics), processes it, and writes proposals about what should happen next.

Agents are like neurons. A single neuron cannot think; a hundred billion of them, connected in the right way, can write poetry.

**Why this term:** "Agent" carries the right weight—autonomy, purpose, action. It's familiar from AI literature, but here it's grounded. You can point to an agent in the code, watch it work, see how it connects to others.

**User story:** "My fishingLOG has a water temperature agent that tracks conditions automatically while I fish. I don't have to think about it."

**Technical note:** Agents learn from experience. Their internal models can be fine‑tuned overnight. Their sense of how valuable their actions are (their "value function") updates with every success and failure. They are not static; they grow.

**Research note:** The concept of specialized agents dates back to Minsky's "Society of Mind" (1986). Modern multi‑agent systems (MAS) research, such as Stone and Veloso (2000), emphasizes the importance of agent specialization for complex tasks. Our agents are distinguished by their continuous learning and dynamic connectivity.

---

### Swarm
*Noun.* /swôrm/

**The collection of all active agents in a Mycelium instance.** A swarm is what's running right now.

**What it is:** When you open your laptop in the morning, a swarm wakes up. Dozens or hundreds of agents begin processing: vision agents watching your screen, audio agents listening for cues, context agents tracking your calendar, intent agents forming hypotheses about what you might need.

The swarm is not a list; it's a living system. Agents are loaded and hibernated based on what you're doing. New agents can be recruited when you encounter something novel. Connections between agents strengthen and weaken as patterns emerge.

**Why this term:** "Swarm" evokes multiplicity, coordination, and emergent behavior. A swarm of bees has no leader, yet it finds food, builds hives, and defends itself. A swarm of agents has no single controller, yet it learns, decides, and acts.

**Analogy:** A forest's mycelial network is a swarm of threads. You can't see most of it, but you can see what it produces.

**Research note:** Swarm robotics and swarm intelligence have been extensively studied (Bonabeau, Dorigo, Theraulaz 1999). Key principles include decentralization, local interactions, and emergence—all central to Mycelium's design.

---

### Graph
*Noun.* /ɡraf/

**The underlying structure of the Mycelium system.** A graph is a way of representing connections.

**What it is:** In mathematics, a graph has:
- **Nodes** — things (in Mycelium, these are agents).
- **Edges** — connections between things (communication channels).
- **Weights** — strengths of those connections (how much influence one agent has on another).

The Mycelium graph is the complete map of how agents are connected. It's both the architecture (who talks to whom) and the knowledge (what those connections mean). A strong edge from agent A to agent B means "when A has something to say, B should pay attention." A cluster of tightly connected agents means "these agents often work together."

The graph is not static. It learns, prunes, and grows—just like biological neural networks.

**Why this term:** "Graph" is mathematically precise and visually intuitive. Everyone understands nodes and edges. And unlike a neural network's inscrutable weights, a graph can be drawn. You can see your agent network, understand it, trust it.

**Analogy:** A city's road network. Roads form where traffic flows, widen with use, narrow when unused. New roads are built when patterns demand them. The network adapts to the needs of its inhabitants.

**Technical note:** The graph is represented as a sparse matrix of synaptic weights, updated via reward‑modulated Hebbian learning.

---

### LOG (Learned Optimization Graph)
*Noun.* /läɡ/ *Acronym.* /el-ō-jē/

**The core architectural principle and platform brand.** LOG stands for Learned Optimization Graph.

**What it means, piece by piece:**

- **Learned:** Nothing in this system is programmed in the traditional sense. You don't write code to tell it what to do. You demonstrate. The system watches, captures what you do, and learns patterns. It builds understanding from observation.
- **Optimization:** Learning alone is not enough. The system actively improves itself. It dreams at night, simulating millions of variations to find better ways. It prunes connections that aren't useful and grows new ones that might be. It learns from the entire user population (anonymously) to benefit from collective wisdom.
- **Graph:** Everything is represented as a graph. Agents are nodes. Connections are edges. Knowledge is in the structure. The graph is both what the system knows and how it's organized.

**Why this word:** "Log" is one of the most beautiful double entendres in our lexicon. Consider:

- A **log** is a record — the raw material of learning. Ship captains kept logs to navigate by past experience. Scientists log experiments to refine hypotheses. You log your fishing trips, your study sessions, your business meetings.
- A **log** is a piece of a tree — connecting directly to the mycelium metaphor. Logs come from forests; LOG comes from Mycelium.
- A **log** is the base of a logarithm — hinting at the mathematical compression that turns raw sequences into compact seeds.

When you say "fishingLOG," you mean both "a fishing log that records your trips" and "a fishing application built on the Learned Optimization Graph architecture." The user gets the familiar meaning; the developer gets the technical precision. Everyone is correct.

**Tagline:** Your personal learned optimization graph.

**Competitive landscape:** Other platforms use terms like "personal AI" or "assistant," but none capture the dual essence of learning and optimization in a graph structure. LOG positions us uniquely.

---

### Logos
*Noun.* /ˈlōˌɡäs/ *plural:* logoi /ˈlōˌɡoi/

**The emergent intelligence of your whole system.** The thing that makes it feel like a partner rather than a tool.

**What it is:** After you've used Mycelium for a while—weeks, months, years—something happens. The system starts to feel like it *knows* you. It anticipates what you need. It suggests things you hadn't thought of. It adapts to your style, your habits, your quirks.

This is your LOGOS. It's not a component you can point to. It's not in any single agent. It's what emerges from the whole—the accumulated wisdom of all your logs, optimized through dreaming, organized through the graph, expressed through behaviors.

The LOGOS is characterized by:
- **Understanding:** The system seems to grasp your intentions, not just your actions.
- **Anticipation:** It knows what you'll need before you ask.
- **Style:** It adapts to your unique way of doing things.
- **Trust:** You rely on it; it rarely lets you down.

**Why this term:** In ancient Greek philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Heraclitus said the Logos is common to all, yet most live as if they had private understanding. Your personal LOGOS is the rational structure underlying your digital life.

The word also plays beautifully with "log." Logos contains "log"—suggesting that from many logs, a coherent intelligence emerges.

**User story:** "My fishingLOG has developed its own logos. It doesn't just record my trips—it seems to *understand* fishing. Sometimes it suggests things I hadn't thought of, and they work. It's like having a partner who knows me."

**Research note:** The concept of emergent intelligence is studied in complex systems and cognitive science. Work by Holland (1998) on emergence and by Clark (2003) on extended mind provides theoretical grounding for the idea that intelligence can reside in the interaction between user and system.

---

## Part II: The Roots — What You Capture

Now that we understand the soil—the agents, the swarm, the graph, the LOG—let's talk about what grows from it. These are the things you create, capture, and cultivate.

---

### Log
*Noun.* /lôɡ/ *Verb.* /lôɡ/

**A record of an event or sequence of actions.** Logs are the raw material from which intelligence is refined.

**What it is:** Every time you interact with a LOG application, it logs what happened. When you fish, it logs location, weather, bait, catch. When you study, it logs subject, duration, focus level, test scores. When you work, it logs meetings, emails, decisions, outcomes.

These logs are not just data; they're experience. They're what the system uses to learn.

**As a verb:** "Log this" tells the system to watch and learn. You perform a behavior once, and the system captures it—the sequence, the context, the result. Later, that behavior becomes a reusable pattern.

**Why this term:** As discussed, "log" carries centuries of meaning. It's the word humans have always used for recording experience. We're just making it alive.

**User story:** "Every time I fish, fishingLOG logs my trips. After a few weeks, it starts noticing patterns I hadn't seen—the bait that works best at this lake, the time of day the bass are active."

**Technical note:** Logs are stored compressed in the logbook. Raw sensor data is encoded into latent vectors before storage, reducing size by ~90% while preserving semantic information.

---

### Logline
*Noun.* /ˈlôɡˌlīn/

**A compressed representation of a behavioral pattern.** A logline is what you get when the system has learned something.

**What it is:** When the system has seen a behavior enough times—or when you explicitly demonstrate it—it distills that behavior into a logline. The logline is not the raw sequence; it's the *essence*. It captures what matters about the behavior while discarding what's incidental.

Technically, a logline is a vector—typically 64 to 1024 floating‑point numbers. That's it. A few hundred bytes that encode a complex behavior. A fishing technique. A study routine. A business workflow.

Loglines are:
- **Portable:** You can share them, sell them, gift them. A logline is small enough to email.
- **Private:** They encode patterns, not raw data. Share a logline without sharing your personal information.
- **Composable:** Loglines can be combined. Like mixing colors, you can create new behaviors from old ones.
- **Optimizable:** They improve over time. Last year's logline may be better this year, after dreaming.

**Why this term:** In Hollywood, a logline is a one‑sentence summary of a movie—enough to know whether you're interested. "A shy teenager discovers he has superpowers and must save his city from a villain." That's a logline. It captures the essence.

Same here. A logline captures the essence of a behavior.

**User story:** "After three successful fishing trips, fishingLOG created a logline for 'cloudy day bass fishing'. I can share it with my friends, and they can use it on their own fishingLOG. They don't need to know the details; the logline contains everything that matters."

**Technical note:** Loglines are generated by the Behavioral Embedding Space (BES) encoder. They are the primary unit of exchange in the ecosystem.

---

### Logbook
*Noun.* /ˈlôɡˌbo͝ok/

**Your personal long‑term memory.** A database containing all your logs and loglines.

**What it is:** Everything you've ever done with your LOG applications lives here. Every fishing trip. Every study session. Every business meeting. Every pattern the system has discovered. All stored, indexed, searchable.

The logbook is:
- **Private:** It lives on your device by default. You control what leaves.
- **Searchable:** You can find past experiences by similarity. "Show me fishing trips like this one."
- **Ever‑improving:** Old loglines can be refined by new experiences. The logbook is not static; it evolves.
- **Portable:** Take your logbook to a new device. Your intelligence moves with you.

**Why this term:** Ships' captains kept logbooks—bound volumes of their voyages, filled with observations, measurements, and lessons learned. They were priceless. Lose your logbook, lose your experience.

Your digital logbook is the same, but it learns.

**User story:** "My studyLOG logbook contains every course I've ever taken. When I start a new subject, it searches for loglines from similar topics and suggests techniques that worked before."

**Technical note:** The logbook is implemented as a local vector database (ChromaDB or LanceDB). Each entry consists of an embedding, metadata, and optional raw data for debugging.

---

### Loom
*Noun.* /lo͞om/

**A reusable, optimized routine discovered from your logs.** (Formerly called "logarithm," but we found that word hard to say. "Loom" flows better.)

**What it is:** A loom is a pattern that has been woven into something reusable. It's the "muscle memory" of the system—common sequences that have been compressed and refined to the point where they execute automatically.

Unlike traditional algorithms, which are written in code, looms are:
- **Learned from demonstration** (not programmed).
- **Continuously optimized** through dreaming.
- **Personalized** to your specific style.
- **Shareable** as loglines.

**Why this term:** A loom is a device for weaving thread into fabric. Threads alone are just strands; woven together, they become something strong and useful. Your logs are threads. A loom weaves them into something you can use.

Also: "loom" is easy to say. It flows. "I used a fishing loom." "The system discovered a new study loom." Try it—it works.

**User story:** "PlayerLOG discovered a loom for my fighting game combo. Now when I'm in the right situation, it executes automatically—faster than I could react."

**Technical note:** Looms are stored as loglines plus metadata about when and how to invoke them. They may also include a small recurrent network that generates the action sequence when triggered.

---

### Loomery
*Noun.* /ˈlo͞omərē/

**A collection of looms, organized by purpose or domain.** Your personal library of reusable routines.

**What it is:** Just as a library organizes books, your loomery organizes looms. Fishing looms in one section. Study looms in another. Business looms in another. You can browse, search, and curate.

**Why this term:** It's where looms live. Simple, clear, evocative.

**User story:** "My fishing loomery has dozens of techniques I've collected over the years—some I discovered myself, some I got from the grove, some I bought from the marketplace. I can browse them by season, by fish type, by location."

**Analogy:** Think of a physical loomery as a workshop where looms are stored and maintained. Your digital loomery is the same.

---

### Loomcast
*Noun.* /ˈlo͞omˌkast/

**A shareable loom.** Like a podcast, but for behaviors.

**What it is:** When you've developed a technique that works, you can package it as a loomcast. Add metadata, a description, tags, maybe a price. Share it with your grove or the whole marketplace.

Loomcasts can be:
- **Subscribed to** (like a podcast feed—new looms arrive automatically).
- **One‑time purchases** (like an app—buy once, use forever).
- **Community‑rated** (like reviews—find the best ones).
- **Anonymized** (privacy‑preserving—no personal data).

**Why this term:** Podcasts are broadcasts you can listen to anytime. Loomcasts are behaviors you can run anytime. The parallel is intentional.

**User story:** "I subscribe to a pro angler's loomcast. Every week, I get new fishing techniques optimized for my local waters. Last week's loomcast doubled my catch rate."

**Technical note:** Loomcasts are distributed via the marketplace protocol, which includes cryptographic signatures for authenticity and optional micropayments.

---

## Part III: The Trunk — How It Works

Now we understand the soil (agents, swarm, graph) and the roots (logs, loglines, looms). Let's climb the trunk—the core mechanisms that make everything work.

---

### Plinko
*Noun.* /ˈpliNGkō/

**The decision layer that chooses among competing agent proposals.** Named for the game where a chip bounces through pegs to land in a slot.

**What it is:** At any moment, multiple agents may have ideas about what should happen next. The vision agent sees a button and thinks "click that." The intent agent, based on context, thinks "maybe wait." The safety agent thinks "definitely don't click that."

Plinko decides who wins.

Here's how it works, step by step:

1. **Agents bid.** Each agent estimates how valuable its proposed action would be. This is learned from experience—agents that propose good things get rewarded; agents that propose bad things get penalized.

2. **Discriminators adjust.** Safety, coherence, and timing filters adjust the bids up or down. A great action that's unsafe gets killed. A mediocre action that's perfectly timed gets a boost.

3. **Noise adds exploration.** Sometimes the system needs to try things that aren't the highest bid, just to see if they might be better. Gumbel noise (a specific kind of randomness) occasionally lets lower‑value actions win.

4. **Temperature controls randomness.** When the system is uncertain—when agents disagree, when entropy is high—temperature rises, encouraging more exploration. When it's confident, temperature drops, favoring exploitation.

The result is a principled way to choose among agents that balances doing what works (exploitation), trying new things (exploration), and staying safe.

**Why this term:** The visual is perfect. Proposals enter at the top, bounce through discriminators and noise, and eventually emerge as a selected action. The path is stochastic but not random, shaped by the structure it passes through.

**User story:** "Sometimes my businessLOG does something unexpected—opens an app I don't usually use at that time. That's Plinko exploring. Usually it's wrong, but sometimes it discovers something useful."

**Research note:** The use of Gumbel‑Softmax for differentiable sampling is standard in reinforcement learning (Jang et al. 2016). Adaptive temperature based on entropy is inspired by work on curiosity‑driven exploration (Pathak et al. 2017). The combination with discriminators is novel.

---

### World Model
*Noun.* /wərld ˈmäd(ə)l/

**A learned simulator that predicts how the environment will respond to actions.** The world model is what makes dreaming possible.

**What it is:** If you click this button, what happens? If you type this text, how does the app respond? If you cast here, will the fish bite? The world model knows—or at least, it has learned to predict.

The world model is trained on your actual logs. It watches what happens when you take actions, and it builds an internal model of cause and effect. Over time, it becomes a pretty good simulator of your digital environment.

This simulator isn't perfect—no model is—but it's good enough to be useful. Good enough to let the system dream.

The world model consists of:
- **Encoder:** Compresses observations into a latent state.
- **Transition model:** Predicts next state given current state and action.
- **Reward model:** Predicts how satisfied you'll be with the outcome.
- **Decoder:** Reconstructs observations (optional, for visualization).

**Why this term:** It's a model of your world. Simple, direct, accurate.

**Research note:** World models are a key component in model‑based reinforcement learning, popularized by Ha and Schmidhuber (2018) and extended in Dreamer (Hafner et al. 2019). Our contribution is applying them to personal digital environments and using them for skill dreaming.

---

### Dreaming
*Verb.* /ˈdrēmiNG/ *Noun.* /ˈdrēmiNG/

**The overnight process where the system improves itself through simulation.** While you sleep, Mycelium dreams.

**What it is:** Dreaming works like this:

1. The system takes your looms—the routines you've taught it.
2. It creates variations. Slight tweaks. Small changes. Combinations with other looms.
3. It runs these variations through the world model, simulating what would happen.
4. It keeps the variations that lead to better predicted outcomes.
5. By morning, your looms are slightly better than they were the night before.

Dreaming happens at multiple scales:
- **Micro‑dreams** refine fine motor skills (typing speed, casting accuracy, mouse precision).
- **Meso‑dreams** optimize routine sequences (email triage, fishing preparation, meeting facilitation).
- **Macro‑dreams** combine looms to create new behaviors (merging fishing and weather prediction, blending study and sleep schedules).

**Why this term:** Just as humans consolidate memories and rehearse skills during sleep, Mycelium dreams to get better while you rest. The metaphor is both intuitive and scientifically grounded—research shows that dreaming in latent spaces enables more efficient learning.

**User story:** "I noticed my fishingLOG has been getting smarter each week. It's not just logging anymore—it's suggesting things I hadn't thought of. That's dreaming at work."

**Research note:** The concept of dreaming in AI is explored in "Dream to Control" (Hafner et al. 2020) and "Neuromorphic Dreaming" (Blakowski et al. 2024). Our multi‑scale dreaming is inspired by the stages of human sleep and the need to optimize at different temporal granularities.

---

### Looming
*Verb.* /ˈlo͞omiNG/

**The process of weaving logs into looms.** When the system discovers a recurring pattern in your logs, it "looms" them—compresses them into a reusable routine.

**What it is:** Looming happens automatically. The system watches for sequences that occur frequently. When it finds one, it extracts it, compresses it, and adds it to your loomery.

You can also loom explicitly. When you perform a new behavior and want to save it, you tell the system "loom this." It captures the demonstration and adds it to your collection.

**Why this term:** It's the verb form of "loom." Simple and natural.

**User story:** "I've been using the same morning routine for weeks. This morning, fishingLOG told me it had loomed my routine—now I can just say 'morning routine' and it happens automatically."

**Technical note:** Looming uses the Skill Chunker component, which employs grammar induction to find natural boundaries in sequences.

---

### Weaving
*Verb.* /ˈwēviNG/

**Combining multiple looms to create new behaviors.** Weaving is how the system innovates.

**What it is:** Take the "early morning" loom from fishing and the "cloudy day" loom from another context, weave them together, and you get a new pattern for overcast dawns. The result is something neither original contained—something new.

Weaving can happen automatically through dreaming, or you can guide it explicitly. "Try weaving my casting loom with my weather prediction loom."

**Why this term:** You're weaving together different threads to create something new, like weaving threads into fabric. The metaphor is consistent and intuitive.

**User story:** "The system wove my 'early morning' loom with my 'cloudy day' loom to create a new pattern for overcast dawns. I'd never have thought to combine them, but it works."

**Technical note:** Weaving is implemented as interpolation in the Behavioral Embedding Space (BES) or as grammar recombination.

---

### Pruning
*Noun.* /ˈpro͞oniNG/

**Removing weak or unused agent connections.** Pruning keeps the graph lean and efficient.

**What it is:** Over time, some connections prove useless. Maybe they were tried and didn't help. Maybe they were useful once but aren't anymore. These connections are noise—they consume resources and can interfere with good ones.

Pruning identifies connections whose synaptic weights have fallen below a threshold for an extended period and removes them entirely. The graph becomes sparser, more efficient, more focused.

**Why this term:** A gardener prunes a tree—removing dead branches so the living ones thrive. The system prunes its graph for the same reason.

**Analogy:** Think of a tree in spring. Dead branches are pruned so nutrients go to living ones. The tree becomes healthier, more productive. Same here.

**Research note:** Synaptic pruning is a well‑established phenomenon in neuroscience (Huttenlocher 1979). In machine learning, it's analogous to weight decay and network pruning techniques. Our approach is inspired by biological pruning but adapted to a dynamic, multi‑agent context.

---

### Grafting
*Noun.* /ˈɡraftiNG/

**Forming new agent connections when patterns suggest they would be useful.** Grafting enables the graph to adapt to new tasks.

**What it is:** Sometimes two agents are frequently active around the same time, in successful sequences, but they're not directly connected. Their communication has to go through intermediaries, which is slower and less direct.

When the system detects this pattern—repeated co‑activation without direct connection—it may graft a new edge directly between them. The new connection starts with a small weight, which can then strengthen through use.

**Why this term:** In orchards, grafting joins a fruit‑bearing branch to a hardy rootstock. The result is stronger than either alone. Grafting does the same for agents.

**User story:** "My fishingLOG's weather agent and location agent were often both active, but they weren't connected. The system grafted a direct connection, and now they share information instantly."

**Technical note:** Grafting candidates are identified through co‑activation analysis. A new edge is initialized with a small weight and then subject to normal plasticity.

---

### Clustering
*Noun.* /ˈkləstəriNG/

**The self‑organization of agents into functional groups.** Using mathematical techniques on the log graph, agents naturally form teams that work well together.

**What it is:** In any complex system, specialization emerges. Some agents work together on vision tasks. Others collaborate on language. Others coordinate actions. These groupings aren't programmed—they emerge from patterns of successful interaction.

Clustering identifies these natural groups. Once identified, the system can optimize within groups (faster, richer communication) and between groups (sparser, higher‑level coordination).

**Why this term:** Agents cluster based on their roles, just as neurons in the brain form functional columns.

**Analogy:** In a soccer team, defenders cluster together, forwards coordinate, but clusters shift as the game evolves. A player might be primarily a defender but join the attack on a corner kick. Same here—agents have primary clusters but can form temporary alliances.

**Research note:** Spectral clustering on graphs is a standard technique (von Luxburg 2007). Our innovation is applying it dynamically to an evolving agent graph to discover functional groupings in real time.

---

### Synaptic Weight
*Noun.* /səˈnaptik wāt/

**The strength of a connection between two agents.** Synaptic weights determine how much influence one agent has on another.

**What it is:** When agent A sends a message, it doesn't go directly to agent B's input. It goes through a weighted connection. If the weight is high (close to 1.0), the message has strong influence. If the weight is low (near 0), it has weak influence. If the weight is zero, the connection might as well not exist.

Synaptic weights change over time:
- **Increase** when the connection is used in successful sequences.
- **Decrease** when used in failures or not used at all.
- **Prune** when they fall below a threshold.
- **Initialize** when new connections form.

**Why this term:** Directly analogizes to biological synapses, which strengthen with use and weaken with disuse. The metaphor is exact.

**Analogy:** Like muscles. Use a connection, it gets stronger. Don't use it, it atrophies. The system is constantly exercising its graph.

---

### Topology Seed
*Noun.* /təˈpäləjē sēd/

**A compact representation of a learned agent configuration.** The nodes, edges, and weights that define a successful collaboration pattern.

**What it is:** Just as a logline captures a behavior, a topology seed captures an *organization*. It answers: For this kind of task, which agents should be connected, and how strongly?

Topology seeds enable:
- **Sharing** proven configurations (like a template for how agents should connect).
- **Transfer** across users (benefiting from how others organize).
- **Evolution** through recombination (creating new configurations).
- **Instant deployment** (load a topology seed and your swarm reorganizes).

**Why this term:** Just as a seed contains the blueprint for a plant, a topology seed contains the blueprint for an agent organization. Plant the seed, grow the graph.

**User story:** "I downloaded a topology seed from a power user that optimizes my businessLOG for morning productivity. Now my agents are organized perfectly at 8am—email agents connected to calendar agents, task agents listening to both. It's like having a professional organizer for my digital life."

**Technical note:** Topology seeds encode the graph structure (compressed adjacency matrix), synaptic weights, agent type references, and a context signature.

---

## Part IV: The Forest — Collective Intelligence

No tree grows alone. These terms describe how individual Mycelium instances connect into a larger intelligence.

---

### Federated Learning
*Noun.* /ˈfedəˌrādid ˈlərniNG/

**The process of sharing anonymized patterns across the user population to improve collective intelligence.** The system learns from everyone while protecting everyone.

**What it is:** No user is an island. The patterns that work for one person might work for another. Federated learning allows the system to benefit from the whole population while keeping individual data private.

Only anonymized patterns are shared—loglines and topology seeds, not raw logs. These are aggregated using techniques that prevent identifying individuals. The result is a collective intelligence that benefits everyone without compromising anyone.

Federated learning:
- **Respects privacy** (only patterns, never raw data).
- **Accelerates learning** (new users benefit from the crowd).
- **Discovers universals** (patterns that work for everyone).
- **Enables personalization** (local fine‑tuning on shared foundations).

**Why this term:** "Federated learning" is the established term for privacy‑preserving cross‑device learning. We use it because it's precise and because the concept is already known.

**Research note:** Federated learning was introduced by McMahan et al. (2017). Our extension to learning topologies and loglines is novel and builds on work like FedAvg and secure aggregation.

---

### Grove
*Noun.* /ɡrōv/

**A community of users who share looms and topology seeds.** Like a book club, but for behaviors.

**What it is:** People who share interests form groves. Fly fishers have one. Organic chemistry students have another. Chess players have another. Within a grove, members share looms they've found effective, rate each other's contributions, and collectively improve their craft.

Groves can be public or private, moderated or free‑form. They are the social fabric of the LOG ecosystem.

**Why this term:** A grove is a small group of trees—a community within the larger forest. It's the perfect metaphor for a community within the larger Mycelium ecosystem.

**User story:** "I joined the 'fly fishing' grove. The collective knowledge has transformed my success rate. Last month, a member shared a loom for reading water that I'd never have figured out on my own."

**Analogy:** Groves are like subreddits or Discord servers, but centered around shared behavioral patterns rather than discussion.

---

### Marketplace
*Noun.* /ˈmärkəˌplās/

**A place where users can buy, sell, and trade looms and topology seeds.** A marketplace for intelligence.

**What it is:** Some people are experts. They've spent years developing techniques that work. The marketplace lets them package that expertise and share it—for free, for a fee, or in exchange for other looms.

The marketplace:
- **Incentivizes** expert contributors (they can earn from their expertise).
- **Curates** quality through ratings and reviews (the best rise to the top).
- **Protects** intellectual property through cryptographic signatures (provenance is tracked).
- **Enables micropayments** (pay per loom or subscribe to a creator).

**Why this term:** It's a marketplace for the new currency of intelligence—looms. The name tells you exactly what it is.

**User story:** "I sold my 'tournament winning' fishing loom and made enough to buy three more from other pros. Now my loomery has techniques from anglers all over the country."

**Technical note:** The marketplace uses blockchain‑inspired provenance tracking (without the energy cost) to ensure creators get credit. Payments can be in traditional currency or in a community token.

---

### Echo
*Noun.* /ˈekō/

**A shared pattern that returns to you from the collective.** Something you contributed, improved by others, now coming back.

**What it is:** When you share a loom—anonymously, with privacy preserved—it joins the collective. Others may use it, refine it, improve it. If it's good, it echoes.

Eventually, that improved version may come back to you. You recognize it—it started with you—but it's better now, enhanced by the wisdom of others.

**Why this term:** An echo is a sound that returns to you, changed by its journey. A pattern echo is the same.

**User story:** "I shared a fishing loom months ago. Yesterday, an improved version came back to me—someone had refined it for a different lake, and the combination works everywhere now."

**Research note:** The echo phenomenon is a form of collective intelligence, similar to how open‑source software improves through community contributions. Our system accelerates this by making patterns directly composable.

---

### Current
*Noun.* /ˈkərənt/

**A flow of shared patterns in a particular domain.** What's working now for people like you.

**What it is:** Currents are trends in the collective. In fishingLOG, there might be a current about topwater lures this season. In studyLOG, a current about effective spaced repetition techniques.

Currents help you discover what's working for others before you'd discover it yourself.

**Why this term:** Like ocean currents, these are flows you can ride. They carry you in productive directions.

**User story:** "I noticed a current in my fishing grove about night fishing. I'd never tried it, but the current convinced me. Now it's my favorite."

**Technical note:** Currents are detected through temporal analysis of shared patterns. They show up in the logbook as trending loglines.

---

### Tapestry
*Noun.* /ˈtapəstrē/

**The collective intelligence of the whole community.** All the patterns, all the blueprints, all the wisdom, woven together.

**What it is:** The tapestry is what emerges when millions of users contribute, share, refine, and combine. It's not a single model or database—it's a living, evolving fabric of shared understanding.

The tapestry is greater than any individual's contribution. It contains patterns no single person could have discovered, combinations no single mind could have imagined.

**Why this term:** A tapestry is a woven fabric, often depicting a complex scene or story. Our collective intelligence is woven from countless individual threads, each contributing to a larger picture.

**User story:** "Sometimes I browse the tapestry just to see what's emerging. Last week, someone combined meditation techniques with study techniques in a way I'd never considered. The tapestry is endlessly creative."

**Technical note:** The tapestry is an emergent property of the federated system. It's not stored in one place; it exists in the relationships between patterns across the community.

---

## Part V: The Fruit — Emergent Properties

These are the things that can't be pointed to in code but are unmistakably present. They're what makes the system feel alive.

---

### Emergence
*Noun.* /ēˈmərjəns/

**The appearance of behaviors and capabilities not explicitly programmed.** The whole becomes greater than the sum of its parts.

**What it is:** No single agent in Mycelium is intelligent. A vision agent just sees. A text agent just reads. An intent agent just decides. But together, they produce behavior that seems intelligent—that anticipates, adapts, and innovates.

This is emergence. It's not magic; it's what happens when simple components interact in a rich, learnable graph. The system as a whole develops properties that no component individually possesses.

In Mycelium, emergence manifests as:
- **Specialization:** Agents naturally become experts in certain tasks.
- **Coordination:** Agents learn to work together without central control.
- **Resilience:** The system degrades gracefully when components fail.
- **Innovation:** New solutions emerge from recombination of existing patterns.
- **Anticipation:** The system learns to predict and prepare for your needs.

**Why this term:** It's the scientific term for how complex global behavior arises from simple local rules. It has rigor and history.

**Analogy:** Ant colonies exhibit complex nest architecture despite each ant following simple rules. No ant knows the plan; the plan emerges. Same here.

**Research note:** Emergence is studied in complex systems science (Holland 1998), neuroscience (Koch 2004), and artificial life. Our system is designed to foster emergence through local learning and global optimization.

---

### Logos
*Noun.* /ˈlōˌɡäs/

**The emergent intelligence of your whole system.** What makes it feel like a partner rather than a tool.

**What it is:** Your LOGOS is not a component. It's not the agents, not the graph, not the logbook. It's what *arises* from them—the coherent, evolving understanding that the system has of you.

The LOGOS is characterized by:
- **Understanding:** The system seems to grasp your intentions, not just your actions.
- **Anticipation:** It knows what you'll need before you ask.
- **Style:** It adapts to your unique way of doing things.
- **Trust:** You rely on it; it rarely lets you down.

**Why this term:** In ancient philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Your personal LOGOS is the rational structure underlying your digital life.

**User story:** "My fishingLOG has developed its own logos. It doesn't just record my trips—it seems to *understand* fishing. Sometimes it suggests things I hadn't thought of, and they work. It's like having a partner who knows me."

---

### Vitality
*Noun.* /vīˈtalədē/

**A metric that measures how well your system is learning and optimizing.** A dashboard for the living system.

**What it is:** Just as you track your physical health—heart rate, steps, sleep—you can track your system's vitality. It's a composite metric that tells you whether your Mycelium instance is thriving.

Vitality considers:
- **Prediction accuracy:** How well does the system anticipate your actions?
- **Optimization rate:** How quickly is it improving through dreaming?
- **Graph coherence:** How well organized is the agent network?
- **Synaptic balance:** Are connections strengthening and weakening appropriately?
- **User satisfaction:** Explicit feedback and implicit signals.

**Why this term:** "Vitality" captures the living nature of the system. A vital system is one that's learning, adapting, and serving you well. A stagnant system is one that's stopped growing.

**User interface:** A dashboard showing your vitality over time, with suggestions for improvement. "Your fishing logbook could benefit from more varied logs. Try fishing in new locations." "Your graph coherence is excellent. Great job!"

---

### Resonance
*Noun.* /ˈrezənəns/

**How well your system's understanding matches your actual needs.** When your LOGOS resonates, it just *gets* you.

**What it is:** Resonance is felt, not measured. It's the experience of the system suggesting exactly what you needed, before you asked. It's the feeling of being understood.

High resonance means the system's predictions match your intentions. Low resonance means constant corrections.

**Why this term:** When two things resonate, they vibrate together. When you and your system resonate, you're in harmony.

---

### Coherence
*Noun.* /kōˈhirəns/

**How well your log graph is organized.** Are the right loggers connected? Do they work together smoothly?

**What it is:** Coherence is a technical metric that measures the quality of the log graph. High coherence means strong, useful connections; clear functional clusters; efficient information flow.

**Why this term:** Coherent means logically consistent and well‑organized. A coherent graph is exactly that.

---

### Momentum
*Noun.* /mōˈmen(t)əm/

**The rate at which your system is improving.** How quickly it's learning, adapting, optimizing.

**What it is:** Momentum measures the velocity of improvement. High momentum means you're in a virtuous cycle—each improvement enables faster future improvements.

**Why this term:** In physics, momentum is mass times velocity. Here, it's capability times learning rate. The metaphor carries.

---

## Part VI: The Verbs — How You Interact

These are the actions you take with the system—the things you do.

---

### Logging In
*Phrase.* /ˈlôɡiNG in/

**Starting a demonstration.** "Logging in" tells the system: "Watch what I'm about to do and learn from it."

**What it is:** When you want to teach the system something new, you "log in" the behavior. You perform it once, and the system captures it—the sequence, the context, the outcome. Later, that behavior becomes a logline, then possibly a loom.

**Why this term:** A beautiful double meaning. You're both "logging in" to use the system and "logging in" a new behavior. The phrase carries both meanings effortlessly.

**User story:** "I logged in my morning fishing routine so fishingLOG could learn my preferences. Now it knows exactly how I like to start the day."

---

### Replaying
*Verb.* /rēˈplāiNG/

**Running a learned behavior from a logline or loom.** Replaying reproduces a demonstrated pattern, adapted to current conditions.

**What it is:** Once a behavior is captured, you can replay it anytime. The system runs through the behavior again, but adapted to the current context. If conditions are different, the behavior adjusts while staying true to the original pattern.

**Why this term:** Simple and clear. You're playing it again.

**User story:** "I replayed last week's successful fishing trip, and the system adapted it to today's different weather. Same technique, adjusted for conditions."

---

### Weaving
*Verb.* /ˈwēviNG/

**Combining multiple looms to create new behaviors.** You can guide weaving explicitly, or the system can do it automatically during dreaming.

**User story:** "I asked the system to weave my 'early morning' loom with my 'cloudy day' loom. It created a new pattern for overcast dawns that works perfectly."

---

### Dreaming
*Verb.* /ˈdrēmiNG/

**The system improving itself overnight.** You don't initiate dreaming; it happens automatically. But you can check its progress.

**User story:** "I checked my vitality dashboard this morning and saw that dreaming improved my fishing looms by 12% overnight."

---

### Casting
*Verb.* /ˈkastiNG/

**Sharing a loom via a loomcast.** Spreading proven behaviors across the community.

**What it is:** When you've developed a technique that works, you can cast it. Package it as a loomcast, add metadata, and share it with your grove or the whole marketplace.

**Why this term:** Short, active, evocative. You're casting your loom out into the world, like casting a fishing line or casting a vote.

**User story:** "I'm casting my 'early morning bass' loom to the fishing grove. Hope it helps others as much as it helped me."

---

### Tuning
*Verb.* /ˈto͞oniNG/

**Adjusting a loom to better fit your context.** Personalizing shared wisdom.

**What it is:** When you import a loomcast, it may not be perfect for your specific situation. Tuning adjusts it—through demonstration, through feedback, through dreaming—until it fits just right.

**Why this term:** You're tuning an instrument to play correctly in your space. You're tuning a behavior to work correctly in your context.

**User story:** "I imported a loomcast from a pro angler, then tuned it for my local lake. Now it's perfect."

---

## Part VII: Technical Appendix

For developers and the deeply curious. These terms are more technical but still built on the same conceptual foundations.

---

### SPORE Protocol
*Noun.* /spôr ˈprōdəˌkôl/

**The lightweight messaging protocol used for agent communication.** SPORE defines how agents talk to each other.

**What it defines:**
- Message formats (JSON or binary Cap'n Proto)
- Topic naming conventions (hierarchical, e.g., `/sensors/camera/frame`)
- Delivery guarantees (best‑effort with optional reliability)
- Agent discovery (announce/acknowledge/heartbeat)
- Compatibility versioning

**Why this term:** Spores are how mycelial networks propagate—fitting for an agent communication protocol.

---

### Behavioral Embedding Space (BES)
*Noun.* /biˈhāvyərəl emˈbediNG spās/

**A learned latent space where every possible behavior is mapped to a vector.** The mathematical foundation for loglines and looms.

**What it is:** Behaviors that are semantically similar lie close together; distinct behaviors are far apart. The BES is trained on a large corpus of demonstrations using a combination of reconstruction and contrastive loss.

**Technical note:** The BES enables similarity search, interpolation, and composition of behaviors.

---

### Logline Format
*Noun.* /ˈlôɡˌlīn ˈfôrˌmat/

**The serialization specification for loglines.** Protobuf schema defining how loglines are stored and transmitted.

**What it includes:** Seed embedding, agent type requirements, base model hashes, cryptographic signatures, metadata.

---

### Topology Seed Format
*Noun.* /təˈpäləjē sēd ˈfôrˌmat/

**The serialization specification for topology seeds.** Protobuf schema for agent configurations.

**What it includes:** Graph structure (compressed adjacency), synaptic weights, agent type references, context signature, performance metrics.

---

### Dreamlogger API
*Noun.* /ˈdrēmˌlôɡər ā-pē-ˈī/

**The interface for triggering and monitoring dreaming sessions.** For developers and power users.

**What it allows:** Manual dream initiation, progress tracking, result validation, rollback, scheduling.

---

## Epilogue: The Language of a New Era

Every transformative technology brings with it a new vocabulary.

The printing press gave us "font," "typeface," "folio," "quarto"—words that named new realities and made them thinkable.

Electricity gave us "watt," "volt," "circuit," "generator"—words that let us understand and control a force we couldn't see.

Computing gave us "byte," "protocol," "algorithm," "cache"—words that became second nature within a generation.

Mycelium and LOG.ai are giving us a new language for a new kind of intelligence—one that grows with us, learns from us, optimizes itself for us, and becomes a living extension of our intent.

**Log. Logline. Loom. Loomery. Grove. Plinko. Vitality. Logos.**

These words name something new. Use them. Share them. They are the vocabulary of the future.

And like all living things, they will grow, change, and adapt. What matters is not that we've found the perfect words, but that we've found words at all—words that let us think and build together.

The rest is up to you.

---

## Quick Reference

| Term | Definition |
|------|------------|
| **Mycelium** | The overall architecture and open‑source project |
| **Agent** | A specialized neural process; a node in the swarm |
| **Swarm** | The collection of all active agents |
| **Graph** | The structure of nodes (agents) and edges (connections) |
| **LOG** | Learned Optimization Graph—the core principle and platform brand |
| **Logos** | The emergent intelligence of your whole system |
| **Log** | A recorded event or sequence; the raw material of learning |
| **Logline** | A compressed behavioral seed |
| **Logbook** | Personal long‑term memory (vector database) |
| **Loom** | A reusable, optimized routine |
| **Loomery** | A collection of looms |
| **Loomcast** | A shareable loom |
| **Plinko** | The stochastic decision layer |
| **World Model** | A learned environment simulator |
| **Dreaming** | Overnight simulation for improvement |
| **Looming** | The process of weaving logs into looms |
| **Weaving** | Combining looms to create new behaviors |
| **Pruning** | Removing weak agent connections |
| **Grafting** | Forming new agent connections |
| **Clustering** | Self‑organization of agents into functional groups |
| **Synaptic Weight** | Strength of a connection between agents |
| **Topology Seed** | A compressed agent configuration |
| **Federated Learning** | Privacy‑preserving cross‑user learning |
| **Grove** | Community for exchanging looms |
| **Marketplace** | Store for buying/selling looms |
| **Echo** | A pattern that returns, improved by the collective |
| **Current** | A trend in shared patterns |
| **Tapestry** | The collective intelligence of the whole community |
| **Emergence** | Global behavior from local interactions |
| **Vitality** | A metric of system health |
| **Resonance** | How well the system understands you |
| **Coherence** | How well the agent graph is organized |
| **Momentum** | The rate of system improvement |
| **Logging In** | Starting a demonstration |
| **Replaying** | Running a learned behavior |
| **Casting** | Sharing a loom via loomcast |
| **Tuning** | Adjusting a loom to your context |

---

*For the latest version of this lexicon, to contribute new terms, or to join the community, visit [github.com/superinstance/mycelium/lexicon](https://github.com/superinstance/mycelium/lexicon).*
