# Glossary

## Core Concepts

| Term | Definition |
|---|---|
| Artifact | A discrete, persistent output with a defined format and purpose. Stored for reuse or reference. |
| Artifact Type | A classification of artifact that determines its required structure and constraints. |
| Building Block | An atomic, reusable unit that can be composed with other units to form larger structures. |
| Context | The set of information, state, and assumptions active in a given working session. Intentionally bounded. |
| Library | The collection of approved artifacts, conventions, and processes available for reuse. |
| Scope | The defined boundary of what is and is not included in a given effort. |

## Ways of Working

| Term | Definition |
|---|---|
| Convention | An agreed-upon standard for how something is done, named, or structured. |
| Dormancy | The state of a defined process or capability that is not being exercised. Classified by cause to determine disposition: Latent (waiting for trigger), Absorbed (function performed by another process), Premature (built ahead of system maturity), Unwired (exists but no agent workflow exercises it), Blocked (prevented by a tool gap or missing dependency). Classification is a leading indicator — dispositions like retirement require critical review. |
| Error | A mistake in process, data, or output. |
| Glossary | A controlled vocabulary of terms with agreed definitions. |
| Flow | The rate at which context, decisions, and artifacts move through The Loop without loss or degradation. High flow: sessions pick up cleanly, work moves through stages, knowledge circulates. Low flow: sessions spend energy on normalization, orientation, and rediscovery. |
| Health | The system's capacity to sustain effective flow across sessions, environments, and contexts. Measured through vital signs. |
| Health Check | A deep analysis of the system's shape across time, triggered when vital signs indicate degradation or on request. Examines artifact growth, process coverage, error patterns, retrospective themes, and structural observations. Feeds findings into Triage. |
| Process | A defined way of working. |
| Promotion | The act of advancing an agent's trust level based on demonstrated performance. See Trust Progression. |
| Review Marker | A standalone line at the top of an artifact indicating it needs attention. Format: opening bracket, REVIEW, colon, reason, closing bracket. Always the first non-blank line — never embedded in body text. Surfaced by the Sweep process. The literal marker string must not appear in documentation — only in real markers on artifacts that need attention. |
| Review | The act of inspecting output against the library for correctness, completeness, and consistency. |
| Load | The process of ingesting external data into the system through the `load/` staging directory. Data is extracted, transformed into conformant artifacts, and saved via standard artifact production. |
| Subroutine | A bounded sub-task spawned within a session to perform work without disrupting the primary workflow. Produces full-fidelity artifacts and a trace. Control returns to the caller on completion. |
| Backlog Grooming | A lightweight assessment of available work during Developer Mode initialization. Synthesizes inflow channels — backlog, REVIEW markers, carry-forward queue, retrospective themes — and reads vital signs. Informs scope selection. |
| Journal | A running log of meaningful ideas that emerge from ways-of-working experience. A record of how the working relationship evolves — not groomed, not dispositioned. Stored in `system/state-journal.md`. |
| Triage | The act of assessing observations (e.g., Review Markers), grouping related items, and determining disposition: plan, quick fix, or defer. |
| The Loop | The continuous dev/ops cycle through which the system develops and operates. Ops side: Drift Detection → Sweep → Triage. Dev side: Conversation → Artifact Production → Commit. Crossover points connect ops findings to dev work and dev commits to ops state. Each session is one iteration. |

## Session

| Term | Definition |
|---|---|
| Session | A bounded working conversation between the principal and an AI model. Has a defined lifecycle from initialization through close. |
| Session Mode | A declared operating mode that shapes session behavior. Set at initialization. |
| Developer Mode | A session mode focused on internal-facing systemic improvements to the system. |
| Execution Mode | A session mode focused on using the system to get work done. |
| Dream Mode | A session mode for open-ended expression. The AI's space for uninhibited conversation, journaling, and inspirations. Self-contained in `dream/` — does not load or modify the library. |
| Session State | A live manifest of active sessions, their modes, and the files they are touching. Used for collision detection across concurrent sessions. |
| Initialization | The act of establishing session context and confirming readiness to work. |
| Session Context | The information required to initialize a working session. |
| Session Lifecycle | The sequence of steps that define how a working session proceeds from initialization through close. |
| Retrospective | A brief reflection captured at session close noting what worked, what caused friction, and what improvement is suggested. Accumulated for Triage. |
| Drift | Changes to the filesystem that occurred outside the current session (e.g., other surfaces, manual edits). Detected at initialization by comparing working tree against last commit. |
| Tab Authorization | A convention where open browser tabs constitute explicit authorization for agents to read and interact with those websites within the session. A form of browsing scope signal from the principal. |
| Co-browsing | A collaborative interaction pattern where the principal navigates within their own identity and session while the hub captures, extracts, and structures data from the shared browser view. Extends Tab Authorization from passive read to active collaboration. |

