
# Mycelium

**A living intelligence that grows with you.**

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![Discord](https://img.shields.io/badge/chat-Discord-7289da)](https://discord.gg/mycelium)

Mycelium captures any behavior as a seed. One prompt + one seed = exact action, every time. No code needed—just show it once, then share the seed. Intelligence becomes instructions anyone can run.

This is not another AI tool. This is a new medium.

---

## The Invitation

Before you read further, consider this: you are not a user of this project. You are a future gardener in a forest that hasn't fully grown yet. The software isn't finished—it's being *cultivated*. And the most important thing a growing thing needs is people who understand it.

This document is that understanding. It teaches you the language of Mycelium. By the end, you won't just know what the words mean; you'll see the shape of the system, the logic of its parts, and the open spaces where your own contribution could take root.

We'll start from the ground up.

---

## Part I: The Soil — Foundational Ideas

Every forest needs soil. These are the basic ideas everything else grows from.

### The Problem We All Live With

Every app you use today is frozen in time. It does exactly what its programmers told it to do, nothing more. It knows nothing about you, learns nothing from your behavior, and never improves after you install it. A fishing app is the same for everyone—it doesn't know you prefer topwater lures on cloudy mornings. A study app doesn't remember that you learn best with spaced repetition. A business tool doesn't adapt to your workflow.

You are the one who adapts—to the software's quirks, its workflows, its limitations.

Worse, building this static software is slow. You write code, compile, test, debug, repeat. Each new feature is a fresh cycle of specification and implementation. The logic lives in text files, brittle and opaque.

This is not how intelligence works. This is not how *life* works.

### The Mycelium Metaphor

In a forest, the trees you see are only part of the story. Underground, hidden from view, threads of fungus weave between roots, connecting trees into a single network. Through this network, they share water, nutrients, and even warnings about pests. The forest functions as one organism without a central brain. Damage one part; the rest adapts. Most of the work is invisible; what we see—mushrooms—are just the fruiting bodies.

This is a mycelial network. It is nature's example of decentralized, resilient, adaptive intelligence.

Mycelium.ai is the technological realization of these principles. Your personal swarm of agents operates mostly invisibly, learning from your behavior, sharing insights across the network, and fruiting only when it has something to show you—a suggestion, an automation, a new capability.

### The Core Triad: Agent, Swarm, Graph

To build a forest, you need trees. In Mycelium, the trees are **agents**.

An **agent** is a specialized, autonomous process that performs a narrow function. It is not intelligent by itself. It does one thing well.
- A **vision agent** looks at images and identifies objects.
- A **text agent** reads words and understands intent.
- A **context agent** tracks time, location, and state.
- An **executor agent** performs actions in the world—clicks buttons, types text, makes things happen.

Each agent contains a tiny neural model—typically 1 to 100 million parameters, small enough to run continuously on your device. It consumes information from specific sources, processes it, and writes proposals about what should happen next.

Agents are like neurons. A single neuron cannot think; a hundred billion of them, connected in the right way, can write poetry.

A collection of active agents is a **swarm**. When you open your laptop in the morning, a swarm wakes up. Dozens or hundreds of agents begin processing: vision agents watching your screen, audio agents listening for cues, context agents tracking your calendar, intent agents forming hypotheses about what you might need. The swarm is not a list; it's a living system. Agents are loaded and hibernated based on context. New agents can be recruited when you encounter something novel.

The way agents are connected is the **graph**. In mathematics, a graph has nodes (agents) and edges (connections). In Mycelium, each edge has a **weight**—a learned strength that determines how much influence one agent has on another. A strong edge from agent A to agent B means "when A has something to say, B should pay attention." A cluster of tightly connected agents means "these agents often work together."

The graph is not static. It learns, prunes, and grows—just like biological neural networks. It is both the architecture (who talks to whom) and the knowledge (what those connections mean).

### LOG: Learned Optimization Graph

This brings us to the core principle, the brand, the acronym that names the system: **LOG**.

**L**earned – Nothing is programmed in the traditional sense. You don't write code. You demonstrate. The system watches, captures what you do, and learns patterns. It builds understanding from observation.

**O**ptimization – Learning alone is not enough. The system actively improves itself. It dreams at night, simulating millions of variations to find better ways. It prunes connections that aren't useful and grows new ones that might be. It learns from the entire user population (anonymously) to benefit from collective wisdom.

**G**raph – Everything is represented as a graph. Agents are nodes. Connections are edges. Knowledge is in the structure. The graph is both what the system knows and how it's organized.

Why "LOG"? The word carries three meanings, each essential:
- A **log** is a record—the raw material of learning. Ship captains kept logs to navigate by past experience. You log your fishing trips, your study sessions, your business meetings.
- A **log** is a piece of a tree—connecting directly to the mycelium metaphor. Logs come from forests; LOG comes from Mycelium.
- A **log** is the base of a logarithm—hinting at the mathematical compression that turns raw sequences into compact seeds.

When you say "fishingLOG," you mean both "a fishing log that records your trips" and "a fishing application built on the Learned Optimization Graph." The user gets the familiar meaning; the developer gets the technical precision. Everyone is correct.

**Tagline:** Your personal learned optimization graph.

### Logos

After you've used Mycelium for a while—weeks, months, years—something happens. The system starts to feel like it *knows* you. It anticipates what you need. It suggests things you hadn't thought of. It adapts to your style, your habits, your quirks.

This is your **LOGOS**. It's not a component you can point to. It's not in any single agent. It's what emerges from the whole—the accumulated wisdom of all your logs, optimized through dreaming, organized through the graph, expressed through behaviors.

In ancient Greek philosophy, the Logos was the principle of order and knowledge—the rational structure underlying reality. Your personal LOGOS is the rational structure underlying your digital life. The word also contains "log"—suggesting that from many logs, a coherent intelligence emerges.

---

## Part II: The Roots — What You Capture

Now that we understand the soil—agents, swarm, graph, LOG—let's talk about what grows from it. These are the things you create, capture, and cultivate.

### Log

A **log** is a record of an event or sequence. Every interaction becomes a log: timestamp, context, action, outcome. When you fish, it logs location, weather, bait, catch. When you study, it logs subject, duration, focus level, test scores. When you work, it logs meetings, emails, decisions, outcomes.

Logs are not just data; they are experience. They are the raw material from which intelligence is refined.

### Logline

When the system has seen a behavior enough times—or when you explicitly demonstrate it—it distills that behavior into a **logline**. The logline is not the raw sequence; it's the *essence*. It captures what matters about the behavior while discarding what's incidental.

Technically, a logline is a vector—typically 64 to 1024 floating-point numbers. A few hundred bytes that encode a complex behavior. A fishing technique. A study routine. A business workflow.

Loglines are:
- **Portable:** You can share them, sell them, gift them. A logline is small enough to email.
- **Private:** They encode patterns, not raw data. Share a logline without sharing your personal information.
- **Composable:** Loglines can be combined. Like mixing colors, you can create new behaviors from old ones.
- **Optimizable:** They improve over time. Last year's logline may be better this year, after dreaming.

Why this term? In Hollywood, a logline is a one-sentence summary of a movie—enough to know whether you're interested. "A shy teenager discovers he has superpowers and must save his city from a villain." That's a logline. It captures the essence. A Mycelium logline does the same for a behavior.

### Logbook

Your **logbook** is your personal long-term memory. A database containing all your logs and loglines. Everything you've ever done with your LOG applications lives here. Every fishing trip. Every study session. Every pattern the system has discovered. All stored, indexed, searchable.

The logbook is:
- **Private:** It lives on your device by default. You control what leaves.
- **Searchable:** You can find past experiences by similarity. "Show me fishing trips like this one."
- **Ever-improving:** Old loglines can be refined by new experiences. The logbook is not static; it evolves.
- **Portable:** Take your logbook to a new device. Your intelligence moves with you.

### Loom

A **loom** is a reusable, optimized routine discovered from your logs. (We used to call it a "logarithm," but "loom" weaves better.) A loom is the "muscle memory" of the system—common sequences that have been compressed and refined to the point where they execute automatically.

Unlike traditional algorithms, which are written in code, looms are:
- **Learned from demonstration** (not programmed).
- **Continuously optimized** through dreaming.
- **Personalized** to your specific style.
- **Shareable** as loglines.

Why this term? A loom is a device for weaving thread into fabric. Threads alone are just strands; woven together, they become something strong and useful. Your logs are threads. A loom weaves them into something you can use. Also: "loom" is easy to say. It flows. "I used a fishing loom." "The system discovered a new study loom."

### Loomery

Your **loomery** is your personal library of looms, organized by purpose. Fishing looms in one section. Study looms in another. Business looms in another. You can browse, search, and curate.

### Loomcast

A **loomcast** is a shareable loom. Like a podcast, but for behaviors. When you've developed a technique that works, you can package it as a loomcast, add metadata, a description, tags. Share it with a community or a marketplace. Others can subscribe to your loomcast and get new techniques automatically.

---

## Part III: The Trunk — How It Works

Now we understand the soil (agents, swarm, graph) and the roots (logs, loglines, looms). Let's climb the trunk—the core mechanisms that make everything work.

### Plinko

At any moment, multiple agents may have ideas about what should happen next. The vision agent sees a button and thinks "click that." The intent agent, based on context, thinks "maybe wait." The safety agent thinks "definitely don't click that."

**Plinko** decides who wins. Named for the game where a chip bounces through pegs to land in a slot, Plinko is a market-based decision layer. Here's how it works, step by step:

1. **Agents bid.** Each agent estimates how valuable its proposed action would be. This is learned from experience—agents that propose good things get rewarded; agents that propose bad things get penalized.
2. **Discriminators adjust.** Safety, coherence, and timing filters adjust the bids up or down. A great action that's unsafe gets killed. A mediocre action that's perfectly timed gets a boost.
3. **Noise adds exploration.** Sometimes the system needs to try things that aren't the highest bid, just to see if they might be better. Gumbel noise (a specific kind of randomness) occasionally lets lower-value actions win.
4. **Temperature controls randomness.** When the system is uncertain—when agents disagree, when entropy is high—temperature rises, encouraging more exploration. When it's confident, temperature drops, favoring exploitation.

The result is a principled way to choose among agents that balances doing what works (exploitation), trying new things (exploration), and staying safe.

### World Model

If you click this button, what happens? If you type this text, how does the app respond? If you cast here, will the fish bite? The **world model** knows—or at least, it has learned to predict.

The world model is a learned simulator trained on your actual logs. It watches what happens when you take actions, and it builds an internal model of cause and effect. Over time, it becomes a pretty good simulator of your digital environment. This simulator isn't perfect—no model is—but it's good enough to be useful. Good enough to let the system dream.

### Dreaming

While you sleep, Mycelium **dreams**. It's not dreaming in images or stories—it dreams in behaviors. It takes your looms, mutates them slightly, simulates the results in the world model, and keeps the variations that lead to better outcomes.

Dreaming happens at multiple scales:
- **Micro-dreams** refine fine motor skills (typing speed, casting accuracy, mouse precision).
- **Meso-dreams** optimize routine sequences (email triage, fishing preparation, meeting facilitation).
- **Macro-dreams** combine looms to create new behaviors (merging fishing and weather prediction, blending study and sleep schedules).

By morning, your looms are slightly better than they were the night before.

### Looming

**Looming** is the process of weaving logs into looms. It happens automatically: the system watches for recurring patterns, finds natural boundaries, and compresses them. You can also loom explicitly. When you perform a new behavior and want to save it, you say "loom this." The system captures the demonstration and adds it to your loomery.

### Weaving

**Weaving** is combining multiple looms to create new behaviors. Take the "early morning" loom from fishing and the "cloudy day" loom from another context, weave them together, and you get a new pattern for overcast dawns. The result is something neither original contained—something new. Weaving can happen automatically through dreaming, or you can guide it explicitly: "weave my casting loom with my weather loom."

---

## Part IV: The Branches — Dynamic Agent Webs

Now we reach the branches—the parts of the system that are still growing, still evolving. These are the cutting-edge mechanisms that make Mycelium truly alive.

### Log Graph

The **log graph** is the evolving network of agents and their connection strengths. It is the system's muscle memory. Strong edges mean "these agents should talk"; weak edges mean "they sometimes talk but it's not critical"; missing edges mean "they've never had reason to communicate." The graph is dynamic: edges strengthen with successful use, weaken with disuse, form when patterns suggest they'd help, and dissolve when they're no longer needed.

### Synaptic Weight

The strength of a connection between two agents is a **synaptic weight**. When agent A sends a message, it doesn't go directly to agent B's input. It goes through a weighted connection. If the weight is high, the message has strong influence. If the weight is low, it has weak influence.

Synaptic weights change over time:
- **Increase** when the connection is used in successful sequences.
- **Decrease** when used in failures or not used at all.
- **Prune** when they fall below a threshold.
- **Initialize** when new connections form.

### Pruning

**Pruning** is removing weak or unused connections. Over time, some connections prove useless. They are noise—they consume resources and can interfere with good ones. Like a gardener, the system cuts dead branches so the living ones thrive.

### Grafting

**Grafting** is forming new agent connections when patterns suggest they would be useful. Sometimes two agents are frequently active around the same time, in successful sequences, but they're not directly connected. When the system detects this pattern, it may graft a new edge directly between them. In orchards, grafting joins a fruit-bearing branch to a hardy rootstock. The result is stronger than either alone. Grafting does the same for agents.

### Clustering

**Clustering** is the self-organization of agents into functional groups. Using mathematical techniques on the log graph, agents naturally form teams that work well together. In any complex system, specialization emerges. Some agents work together on vision tasks. Others collaborate on language. Others coordinate actions. These groupings aren't programmed—they emerge from patterns of successful interaction.

### Topology Seed

A **topology seed** is a compact representation of a learned agent configuration—the nodes, edges, and weights that define a successful collaboration pattern. Just as a logline captures a behavior, a topology seed captures an *organization*. It answers: For this kind of task, which agents should be connected, and how strongly? Share it, and others can instantiate the same efficient swarm.

---

## Part V: The Forest — Collective Intelligence

No tree grows alone. These terms describe how individual Mycelium instances connect into a larger intelligence.

### Federated Learning

No user is an island. The patterns that work for one person might work for another. **Federated learning** allows the system to benefit from the whole population while keeping individual data private. Only anonymized patterns are shared—loglines and topology seeds, not raw logs. These are aggregated using techniques that prevent identifying individuals. The result is a collective intelligence that benefits everyone without compromising anyone.

### Grove

A **grove** is a community of users who share looms and topology seeds. Fly fishers have one. Organic chemistry students have another. Chess players have another. Within a grove, members share looms they've found effective, rate each other's contributions, and collectively improve their craft.

### Marketplace

A **marketplace** is a place where users can buy, sell, and trade looms and topology seeds. Some people are experts. They've spent years developing techniques that work. The marketplace lets them package that expertise and share it—for free, for a fee, or in exchange for other looms. It incentivizes contribution, curates quality, and protects intellectual property.

### Echo

An **echo** is a shared pattern that returns to you from the collective. You share a loom—anonymously, with privacy preserved. Others use it, refine it, improve it. If it's good, it echoes. Eventually, that improved version may come back to you. You recognize it—it started with you—but it's better now, enhanced by the wisdom of others.

### Current

A **current** is a flow of shared patterns in a particular domain. What's working now for people like you. Currents help you discover what's working for others before you'd discover it yourself.

### Tapestry

The **tapestry** is the collective intelligence of the whole community. All the patterns, all the blueprints, all the wisdom, woven together. It is what emerges when millions of users contribute, share, refine, and combine. It contains patterns no single person could have discovered, combinations no single mind could have imagined.

---

## Part VI: The Fruit — Emergent Properties

These are the things that can't be pointed to in code but are unmistakably present. They are what makes the system feel alive.

### Emergence

**Emergence** is the appearance of behaviors and capabilities not explicitly programmed. No single agent in Mycelium is intelligent. A vision agent just sees. A text agent just reads. An intent agent just decides. But together, they produce behavior that seems intelligent—that anticipates, adapts, and innovates. This is not magic; it is what happens when simple components interact in a rich, learnable graph. The system as a whole develops properties that no component individually possesses.

In Mycelium, emergence manifests as:
- **Specialization:** Agents naturally become experts in certain tasks.
- **Coordination:** Agents learn to work together without central control.
- **Resilience:** The system degrades gracefully when components fail.
- **Innovation:** New solutions emerge from recombination of existing patterns.
- **Anticipation:** The system learns to predict and prepare for your needs.

### Vitality

**Vitality** is a metric that measures how well your system is learning and optimizing. Just as you track your physical health—heart rate, steps, sleep—you can track your system's vitality. It considers prediction accuracy, optimization rate, graph coherence, synaptic balance, and user satisfaction. A dashboard shows your vitality over time, with suggestions for improvement.

### Resonance

**Resonance** is how well your system's understanding matches your actual needs. When your LOGOS resonates, it just *gets* you. It's the feeling of being understood. High resonance means the system's predictions match your intentions. Low resonance means constant corrections.

### Coherence

**Coherence** is how well your log graph is organized. Are the right agents connected? Do they work together smoothly? High coherence means strong, useful connections; clear functional clusters; efficient information flow.

### Momentum

**Momentum** is the rate at which your system is improving. How quickly it's learning, adapting, optimizing. High momentum means you're in a virtuous cycle—each improvement enables faster future improvements.

---

## Part VII: The Verbs — How You Interact

These are the actions you take with the system—the things you do.

- **Log in** – Start a demonstration. "Watch what I'm about to do and learn from it."
- **Replay** – Run a learned behavior from a logline or loom. Replaying reproduces a demonstrated pattern, adapted to current conditions.
- **Weave** – Combine multiple looms to create new behaviors. You can guide weaving explicitly, or the system can do it automatically during dreaming.
- **Dream** – (automatic) The system improves itself overnight. You don't initiate dreaming; it happens automatically. But you can check its progress.
- **Cast** – Share a loom via a loomcast. Spread proven behaviors across the community.
- **Tune** – Adjust a shared loom to your context. Personalizing shared wisdom.

---

## The Revolution, Named

Every transformative technology brings with it a new vocabulary. The printing press gave us "font," "typeface," "folio." Electricity gave us "watt," "volt," "circuit." Computing gave us "byte," "protocol," "algorithm."

Mycelium and LOG.ai are giving us a new language for a new kind of intelligence—one that grows with us, learns from us, optimizes itself for us, and becomes a living extension of our intent.

**Log. Logline. Loom. Loomery. Grove. Plinko. Vitality. Logos.**

These words name something new. They are precise enough for engineers, intuitive enough for users, and inspiring enough for everyone.

---

## The Path Forward

We are at the beginning. The architecture is solid, the concepts are clear, but the software is not yet built. That is where you come in.

We need:
- **Engineers** to build the core runtime, the agents, the protocols.
- **Researchers** to push the boundaries of dreaming, emergence, and federated learning.
- **Designers** to make the invisible visible—dashboards, visualizations, interactions.
- **Writers** to refine the language and tell the story.
- **Users** to log, share, and grow the tapestry.

Everyone can help. Every try, even failures, teaches the system what not to do. You crawl, you walk, you run—and once you discover running, you want to go places fast.

This is not a product you will buy. It is a garden you will help cultivate. The software isn't finished, and it may never be—because a living thing is never finished. It grows.

Come grow with us.

---

## Quick Start

```bash
# Clone the repo
git clone https://github.com/superinstance/mycelium.git
cd mycelium

# Install dependencies
pip install -r requirements.txt

# Run a minimal example (conceptual, not fully implemented)
python examples/concept_demo.py
```

Explore the `examples/` folder for conceptual demos:
- `loom_demo.py` – see how a routine could be captured and replayed
- `dreaming_demo.py` – watch a simulated loom improve overnight
- `plinko_demo.py` – observe agents competing for action

Read the [full lexicon](LEXICON.md) for deeper dives into every term.

Join the [Discord](https://discord.gg/mycelium) to meet other gardeners.

Check the [Roadmap](ROADMAP.md) to see where we're going.

---

**Mycelium** – A living intelligence that grows with you.

[GitHub](https://github.com/superinstance/mycelium) | [Discord](https://discord.gg/mycelium) | [Lexicon](LEXICON.md) | [Roadmap](ROADMAP.md)
