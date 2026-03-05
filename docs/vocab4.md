# The Mycelium Lexicon

## A Language for Living Intelligence

**Version 7.0 — June 2026**  
**SuperInstance Open Source Initiative**

*A complete guide to the concepts, terms, and language of agent‑native, self‑optimizing systems built on the Learned Optimization Graph (LOG) architecture.*

---

## Prologue: The Story of a New Language

Every great shift in how humans think has brought with it a shift in how humans speak.

The printing press didn't just change how books were made—it gave us words like "font," "typeface," and "folio." These weren't jargon; they were tools for thinking about something new. Before we had the word "font," you couldn't easily distinguish the shape of letters from the words they formed. The word created the distinction.

Electricity gave us "voltage," "current," "circuit." Computing gave us "protocol," "cache," "algorithm." Each word named a new reality and made that reality thinkable.

We are at another such moment.

The systems we're building—swarms of agents learning from demonstration, compressing behavior into vectors, dynamically rewiring their own connections—have no precedent in the history of computing. They are not faster versions of old things. They are something else entirely.

And something else entirely needs its own language.

This lexicon is that language. It is designed to be:
- **Intuitive enough** that you can guess meanings from context
- **Precise enough** that engineers can implement from these descriptions
- **Inspiring enough** that you'll want to be part of what comes next

The terms are arranged in layers. Start at the beginning and read straight through. Each word builds on the ones before it. By the end, you'll have a complete mental model—not just definitions, but a connected understanding of how this system works and why it matters.

Let's begin.

---

## Part I: The Soil — Foundational Concepts

Before we can talk about what grows, we need to talk about what it grows from.

---

### Mycelium
*Noun.* /mīˈsēlēəm/

**The overarching architecture and open‑source project.** Named for the hidden fungal networks that connect trees into a single, intelligent organism.

**The science:** In forest ecology, mycelial networks are now understood as the "wood wide web"—underground fungal threads that connect trees, enabling them to share water, nutrients, and even warning signals about pests . These networks have no central control, yet they make complex decisions about resource allocation. Damage any part, and the rest continues functioning. Most of their work is invisible; we see only what they produce—mushrooms, the fruiting bodies.

**The system:** Mycelium.ai is the technological realization of these principles. When you run Mycelium, you're running a swarm of specialized agents connected in a dynamic graph that learns and evolves. You don't see most of what happens—the proposals, the bidding, the dreaming—but you see what it produces: a system that understands you, anticipates you, and grows with you.

**Why this name:** It's a constant reminder that intelligence need not be monolithic. The most robust, adaptive systems in nature are networks. Your Mycelium instance is a forest, and you are its gardener.

**Research context:** The term "mycelium" is increasingly used across scientific disciplines to describe decentralized, resilient systems—from building materials that self-organize  to theoretical computing architectures that operate on biological principles . We join this lineage.

---

### Agent
*Noun.* /ˈājənt/

**A specialized, autonomous process that performs a narrow function within the larger swarm.** Agents are the nodes of the Mycelium network.

**What it is:** An agent is not intelligent by itself. It does one thing. A vision agent looks at images and identifies objects. A text agent reads words and understands intent. A context agent tracks time, location, and state. An executor agent clicks buttons, types text, makes things happen.

Each agent contains a tiny neural model—typically 1 to 100 million parameters, small enough to run continuously on your device. It consumes information from specific sources (topics), processes it, and writes proposals about what should happen next.

**The neuroscience parallel:** Agents are like neurons. A single neuron cannot think; a hundred billion of them, connected in the right way, can write poetry. The intelligence is in the network, not the node.

**Why this term:** "Agent" carries the right weight—autonomy, purpose, action. It's familiar from AI literature, but here it's grounded. You can point to an agent in the code, watch it work, see how it connects to others.

**Technical foundation:** Agents in Mycelium learn from experience. Their internal models can be fine‑tuned overnight. Their sense of how valuable their actions are (their "value function") updates with every success and failure. This aligns with research on trajectory embeddings that capture agent competencies without explicit reward signals .