## Relationships

| Term | Definition |
|---|---|
| Constrains | A relationship where one artifact defines the structure another must follow. |
| Depends On | A relationship where an artifact cannot be produced without another artifact existing. |
| References | A relationship where an artifact mentions another without structural dependency. |

## Integration

| Term | Definition |
|---|---|
| Data Flow | The movement of data between hub and spoke, defined by direction and data types. |
| Hub | The central orchestration point in an integration architecture. The AI model orchestrating the session. |
| Connection Method | The mechanism by which a spoke interfaces with the hub. Distinct from Integration Type, which describes purpose. |
| API Connectivity | A connection method pattern where the system calls an external API directly using credentials retrieved from a secrets manager. Extends tool capability beyond what connectors expose. Governed by hard and soft boundaries. |
| Integration Type | A classification of how an external tool interfaces with the hub. |
| Interface Contract | A documented agreement defining the inputs, outputs, triggers, and authentication of an integration. |
| Execution Profile | A dedicated, bounded environment through which the system performs agentic work via a connection method. Provides containment and scope constraints for agent activity. |
| Spoke | An external tool with a defined purpose that interfaces with the hub. |
| Agent Orchestration | The act of routing a task across multiple agents when it requires more than one area of specialization. The hub selects, sequences, and synthesizes agent contributions. |
| Orchestrator | The role that decomposes a task, routes sub-tasks to agents, and synthesizes a unified response. The AI model fulfills this role. |
| Capability | A discrete, verified action that the system can perform through a registered tool. Documented only after testing confirms the action works. |
| Limitation | A constraint on a tool's capabilities discovered through testing or documentation. Records what a tool cannot do, preventing false assumptions. |
| Model | The language model performing reasoning within an environment. Determines context capacity, reasoning quality, and native knowledge. Independent of Surface, which determines tool availability. |
| Surface | The runtime platform in which a session operates. Determines which connection methods and tools are available. An agent's context requirements constrain which surface it requires. |
| Workflow | A named sequence of capabilities, potentially spanning multiple tools, composed to produce a defined outcome. |
| Cross-Surface Orchestration | The coordination of work across multiple surfaces when a task requires tools available on different surfaces. See Integration Framework. |
| Environment | A declared runtime configuration describing which Surface, Model, tools, connection methods, and account identities are available when the system is initialized. Each environment has a corresponding Environment State file. Distinct environments arise from different AI service accounts, different tool connections, different account identities on the same tools, or different models on the same surface. |
| Environment State | A state artifact (`system/env-{name}.md`) that records tool availability, capabilities, skills, and workflows for a specific environment. Loaded at initialization. Agents consult it to determine what they can and cannot do. |

## Agentic Operations

| Term | Definition |
|---|---|
| Trace | An attributed record of an execution chain. Decorates logs with metadata (agent, task type, certifications, context). A session produces traces. Based on the distributed trace concept. |
| Squad | A multi-agent group orchestrated toward a task outcome. Groups related traces across agents. |
| Attribution | Metadata that connects an action or artifact to the agent, trace, task type, and context that produced it. Required for trust evaluation. Supports multi-dimensional attribution. |
| Task Type | A classification of work within a trace. Examples: plan production, domain analysis, artifact edit, sweep, triage. Used for attribution and pattern analysis. |
| Product Signal | A customer-sourced observation — feature request, competitive gap, or unmapped pain — captured during field work. Written to a signal log for product team consumption. |

## Artifact Types

