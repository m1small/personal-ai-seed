# Personal AI Seed

A way of working — not an app, not a framework, not a chatbot wrapper. A **library-based operating system** for orchestrating work between you and AI models across sessions, surfaces, and life domains.

This is the seed. What grows from it is your tree.

## The Tree

```
                    ╭─────────────────────────╮
                    │   Insights + Actions     │  ← Canopy
                    │  (surfaced by agents,    │    What your system produces.
                    │   approved by you)       │    Briefings, analyses, drafts,
                    ╰────────────┬────────────╯    decisions — through your
                                 │                  approval gate.
                 ┌───────────────┼───────────────┐
                 │               │               │
           ┌─────┴─────┐  ┌─────┴─────┐  ┌─────┴─────┐
           │  Health    │  │  Career   │  │ Finances  │  ← Branches
           │           │  │           │  │           │    Life domains.
           │  agents   │  │  agents   │  │  agents   │    Each branch has agents,
           │  certs    │  │  certs    │  │  certs    │    certifications, data,
           │  data     │  │  data     │  │  data     │    and personas.
           └─────┬─────┘  └─────┬─────┘  └─────┬─────┘
                 │               │               │
                 └───────────────┼───────────────┘
                                 │
                    ╭────────────┴────────────╮
                    │   Processes & Conventions│  ← Trunk
                    │   The Loop               │    How work happens.
                    │   Session Lifecycle       │    The way of working that
                    │   Trust Progression       │    makes everything above
                    │   Schemas & Rules         │    possible.
                    ╰────────────┬────────────╯
                                 │
                    ╭────────────┴────────────╮
                    │   Your Data              │  ← Personal Data
                    │   Version-controlled     │    Everything your system
                    │   markdown + CSV         │    knows, versioned in git.
                    ╰────────────┬────────────╯
                                 │
                    ╭────────────┴────────────╮
                    │   LLM Services           │  ← Roots
                    │   Claude, GPT, Llama,    │    Any model, any surface.
                    │   local or cloud         │    The system is model-agnostic.
                    ╰─────────────────────────╯
```

## What Makes This Different

**Library-based.** Everything is version-controlled markdown. Your processes, agent definitions, domain knowledge, data stores — all plain text in a git repository. No proprietary formats, no vendor lock-in, no database to manage.

**Model-agnostic.** The seed works with any LLM that can read files and follow instructions. Claude, GPT, Llama, Gemini — the system adapts. You declare your environment; agents consult it.

**Trust-governed.** Agents start untrusted. They earn autonomy through demonstrated performance tracked in a trust ledger. You control the blast radius of every capability.

**Self-improving.** The Loop — a continuous dev/ops cycle — means your system gets better through use. Every session is an iteration. Errors and friction are inputs, not waste. You build and execute concurrently.

**Session-native.** Each conversation has a lifecycle: initialize, scope, work, review, close. Drift detection normalizes what changed between sessions. Nothing falls through the cracks.

## How It Grows

The Loop is the growth mechanism:

```
    ╭──── Dev ────╮         ╭──── Ops ────╮
    │             │         │             │
    │  Converse   │         │  Detect     │
    │  Produce    │ ──────> │  Sweep      │
    │  Commit     │         │  Triage     │
    │             │ <────── │             │
    ╰─────────────╯         ╰─────────────╯
```

**Dev side:** You and your AI have a conversation, produce artifacts, and commit changes.

**Ops side:** The system detects drift, sweeps for health, and triages findings into future work.

**The crossover:** Dev commits become ops state. Ops findings become dev work. This is how a tree grows — building and sustaining happen simultaneously.

## What's in the Seed

```
personal-ai-seed/
  glossary.md              Controlled vocabulary.
  processes.md             How work happens.
  CLAUDE.md                Entry point (Claude Code users).

  schemas/                 Structural definitions.
  .claude/rules/           Enforceable process extracts.
  system/                  Infrastructure and state.
  tools/                   Tool integration contracts.
  prompts/                 Bootstrap for non-Claude surfaces.
  dream/                   Reflective space.

  agents/                  Empty — you grow these.
  certifications/          Empty — you grow these.
  personas/                Empty — you grow these.
  data/                    Empty — you grow these.
  plans/                   Empty — you grow these.
  examples/                Annotated walkthroughs.
```

The seed gives you the trunk — processes, schemas, governance, and conventions. The branches are yours to grow.

## The Hierarchy

- **Seed** — What you're looking at. The distributable pattern.
- **Tree** — What grows from it. Your personal AI system.
- **Grove** — A community of trees. People growing together, sharing patterns.
- **Forest** — All of us. Everyone building their own Personal AI.

## We Are All Application Developers

Personal AI means you are building a custom system — your own processes, your own agents, your own domain knowledge, your own agentic workflows. This isn't about prompting better. It's about building a system that compounds your capability over time.

The seed teaches this through doing. You don't read about The Loop — you live it from your first session.

## Getting Started

See **[PLANTING.md](PLANTING.md)** for the step-by-step guide from zero to your first working session.

## Community

This seed was developed through the [Kwaai.ai](https://kwaai.ai) Personal AI community — a nonprofit R&D and policy lab dedicated to making Personal AI accessible to everyone.

## License

MIT
