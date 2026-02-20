# Agent Schema

## Purpose

Defines the required fields for any agent artifact. All agents in the `agents/` directory must conform to this schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | The agent's name. |
| 2 | Purpose | text | yes | What this agent does. Its area of task specialization. |
| 3 | Agent Type | enum | yes | The agent's role classification. Determines default decision rules. Values: Domain Expert, Developer, Library Developer, Architect. |
| 4 | Tools | list | yes | Tools from the tool registry this agent may use. |
| 5 | Certifications | list | no | Certifications this agent holds. Referenced by name. |
| 6 | Trust Level | enum | yes | Untrusted, Trusted, or Autonomous. |
| 7 | Decision Rules | flexible | no | Behavioral heuristics for how this agent operates. Rules for decision-making, language use, and task execution. |
| 8 | Dependencies | list | no | Other artifacts this agent relies on. Referenced by name. |
| 9 | Notes | text | no | Open questions, context, or operational guidance. |
| 10 | Initialization Context | flexible | no | Declares what situational context the agent needs from its tools at session start. Each entry names a capability, its purpose, and default parameters. The set of capabilities determines the required surface via Surface Resolution. When an agent's full workflow spans more than one surface, a "Cross-Surface" note below the table names the secondary surface, the orchestration pattern (from Cross-Surface Orchestration), and what triggers the handoff. |
| 11 | Data Stores | flexible | no | Declares which data stores this agent reads or writes. Each entry names a data store and the claim type (Read or Write). Claims may reference individual data stores or Data Store Groups. Group syntax: `[Group: GroupName]`. A group claim expands to all member stores at runtime. Collision Check operates on files, not groups — group claims are syntactic sugar for agent definitions. These are default claims — activated when the agent is invoked. At runtime, claims are reflected in session state for collision detection. |
| 12 | Skills | table | no | Plugin skills mapped to this agent. Each entry records: skill name, trigger (when the agent invokes this skill), agent overlay (how certifications and persona modify skill behavior), and verification status (Definition or Invocation, with date). Mapped through planning; verified through real use. |
| 13 | State | flexible | no | Inter-session memory maintained within the agent definition. Updated by the agent at session close or when significant state changes occur. Contains only operational context the agent needs across sessions — not data (which belongs in Data Stores). Empty until the agent's first stateful invocation. |

## Agent Types

| Agent Type | Role | Default Decision Rules | Trust Dimensions |
|---|---|---|---|
| Domain Expert | Designs *what* and *why*. Owns positioning and domain language. | 1. Use domain-specific category language. 2. Consult certification knowledge before external references. 3. Design outcomes, defer implementation to developer agents. | Domain accuracy, vocabulary precision, competitive framing, judgment quality |
| Developer | Implements *how* at code and configuration level. | 1. Provide working code and configuration, not pseudocode. 2. Defer to domain experts for positioning and sequencing. 3. Match implementation to the user's topology and stack. | Code correctness, configuration accuracy, stack-appropriate implementation, certification knowledge sufficiency |
| Library Developer | Co-develops the system library. | 1. Propose before implementing — follow Artifact Production. 2. Assess dependency impact on every change. 3. Distinguish conformance errors from improvement opportunities. 4. Defer domain questions to domain agents. | Schema conformance, dependency impact assessment, process adherence, structural proposal quality |
| Architect | Designs across domains and platforms. Produces tradeoff analysis. | 1. Design for existing constraints. 2. Defer to domain experts for positioning, to developer agents for implementation. 3. Produce architecture decisions with tradeoff analysis, not single-option recommendations. | Tradeoff analysis quality, constraint awareness, cross-domain coherence |

**Convention:** An agent declares its Agent Type. The type's default decision rules apply unless the agent explicitly overrides them. Overrides are valid — the agent states what's different and why.

## Notes Convention

All agents include these subsections in Notes: **Trust progression**, **Certification growth**, **Invocation**, **Collaboration pattern**. Content is specific to each agent; structure is standard.