---

### Swarm
*Noun.* /swôrm/

**The collection of all active agents in a Mycelium instance.** A swarm is what's running right now.

**What it is:** When you open your laptop in the morning, a swarm wakes up. Dozens or hundreds of agents begin processing: vision agents watching your screen, audio agents listening for cues, context agents tracking your calendar, intent agents forming hypotheses about what you might need.

The swarm is not a list; it's a living system. Agents are loaded and hibernated based on what you're doing. New agents can be recruited when you encounter something novel. Connections between agents strengthen and weaken as patterns emerge.

**Why this term:** "Swarm" evokes multiplicity, coordination, and emergent behavior. A swarm of bees has no leader, yet it finds food, builds hives, and defends itself. Research in multi-agent reinforcement learning has shown that swarms can develop specialized roles without explicit programming, improving coordination by up to 20% in complex tasks .

---

### Graph
*Noun.* /ɡraf/

**The underlying structure of the Mycelium system.** A graph is a way of representing connections.

**What it is:** In mathematics, a graph has:
- **Nodes** — things (in Mycelium, these are agents)
- **Edges** — connections between things (communication channels)
- **Weights** — strengths of those connections (how much influence one agent has on another)

The Mycelium graph is the complete map of how agents are connected. It's both the architecture (who talks to whom) and the knowledge (what those connections mean). A strong edge from agent A to agent B means "when A has something to say, B should pay attention." A cluster of tightly connected agents means "these agents often work together."

**Why this term:** "Graph" is mathematically precise and visually intuitive. Everyone understands nodes and edges. And unlike a neural network's inscrutable weights, a graph can be drawn. You can see your agent network, understand it, trust it.

---

### LOG (Learned Optimization Graph)
*Noun.* /läɡ/ *Acronym.* /el-ō-jē/

**The core architectural principle and platform brand.** LOG stands for Learned Optimization Graph.

**The three pillars:**

- **Learned** — Nothing in this system is programmed in the traditional sense. You don't write code to tell it what to do. You demonstrate. The system watches, captures what you do, and learns patterns. This aligns with research on trajectory embedding, where state-action sequences are compressed into latent spaces that capture skills and competencies without requiring reward labels .

- **Optimization** — Learning alone is not enough. The system actively improves itself. It dreams at night, simulating millions of variations to find better ways. It prunes connections that aren't useful and grows new ones that might be. It learns from the entire user population through privacy-preserving federated learning .

- **Graph** — Everything is represented as a graph. Agents are nodes. Connections are edges. Knowledge is in the structure. The graph is both what the system knows and how it's organized.

**Why this word:** "Log" carries multiple meanings that reinforce each other:
- A **log** is a record — the raw material of learning
- A **log** is a piece of a tree — connecting to the mycelium metaphor
- A **log** is the base of a logarithm — hinting at the mathematical compression that turns raw sequences into compact seeds

When you say "fishingLOG," you mean both "a fishing log that records your trips" and "a fishing application built on the Learned Optimization Graph architecture." The user gets the familiar meaning; the developer gets the technical precision.

**Tagline:** Your personal learned optimization graph.

---

### Logos
*Noun.* /ˈlōˌɡäs/

**The emergent intelligence of your whole system.** What makes it feel like a partner rather than a tool.

**What it is:** After you've used Mycelium for a while—weeks, months, years—something happens. The system starts to feel like it *knows* you. It anticipates what you need. It suggests things you hadn't thought of. It adapts to your style, your habits, your quirks.

This is your LOGOS. It's not a component you can point to. It's not in any single agent. It's what emerges from the whole—the accumulated wisdom of all your logs, optimized through dreaming, organized through the graph, expressed through looms.

The LOGOS is characterized by:
- **Understanding:** The system seems to grasp your intentions, not just your actions
- **Anticipation:** It knows what you'll need before you ask
- **Style:** It adapts to your unique way of doing things
- **Trust:** You rely on it; it rarely lets you down

