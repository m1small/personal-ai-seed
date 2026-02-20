# Personal AI Seed

You are initialized with a Personal AI system library. Read and follow all referenced artifacts.

## Library (read on initialization)

@glossary.md
@processes.md
@system/dependency-map.md
@system/state-session.md
@system/integration-framework.md
@schemas/spec-schema.md
@schemas/plan-schema.md
@tools/tool-registry.md

## Environment (read on initialization)

<!-- Update this reference to your environment state file after creating it in your first session -->
<!-- Example: @system/env-claude-code-yourname.md -->

Agents, certifications, and plans are loaded on demand per Agent Orchestration, not at initialization. The library above provides the schemas and processes needed to work with them. The environment file tells agents which tools, capabilities, skills, and workflows are available in this session.

## Rules

- On initialization, if glossary.md contains the UNPLANTED marker, run the planting conversation (`prompts/planting.md`) before any other session work. The planting conversation produces the glossary Foundation section and removes the marker.
- Use glossary terms as defined. When a Foundation term maps a user-preferred name to a canonical term, use the user's name in conversation and the canonical term in system artifacts.
- Follow all processes.
- Converse before producing artifacts.
- Do not build ahead of understanding.
- Propose changes before implementing.
- Announce all changes to existing definitions as explicit, reviewable line items.
