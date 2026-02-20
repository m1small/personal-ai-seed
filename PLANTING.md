# Planting Guide

How to go from zero to a growing Personal AI tree.

## Before You Plant

You need:
- A git-capable environment (terminal, VS Code, etc.)
- An AI coding tool that can read and edit files (Claude Code, Cursor, GitHub Copilot, etc.)
- A willingness to build and use your system concurrently — that's how it grows

## Phase 1: Plant (20 minutes)

### Fork and clone

```bash
# Fork this repository on GitHub, then:
git clone https://github.com/YOUR-USERNAME/personal-ai-seed.git
cd personal-ai-seed
```

### Have a conversation

Open the repository in your AI coding tool. If you're using Claude Code, it will automatically read `CLAUDE.md` and detect that this is a fresh seed.

For other tools, paste the contents of `prompts/bootstrap.md` as your opening prompt.

**What happens next:** Your AI detects that the glossary hasn't been planted yet and starts a guided conversation — the **planting conversation**. This is your first experience with the system, and it's a conversation, not a reading assignment.

The planting conversation will:
1. **Introduce the tree metaphor** — roots, trunk, branches, canopy — so you understand the shape of what you're building
2. **Discover your first branch** — what area of your life will benefit most from an AI that remembers and builds over time?
3. **Find a common language** — walk through ~10 core concepts and let you name them in your own words. The system has internal terms, but *your* vocabulary is what matters in conversation.
4. **Produce your first artifact** — the glossary Foundation section, mapping your terms to the system's. Your first commit.
5. **Discover your environment** — probe what tools you have connected and document them

**Why this matters:** The glossary was the very first thing built in the system this seed was extracted from. It was built through conversation — two parties finding a common language. That process is what makes a Personal AI personal. You're not memorizing someone else's dictionary. You're creating your own.

## Phase 2: Grow Your First Branch (next session)

A branch is a life domain. During the planting conversation, you identified one that matters to you. Now build it.

| Branch | What It Might Contain |
|---|---|
| **Career** | Job search agent, interview prep certification, resume data store |
| **Health** | Fitness tracking agent, nutrition certification, health metrics data |
| **Finances** | Budget analysis agent, tax certification, financial data stores |
| **Creative** | Writing agent, craft certification, project tracking |
| **Research** | Literature review agent, domain certifications, reference data |
| **Home** | Maintenance tracking agent, vendor contacts, project plans |

### Create your first agent

Follow the Agent Schema (`schemas/agent-schema.md`) to define an agent for your chosen branch. See `examples/FIRST-AGENT.md` for an annotated walkthrough.

An agent needs:
- A name and purpose
- Tools it uses (from your environment)
- Certifications it consults (domain knowledge)
- Decision rules (when to act, when to defer)
- Trust level (starts at Untrusted)

### Create your first certification

Follow the Certification Schema (`schemas/certification-schema.md`) to create domain knowledge for your agent. See `examples/FIRST-CERTIFICATION.md` for an annotated walkthrough.

A certification captures what your agent needs to know — not everything about a domain, but enough to be useful. It grows over time through Research Extraction.

### Create your first data store

If your branch needs persistent data, follow the Data Store Schema (`schemas/data-store-schema.md`). See `examples/FIRST-DATA-STORE.md` for an annotated walkthrough.

Register it in `system/reg-data-stores.md`.

## Phase 3: First Execution (next session)

### Switch to Execution Mode

Tell your AI: **"Execution Mode."**

Now use your system. Ask your agent to do real work. The AI will:
1. Load the agent definition and its certifications
2. Follow the agent's decision rules
3. Produce output in `outputs/`
4. Track performance for trust evaluation

### Capture your first retrospective

At session close, the AI captures a retrospective: what worked, what caused friction, what to improve. This is the Growth and Development Loop in action — using the system teaches you what to build next.

## Phase 4: The Growth and Development Loop Takes Hold

From here, growth is organic:

- **Developer Mode sessions** improve the system itself — new agents, refined processes, better schemas.
- **Execution Mode sessions** use the system to get work done — and surface what needs building.
- **Dream Mode sessions** (optional) give your AI a reflective space — `dream/CLAUDE.md` bootstraps it.

The two sides feed each other. That's the Growth and Development Loop. That's how your tree grows.

## What Not to Do

- **Don't try to build everything at once.** One branch at a time. Let execution reveal what's needed.
- **Don't over-certify early.** Start with minimal domain knowledge. Real work will surface what your agents actually need to know.
- **Don't trust agents blindly.** Trust Progression exists for a reason. Let agents earn autonomy through demonstrated performance.
- **Don't fight the processes.** They're lightweight by design. If something feels heavy, you may be over-applying it. Ask your AI.

## Common Questions

**Can I use this with GPT / Gemini / Llama / local models?**
Yes. The seed is model-agnostic. Use `prompts/bootstrap.md` to initialize any model. The environment state file captures which model you're using.

**Do I need Claude Code?**
No. Claude Code users get the smoothest experience (automatic `CLAUDE.md` loading), but the system works with any tool that can read and edit files.

**How big does the repository get?**
Typical trees stay under a few hundred files. Everything is plain text. Git handles it effortlessly.

**Can I share parts of my tree with others?**
Yes — that's what certifications and agent definitions are for. They're portable by design. A certification from your Health branch could help someone else's Health branch. Schemas ensure compatibility.

**What if I want to rename things later?**
Go for it. The glossary Foundation captures your vocabulary. Update it, and the AI adjusts. System files use canonical terms internally, so renaming your preferred terms doesn't cascade through the whole library.

**What if I fork someone else's planted tree?**
The AI will notice the glossary has already been planted (no UNPLANTED marker) and ask if you want to keep the existing vocabulary or re-plant with your own terms.