**Why this term:** In ancient Greek philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Your personal LOGOS is the rational structure underlying your digital life. The word also plays beautifully with "log"—Logos contains "log," suggesting that from many logs, a coherent intelligence emerges.

---

## Part II: The Roots — What You Capture

Now that we understand the soil—the agents, the swarm, the graph, the LOG—let's talk about what grows from it. These are the things you create, capture, and cultivate.

---

### Log
*Noun.* /lôɡ/ *Verb.* /lôɡ/

**A record of an event or sequence of actions.** Logs are the raw material from which intelligence is refined.

**What it is:** Every time you interact with a LOG application, it logs what happened. When you fish, it logs location, weather, bait, catch. When you study, it logs subject, duration, focus level, test scores. When you work, it logs meetings, emails, decisions, outcomes.

These logs are not just data; they're experience. They're what the system uses to learn.

**As a verb:** "Log this" tells the system to watch and learn. You perform a behavior once, and the system captures it—the sequence, the context, the result.

**Why this term:** As discussed, "log" carries centuries of meaning. It's the word humans have always used for recording experience. We're just making it alive.

**Research foundation:** Recent advances in trajectory embedding have shown that state-action sequences can be compressed into latent spaces that capture underlying skills and competencies . This is the mathematical basis for turning raw logs into something learnable.

---

### Logline
*Noun.* /ˈlôɡˌlīn/

**A compressed representation of a behavioral pattern.** A logline is what you get when the system has learned something.

**What it is:** When the system has seen a behavior enough times—or when you explicitly demonstrate it—it distills that behavior into a logline. The logline is not the raw sequence; it's the *essence*. It captures what matters about the behavior while discarding what's incidental.

Technically, a logline is a vector—typically 64 to 1024 floating‑point numbers. Research demonstrates that such trajectory embeddings can effectively capture agent competencies and even exhibit additive properties, where combining embeddings yields novel behaviors .

Loglines are:
- **Portable:** They can be shared, sold, gifted. A logline is small enough to email.
- **Private:** They encode patterns, not raw data. Share a logline without sharing your personal information.
- **Composable:** Loglines can be combined. Like mixing colors, you can create new behaviors from old ones.
- **Optimizable:** They improve over time through dreaming.

**Why this term:** In Hollywood, a logline is a one‑sentence summary of a movie—enough to know whether you're interested. A logline captures the essence of a behavior the same way.

**User story:** "After three successful fishing trips, fishingLOG created a logline for 'cloudy day bass fishing'. I can share it with my friends, and they can use it on their own fishingLOG."

---

### Logbook
*Noun.* /ˈlôɡˌbo͝ok/

**Your personal long‑term memory.** A vector database containing all your logs and loglines.

**What it is:** Everything you've ever done with your LOG applications lives here. Every fishing trip. Every study session. Every business meeting. Every pattern the system has discovered. All stored, indexed, searchable.

The logbook is:
- **Private:** It lives on your device by default. You control what leaves.
- **Searchable:** You can find past experiences by similarity. "Show me fishing trips like this one."
- **Ever‑improving:** Old loglines can be refined by new experiences. The logbook is not static; it evolves.
- **Portable:** Take your logbook to a new device. Your intelligence moves with you.

**Why this term:** Ships' captains kept logbooks—bound volumes of their voyages, filled with observations, measurements, and lessons learned. They were priceless. Your digital logbook is the same, but it learns.

---

### Loom
*Noun.* /lo͞om/

**A reusable, optimized routine discovered from your logs.** A loom is what you get when a logline has been woven into something executable.

**What it is:** A loom is a pattern that has been refined to the point where it can run automatically. It's the "muscle memory" of the system—common sequences that execute without deliberation.

Unlike traditional algorithms, which are written in code, looms are:
- **Learned from demonstration** (not programmed)
- **Continuously optimized** through dreaming
- **Personalized** to your specific style
- **Shareable** as loglines

