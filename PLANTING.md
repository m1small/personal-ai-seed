# Planting Guide

How to go from zero to a growing Personal AI tree.

## Before You Plant

You need:
- A git-capable environment (terminal, VS Code, etc.)
- An AI coding tool that can read and edit files (Claude Code, Cursor, GitHub Copilot, etc.)
- A willingness to build and use your system concurrently — that's how it grows

## Phase 1: Plant (10 minutes)

### Fork and clone

```bash
# Fork this repository on GitHub, then:
git clone https://github.com/YOUR-USERNAME/personal-ai-seed.git
cd personal-ai-seed
```

### Read the framework

Read these two files. They are the trunk of your tree:

1. **`glossary.md`** — The vocabulary. Every term used in the system has an agreed definition.
2. **`processes.md`** — How work happens. Focus on: The Loop, Initialization, Session Lifecycle, Artifact Production.

Don't memorize them — your AI will reference them every session. But read them once so you understand what you're building on.

## Phase 2: First Session — Grow Your Trunk (30 minutes)

### Open your first session

Open the repository in your AI coding tool. If you're using Claude Code, it will automatically read `CLAUDE.md` and initialize.

For other tools, paste the contents of `prompts/bootstrap.md` as your opening prompt.

### Declare Developer Mode

Tell your AI: **"Developer Mode."**

This is your first session. The AI will:
1. Read the library (glossary, processes, schemas)
2. Run Drift Detection (nothing to detect yet — clean start)
3. Register this session in `system/state-session.md`
4. Ask you what to work on

### Create your environment state file

Tell the AI what tools you have connected. It will probe your environment and produce an environment state file at `system/env-{your-name}.md` documenting:
- Which surface you're on (Claude Code, Cursor, etc.)
- Which tools are connected and their connection methods
- Verified capabilities for each tool
- Known limitations

This is your root system — what your tree can draw from.

### Update CLAUDE.md (or your platform's equivalent)

Update the entry point to reference your new environment file. This ensures every future session knows your setup.

### First commit

Your AI will commit:
- Environment state file
- Updated CLAUDE.md
- Session state registration

**Congratulations — your tree has roots and the beginning of a trunk.**

## Phase 3: Grow Your First Branch (next session)

A branch is a life domain. Pick one that matters to you right now:

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

## Phase 4: First Execution (next session)

### Switch to Execution Mode

Tell your AI: **"Execution Mode."**

Now use your system. Ask your agent to do real work. The AI will:
1. Load the agent definition and its certifications
2. Follow the agent's decision rules
3. Produce output in `outputs/`
4. Track performance for trust evaluation

### Capture your first retrospective

At session close, the AI captures a retrospective: what worked, what caused friction, what to improve. This is The Loop in action — using the system teaches you what to build next.

## Phase 5: The Loop Takes Hold

From here, growth is organic:

- **Developer Mode sessions** improve the system itself — new agents, refined processes, better schemas.
- **Execution Mode sessions** use the system to get work done — and surface what needs building.
- **Dream Mode sessions** (optional) give your AI a reflective space — `dream/CLAUDE.md` bootstraps it.

The two sides feed each other. That's The Loop. That's how your tree grows.

## What Not to Do

- **Don't try to build everything at once.** One branch at a time. Let execution reveal what's needed.
- **Don't skip the vocabulary.** The glossary exists so you and your AI share a language. Ambiguity is friction.
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

**What if I want to rename things?**
Go for it. The glossary is yours. Just update all references — the AI will help you find them.