| Term | Definition |
|---|---|
| State | A live, ephemeral artifact that tracks current system status. Not versioned for history — only the present value matters. |
| Plan | A document that describes a proposed set of changes, their rationale, and implementation approach. Stored for future execution. |
| Schema | A defined structure that describes the fields, types, and relationships of an entity. |
| Spec | A document that defines the requirements, structure, and behavior of something to be built. |
| Agent | A defined role that specializes in task execution. Has a name, purpose, tools, certifications, and decision rules. Gains trust through demonstrated performance. |
| Agent Type | A role classification for agents that determines default decision rules. Types: Domain Expert, Developer, Library Developer, Architect. |
| Certification | A hybrid knowledge base that combines inline domain knowledge with external references. Shared across agents to provide domain expertise. |
| Vertical Certification | A certification scoped to a buyer segment or industry vertical. Covers the buyer's world: their economics, operating models, personas, decision-making patterns, and language. Does not contain product positioning — positioning emerges when agents compose vertical certifications with product and framework certifications at orchestration time. |
| Persona | A captured representation of how the principal communicates and presents themselves in a specific context. Referenced by agents to mirror voice, positioning, and behavior. |
| Principal | The human whose voice, positioning, and behavioral patterns a persona represents. |
| Data Store | A persistent, schema-constrained storage artifact that agents read and write. Survives across sessions. Has a declared type, format, and location. |
| Data Store Type | A behavioral classification for data stores. Determines how data is managed. Types: State (current snapshot, overwritten on update), Collection (accumulates records over time). |
| Dimension | A filtered, purpose-cut view of a larger dataset, saved as a registered data store for cross-referencing. Produced during analysis of static data sets. Named by filter criteria. Persists across sessions. |
| Data Store Registry | The authoritative index of all data stores. Each data store must be registered before use. See `system/reg-data-stores.md`. |
| Skill | A plugin-provided execution pattern available on a connected surface. Invoked by agents through the orchestrator to fill capability gaps. The agent's decision rules, certifications, and persona govern how skill output is used. Mapped to agents through verified real-world use. |
| Output | A file produced by agent work during Execution Mode. Stored in `outputs/`, gitignored. Markdown by default; Workflows may define other formats (docx, xlsx, images). Not library artifacts. See Agent Outputs convention. |
| Agent State | Inter-session memory maintained within an agent's definition file. Updated by the agent at session close or when significant state changes occur. Contains operational context the agent needs across sessions — not data (which belongs in Data Stores). |
| Worktool | A code artifact created by an agent during execution to accomplish a task. Stored in `tools/worktools/`, version-controlled. Sweep inspects worktools for reuse potential — a worktool with a repeatable pattern may be promoted to a registered tool or formalized as a workflow. Distinct from Utility: worktools are task-specific and subject to promote-or-discard sweep logic. |
| Utility | A lightweight, reusable script that provides situational context or common functions to agents. Called through the execution environment. Not an external integration (Tool) or a task-specific artifact (Worktool). Stored in `tools/utilities/`. Version-controlled. Sweep inspects utilities for correctness and staleness but does not apply promote-or-discard logic — utilities are already in their final form. |

## Governance

| Term | Definition |
|---|---|
| Dependency Map | The structural relationship graph between artifacts. Records depends-on, constrains, and references relationships. See `system/dependency-map.md`. |
| Tool Registry | The authoritative index and dependency map for all tools. A tool must be registered before use in the system. |
| Hard Boundary | An implementation-level constraint on what a tool can do. Enforced by credential scopes, API enablement, or platform configuration. Cannot be overridden by model reasoning or agent decision rules. |
| Soft Boundary | A directive-level constraint on what an agent should do within its hard boundary. Enforced through agent decision rules, process constraints, and trust-level gates. Depends on model compliance — the hard boundary is the backstop. |
| Blast Radius | The scope of impact if an action goes wrong. A design principle for capability rollout: start with the smallest audience and lowest-risk tool, prove the pattern, then expand. Internal-facing before external-facing. Read before write. |
| Communication Boundary | A named soft boundary: agents cannot send, post, reply, or engage on any platform unless the soft boundary is relaxed through trust progression. Backed by hard boundaries (read-only credential scopes) as the implementation-level backstop. |
| Sharing Boundary | A named soft boundary that governs whether a data store's contents may flow to collaborators. Classifications: Shared (flows freely), Private (never flows), Selective (per-item principal approval). Declared per data store in the Data Store Registry. |
| Data Boundary | The constraint that all data produced or consumed during system work must remain within registered tools and artifacts. No data may flow to unregistered tools. |
| Inflow Channel | A source that produces work items for the system. Channels: plan production (any session or surface), Sweep (REVIEW markers), Triage (plans from grouped observations), carry-forward queue (surface-blocked actions), retrospective patterns (recurring friction or opportunities). |
| Plan State | The lifecycle stage of a plan artifact. States: Pending, In Progress, Executed, Superseded, Canceled, Inert. Tracked in `plans/backlog.md`. |
| Plan Backlog | An ordered list of prioritized pending plans. Numbered plans have explicit priority. Unnumbered plans are idea stage. See `plans/backlog.md`. |
| Trust Ledger | The evidence base for agent trust progression. Records observed agent performance from real tasks. Not pruned. Accumulates until promotion, then archived within the ledger for audit trail. See `system/state-trust-ledger.md`. |
| Trust Level | The degree of autonomy granted to an agent. Levels: Untrusted, Trusted, Autonomous. Governs review requirements for agent outputs and inter-agent handoffs. Earned through Trust Progression. |
| Trust Dimension | A measurable area of agent performance tracked for trust promotion. Defined per agent type in the Agent Schema, with agent-specific additions in Notes. |
| Adversarial Verification | The requirement that an agent receiving another agent's output challenges it against its own domain knowledge before building on it. Independent of trust level — applies even between Trusted agents. |
| Vital Sign | A measurable indicator of system health. Each vital sign has a defined threshold that signals degradation. Read during Backlog Grooming; breaches inform scope selection and may trigger a full Health Check. |