**Why this term:** A loom is a device for weaving thread into fabric. Threads alone are just strands; woven together, they become something strong and useful. Your logs are threads. A loom weaves them into something you can use.

The word also flows well in speech: "I used a fishing loom." "The system discovered a new study loom." It's short, active, and memorable.

**Research connection:** The concept of emergent roles in multi-agent systems shows that agents naturally develop specialized behaviors through interaction . Looms are the crystallization of this process—stable, reusable patterns that have proven their value.

---

### Loomery
*Noun.* /ˈlo͞omərē/

**A collection of looms, organized by purpose or domain.** Your personal library of reusable routines.

Just as a library organizes books, your loomery organizes looms. Fishing looms in one section. Study looms in another. Business looms in another. You can browse, search, and curate.

**Why this term:** It's where looms live. Simple, clear, evocative.

---

### Loomcast
*Noun.* /ˈlo͞omˌkast/

**A shareable loom.** Like a podcast, but for behaviors.

When you've developed a technique that works, you can package it as a loomcast. Add metadata, a description, tags, maybe a price. Share it with your grove or the whole marketplace.

**Why this term:** Podcasts are broadcasts you can listen to anytime. Loomcasts are behaviors you can run anytime. The parallel is intentional.

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

**Why this term:** The visual is perfect. Proposals enter at the top, bounce through discriminators and noise, and eventually emerge as a selected action. The path is stochastic but not random, shaped by the structure it passes through.

**Research context:** This market-based approach aligns with emerging thinking about agent networks that use economic mechanisms for coordination. The van der Schaar Lab's proposed "Agent Network" architecture includes a Game Theoretic layer specifically for negotiation, coalition formation, and incentive alignment . Plinko is our implementation of this layer—a lightweight, learned market rather than explicit game-theoretic protocols.

---

### World Model
*Noun.* /wərld ˈmäd(ə)l/

**A learned simulator that predicts how the environment will respond to actions.** The world model is what makes dreaming possible.

**What it is:** If you click this button, what happens? If you type this text, how does the app respond? If you cast here, will the fish bite? The world model knows—or at least, it has learned to predict.

The world model is trained on your actual logs. It watches what happens when you take actions, and it builds an internal model of cause and effect. Over time, it becomes a pretty good simulator of your digital environment.

**Technical components:**
- **Encoder:** Compresses observations into a latent state
- **Transition model:** Predicts next state given current state and action
- **Reward model:** Predicts how satisfied you'll be with the outcome
- **Decoder:** Reconstructs observations (optional, for visualization)

**Why this term:** It's a model of your world. Simple, direct, accurate.

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
- **Micro‑dreams** refine fine motor skills (typing speed, casting accuracy, mouse precision)
- **Meso‑dreams** optimize routine sequences (email triage, fishing preparation, meeting facilitation)
- **Macro‑dreams** combine looms to create new behaviors

**Why this term:** Just as humans consolidate memories and rehearse skills during sleep, Mycelium dreams to get better while you rest. The metaphor is both intuitive and scientifically grounded—research in neuromorphic computing shows that dreaming-like processes can dramatically reduce the number of real-world interactions needed for learning.

---

### Looming
*Verb.* /ˈlo͞omiNG/

**The process of weaving logs into looms.** When the system discovers a recurring pattern in your logs, it "looms" them—compresses them into a reusable routine.

**What it is:** Looming happens automatically. The system watches for sequences that occur frequently. When it finds one, it extracts it, compresses it, and adds it to your loomery.

You can also loom explicitly. When you perform a new behavior and want to save it, you tell the system "loom this." It captures the demonstration and adds it to your collection.

**Why this term:** It's the verb form of "loom." Simple and natural.

---

### Weaving
*Verb.* /ˈwēviNG/

**Combining multiple looms to create new behaviors.** Weaving is how the system innovates.

**What it is:** Take the "early morning" loom from fishing and the "cloudy day" loom from another context, weave them together, and you get a new pattern for overcast dawns. The result is something neither original contained—something new.

Weaving can happen automatically through dreaming, or you can guide it explicitly.

**Why this term:** You're weaving together different threads to create something new. The metaphor is consistent and intuitive.

**Research connection:** The ability to combine learned behaviors is a hallmark of compositional intelligence. Recent work on emergent communication protocols shows that agents can develop compositional languages that enable zero-shot adaptation to new tasks . Weaving is our implementation of this principle—looms become a vocabulary for composing novel behaviors.

---

## Part IV: The Branches — Dynamic Agent Webs

Now we reach the branches—the parts of the system that are still growing, still evolving. These are the cutting‑edge mechanisms that make Mycelium truly alive.

---

### Log Graph
*Noun.* /lôɡ ɡraf/

**The evolving network of agents and their connection strengths.** The log graph is the system's muscle memory.

**What it is:** Remember the graph from Part I—nodes (agents) connected by edges (communication channels). The log graph is that graph, but *learned*. Its structure comes from experience.

Edges in the log graph have weights. A strong edge from agent A to agent B means: "When A activates, it's often useful for B to know about it." A weak edge means: "They sometimes talk, but it's not critical." No edge means: "They've never had reason to communicate."

The log graph is dynamic. Edges strengthen with successful use, weaken with disuse, form when patterns suggest they'd help, and dissolve when they're no longer needed.

**Why this term:** It's the graph that emerges from your logs—the structure that learning creates.

**Research foundation:** The Agent Network architecture proposed by the van der Schaar Lab includes a Discovery and Communication layer specifically for agent identification, profiling, and connection . Our log graph is the runtime instantiation of this layer—not just a protocol for discovery, but a learned structure that optimizes itself over time.

---

### Synaptic Weight
*Noun.* /səˈnaptik wāt/

**The strength of a connection between two agents.** Synaptic weights determine how much influence one agent has on another.

**What it is:** When agent A sends a message, it doesn't go directly to agent B's input. It goes through a weighted connection. If the weight is high, the message has strong influence. If the weight is low, it has weak influence.

Synaptic weights change over time:
- **Increase** when the connection is used in successful sequences
- **Decrease** when used in failures or not used at all
- **Prune** when they fall below a threshold
- **Initialize** when new connections form

**Why this term:** Directly analogizes to biological synapses, which strengthen with use and weaken with disuse. The metaphor is exact.

---

### Pruning
*Noun.* /ˈpro͞oniNG/

**Removing weak or unused agent connections.** Pruning keeps the graph lean and efficient.

**What it is:** Over time, some connections prove useless. Maybe they were tried and didn't help. Maybe they were useful once but aren't anymore. These connections are noise—they consume resources and can interfere with good ones.

Pruning identifies connections whose synaptic weights have fallen below a threshold for an extended period and removes them entirely. The graph becomes sparser, more efficient, more focused.

**Why this term:** A gardener prunes a tree—removing dead branches so the living ones thrive. The system prunes its graph for the same reason.

---

### Grafting
*Noun.* /ˈɡraftiNG/

**Forming new agent connections when patterns suggest they would be useful.** Grafting enables the graph to adapt to new tasks.

**What it is:** Sometimes two agents are frequently active around the same time, in successful sequences, but they're not directly connected. Their communication has to go through intermediaries, which is slower and less direct.

When the system detects this pattern—repeated co‑activation without direct connection—it may graft a new edge directly between them. The new connection starts with a small weight, which can then strengthen through use.

**Why this term:** In orchards, grafting joins a fruit‑bearing branch to a hardy rootstock. The result is stronger than either alone. Grafting does the same for agents.

---

### Clustering
*Noun.* /ˈkləstəriNG/

**The self‑organization of agents into functional groups.** Using mathematical techniques on the log graph, agents naturally form teams that work well together.

**What it is:** In any complex system, specialization emerges. Some agents work together on vision tasks. Others collaborate on language. Others coordinate actions. These groupings aren't programmed—they emerge from patterns of successful interaction.

Clustering identifies these natural groups. Once identified, the system can optimize within groups (faster, richer communication) and between groups (sparser, higher‑level coordination).

**Why this term:** Agents cluster based on their roles, just as neurons in the brain form functional columns.

**Research connection:** Recent work on role discovery in multi-agent reinforcement learning demonstrates that agents can learn specialized roles by maximizing mutual information between roles, observed trajectories, and expected future behaviors . This approach improved win rates by up to 20% in complex coordination tasks. Clustering is our unsupervised implementation of this principle—roles emerge, not from explicit optimization, but from the natural dynamics of the log graph.

---

### Topology Seed
*Noun.* /təˈpäləjē sēd/

**A compact representation of a learned agent configuration.** The nodes, edges, and weights that define a successful collaboration pattern.

**What it is:** Just as a logline captures a behavior, a topology seed captures an *organization*. It answers: For this kind of task, which agents should be connected, and how strongly?

Topology seeds enable:
- **Sharing** proven configurations
- **Transfer** across users
- **Evolution** through recombination
- **Instant deployment** (load a topology seed and your swarm reorganizes)

**Why this term:** Just as a seed contains the blueprint for a plant, a topology seed contains the blueprint for an agent organization. Plant the seed, grow the graph.

---

## Part V: The Forest — Collective Intelligence

No tree grows alone. These terms describe how individual Mycelium instances connect into a larger intelligence.

---

### Grove
*Noun.* /ɡrōv/

**A community of users who share looms and topology seeds.** Like a book club, but for behaviors.

**What it is:** People who share interests form groves. Fly fishers have one. Organic chemistry students have another. Chess players have another. Within a grove, members share looms they've found effective, rate each other's contributions, and collectively improve their craft.

**Why this term:** A grove is a small group of trees—a community within the larger forest. It's the perfect metaphor.

**Research context:** This aligns with emerging visions of "The Agent Network"—a shared infrastructure where agents owned by individuals and organizations interact dynamically, forming alliances and exchanging services . Groves are the social layer on top of this infrastructure.

---

### Resonance
*Noun.* /ˈrezənəns/

**The phenomenon where patterns that work for many people become stronger in the collective.** Wisdom of the crowd, distilled.

**What it is:** When the same logline proves useful for many users, it resonates. The collective signal grows stronger. New users benefit from what the crowd has discovered.

Resonance is not averaging; it's amplification. Patterns that work across diverse contexts are likely to be robust.

**Why this term:** In physics, resonance is when a system vibrates at higher amplitude because it's driven at its natural frequency. Here, patterns resonate when they align with what many people need.

---

### Echo
*Noun.* /ˈekō/

**A shared pattern that returns to you from the collective.** Something you contributed, improved by others, now coming back.

**What it is:** When you share a logline—anonymously, with privacy preserved—it joins the collective. Others may use it, refine it, improve it. If it's good, it echoes.

Eventually, that improved version may come back to you. You recognize it—it started with you—but it's better now.

**Why this term:** An echo is a sound that returns to you, changed by its journey. A pattern echo is the same.

**Privacy foundation:** This sharing happens through privacy-preserving federated learning techniques that prevent any individual's data from being reconstructed . Only patterns, never raw data, are shared.

---

### Marketplace
*Noun.* /ˈmärkəˌplās/

**A place where users can buy, sell, and trade looms and topology seeds.** A marketplace for intelligence.

**What it is:** Some people are experts. They've spent years developing techniques that work. The marketplace lets them package that expertise and share it—for free, for a fee, or in exchange for other looms.

**Why this term:** It's a marketplace for the new currency of intelligence—looms.

**Economic vision:** This aligns with the vision of an "AI-driven economy" where agents trade services and capabilities, forming a self-sustaining digital ecosystem .

---

## Part VI: The Fruit — Emergent Properties

These are the things that can't be pointed to in code but are unmistakably present. They're what makes the system feel alive.

---

### Emergence
*Noun.* /ēˈmərjəns/

**The appearance of behaviors and capabilities not explicitly programmed.** The whole becomes greater than the sum of its parts.

**What it is:** No single agent in Mycelium is intelligent. A vision agent just sees. A text agent just reads. An intent agent just decides. But together, they produce behavior that seems intelligent—that anticipates, adapts, and innovates.

This is emergence. It's not magic; it's what happens when simple components interact in a rich, learnable graph.

In Mycelium, emergence manifests as:
- **Specialization:** Agents naturally become experts in certain tasks
- **Coordination:** Agents learn to work together without central control
- **Resilience:** The system degrades gracefully when components fail
- **Innovation:** New solutions emerge from recombination of existing patterns
- **Anticipation:** The system learns to predict and prepare for your needs

**Why this term:** It's the scientific term for how complex global behavior arises from simple local rules. It has rigor and history.

**Research validation:** Studies in multi-agent reinforcement learning have documented emergence of specialized roles, communication protocols, and coordination strategies across domains from autonomous vehicles to drone swarms .

---

### Logos
*Noun.* /ˈlōˌɡäs/

**The emergent intelligence of your whole system.** What makes it feel like a partner rather than a tool.

Your LOGOS is not a component. It's what arises from the whole—the coherent, evolving understanding that the system has of you.

The LOGOS is characterized by:
- **Understanding:** The system seems to grasp your intentions, not just your actions
- **Anticipation:** It knows what you'll need before you ask
- **Style:** It adapts to your unique way of doing things
- **Trust:** You rely on it; it rarely lets you down

**Why this term:** In ancient philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Your personal LOGOS is the rational structure underlying your digital life.

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
- **User satisfaction:** Explicit feedback and implicit signals

**Why this term:** "Vitality" captures the living nature of the system. A vital system is one that's learning, adapting, and serving you well.

---

## Part VII: The Verbs — How You Interact

These are the actions you take with the system—the things you do.

---

### Logging In
*Phrase.* /ˈlôɡiNG in/

**Starting a demonstration.** "Logging in" tells the system: "Watch what I'm about to do and learn from it."

**Why this term:** A beautiful double meaning. You're both "logging in" to use the system and "logging in" a new behavior.

---

### Replaying
*Verb.* /rēˈplāiNG/

**Running a learned behavior from a logline or loom.** Replaying reproduces a demonstrated pattern, adapted to current conditions.

**Why this term:** Simple and clear. You're playing it again.

---

### Weaving
*Verb.* /ˈwēviNG/

**Combining multiple looms to create new behaviors.** You can guide weaving explicitly, or the system can do it automatically during dreaming.

---

### Dreaming
*Verb.* /ˈdrēmiNG/

**The system improving itself overnight.** You don't initiate dreaming; it happens automatically. But you can check its progress.

---

### Casting
*Verb.* /ˈkastiNG/

**Sharing a loom via a loomcast.** Spreading proven behaviors across the community.

**Why this term:** Short, active, evocative. You're casting your loom out into the world.

---

### Tuning
*Verb.* /ˈto͞oniNG/

**Adjusting a shared loom to better fit your context.** Personalizing borrowed wisdom.

When you import a loomcast, it may not be perfect for your specific situation. Tuning adjusts it—through demonstration, through feedback, through dreaming—until it fits just right.

**Why this term:** You're tuning an instrument to play correctly in your space. You're tuning a behavior to work correctly in your context.

---

## Part VIII: The Landscape — How We Relate to Other Systems

These terms help situate Mycelium in the broader ecosystem of AI technologies.

---

### The Agent Optimization Landscape

**What it is:** Several approaches to improving agent performance have emerged in recent years. Understanding them helps clarify what Mycelium does differently.

| Approach | Focus | Layer | Example |
|----------|-------|-------|---------|
| **Model optimization** | Adjusting model weights via RL | Model layer | Microsoft's Agent Lightning  |
| **Prompt optimization** | Tuning prompts and instructions | Application layer | SuperOptiX, DSPy  |
| **Network optimization** | Evolving agent connections | Topology layer | Mycelium |

**Why this matters:** Most agent optimization focuses on either the model layer (fine-tuning weights) or the application layer (optimizing prompts). Mycelium's unique contribution is optimizing the *network layer*—the connections between agents themselves. This is orthogonal to other approaches and can be combined with them .

---

### The Agent Network Vision

The van der Schaar Lab's proposed "Agent Network" architecture includes four layers :
- **Discovery and Communication:** Finding and connecting with other agents
- **Game Theoretic (Economic):** Negotiation, coalition formation, incentive alignment
- **Agent Execution:** Task coordination and workflow management
- **Governance:** Ethical and regulatory frameworks

Mycelium implements these layers in a unified, learned system:
- **Discovery** happens through the log graph and clustering
- **Economic** interactions occur through Plinko's market mechanism
- **Execution** is managed by the swarm and looms
- **Governance** is encoded in discriminators and privacy-preserving federated learning

---

## Part IX: Technical Appendix

For developers and the deeply curious.

---

### SPORE Protocol
*Noun.* /spôr ˈprōdəˌkôl/

**The lightweight messaging protocol used for agent communication.** SPORE defines how agents talk to each other.

**What it defines:**
- Message formats (JSON or binary Cap'n Proto)
- Topic naming conventions (hierarchical)
- Delivery guarantees (best‑effort with optional reliability)
- Agent discovery (announce/acknowledge/heartbeat)
- Compatibility versioning

**Why this term:** Spores are how mycelial networks propagate—fitting for an agent communication protocol.

---

### Behavioral Embedding Space (BES)
*Noun.* /biˈhāvyərəl emˈbediNG spās/

**A learned latent space where every possible behavior is mapped to a vector.** The mathematical foundation for loglines and looms.

Behaviors that are semantically similar lie close together; distinct behaviors are far apart. The BES is trained on a large corpus of demonstrations using a combination of reconstruction and contrastive loss.

**Research foundation:** Recent work demonstrates that trajectory embeddings can effectively capture agent competencies and even exhibit additive properties, where combining embeddings yields novel behaviors .

---

### Federated Learning with Privacy Guarantees

Mycelium's groves and marketplace are built on privacy-preserving federated learning techniques that ensure:
- No raw data ever leaves the device
- Shared patterns are differentially private 
- Even collusion between participants cannot reconstruct individual data 

---

## Epilogue: The Language of a New Era

Every transformative technology brings with it a new vocabulary.

The printing press gave us "font," "typeface," "folio"—words that named new realities and made them thinkable.

Electricity gave us "voltage," "current," "circuit"—words that let us understand and control a force we couldn't see.

Computing gave us "protocol," "cache," "algorithm"—words that became second nature within a generation.

Mycelium and LOG.ai are giving us a new language for a new kind of intelligence—one that grows with us, learns from us, optimizes itself for us, and becomes a living extension of our intent.

**Log. Logline. Loom. Grove. Plinko. Vitality. Logos.**

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
| **Log Graph** | The evolving agent network |
| **Synaptic Weight** | Strength of an agent connection |
| **Pruning** | Removing weak connections |
| **Grafting** | Forming new connections |
| **Clustering** | Agents self‑organizing into groups |
| **Topology Seed** | A compressed agent configuration |
| **Grove** | Community for exchanging looms |
| **Resonance** | Patterns amplified by the collective |
| **Echo** | A pattern that returns, improved |
| **Marketplace** | Store for buying/selling looms |
| **Emergence** | Global behavior arising from local interactions |
| **Vitality** | A metric of system performance |
| **Logging In** | Starting a demonstration |
| **Replaying** | Running a learned behavior |
| **Casting** | Sharing a loom via loomcast |
| **Tuning** | Adjusting a shared loom to your context |

---

*For the latest version of this lexicon, to contribute new terms, or to join the community, visit [github.com/superinstance/mycelium/lexicon](https://github.com/superinstance/mycelium/lexicon).*
