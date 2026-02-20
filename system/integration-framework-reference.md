# Integration Framework — Reference

Detailed patterns, procedures, and governance for integration work. Loaded on demand when doing tool integration, cross-surface orchestration, or boundary framework work. The core framework is in `system/integration-framework.md`.

## Connector Subtypes

Connectors vary in how they expose tools to the session. The subtype is recorded in the tool registry and interface contract as `Connector (Subtype)`.

| Subtype | Description |
|---|---|
| Platform | Services managed by the AI provider, connected through the platform UI. Tools are injected directly into the conversation context. |
| MCP | Third-party services exposed through the MCP registry. Tools appear in registry search results with schemas. |
| Browser Extension | Services exposed through a browser extension. Tools available when the extension is active. |

Connector subtypes are platform-specific. The subtypes above document common connector mechanisms. Other AI model backends may expose their own connector patterns — these would be documented as additional subtypes when the system operates on those platforms.

## API Connectivity

A connection method pattern where the system calls an external API directly using credentials retrieved at runtime. Complements — does not replace — existing connection methods. A tool may have both a Connector (for platform-managed access) and API Connectivity (for operations the connector doesn't expose). The tool contract documents which capabilities are available through which method.

### Pattern

1. **Credential retrieval** — Agent identifies credential need from tool contract. Orchestrator retrieves the credential using the documented retrieval mechanism.
2. **Scope validation** — Before making an API call, verify the credential's scopes against the tool contract's declared hard boundary. If the requested action exceeds the hard boundary, stop and escalate to the principal.
3. **API call** — Execute the API call through the execution environment (shell command, script, or direct HTTP). The tool contract documents the API endpoints, authentication method, and expected response format.
4. **Result handling** — API response flows back to the hub for agent processing. Data boundary rules apply — results stay within registered artifacts.
5. **Credential hygiene** — Credentials are injected as environment variables for the session. Never written to disk, committed, or persisted. On session close, environment variables are discarded.

### Relationship to Other Methods

API Connectivity fills the gap between what connectors expose and what the underlying API supports. The capability ceiling for a connector is set by the platform provider. The capability ceiling for API Connectivity is set by the system through provisioned credential scopes.

When both methods serve the same capability, the connector is preferred (simpler, platform-managed auth). API Connectivity is used for operations the connector doesn't surface.

### Prerequisites

- Credential retrieval mechanism operational (e.g., Bitwarden CLI, secrets directory).
- Credential provisioned with declared scopes.
- Tool contract updated with API connection method, capabilities, and boundary declarations.

## Surface Availability

Which surfaces exist and what connection methods they support is declared in the Environment State file for each environment. The framework defines the concept; the environment declares the specifics.

When a task requires tools across surfaces, use the Cross-Surface Orchestration patterns below to coordinate the work.

### Surface Resolution

An agent's required surface is determined by its Initialization Context:

1. Collect all capabilities referenced in the agent's Initialization Context.
2. Map each capability to its tool's connection method (from the tool registry).
3. Map each connection method to the surface(s) that support it (from the environment state file).
4. The agent requires a surface that supports *all* referenced connection methods. If no single surface covers all methods, the agent's initialization must be split across surfaces or the gap documented.

## Cross-Surface Orchestration

When an agent's workflow requires tools on more than one surface, the work must be split across sessions. The orchestrator manages this through one of three patterns, selected based on task characteristics.

### Patterns

| Pattern | When to Use | How It Works |
|---|---|---|
| Sequential Handoff | Task has clear phases — gather on one surface, act on another. Most common. | Complete work on Surface A, capture output as an artifact or conversation summary, switch to Surface B, continue with carried context. |
| Parallel Sessions | Two independent workstreams that share artifacts but don't block each other. | Two sessions active concurrently (one per surface). Session state provides collision detection. Shared artifacts are the coordination mechanism. |
| Artifact Bridge | Context must transfer between surfaces with fidelity — not just a summary, but structured data. | A defined artifact (e.g., briefing, task handoff, plan) is produced on Surface A and consumed on Surface B. The artifact format is the contract between surfaces. |

### Selection Criteria

1. **Does the task have sequential phases?** (e.g., research then implement) → Sequential Handoff.
2. **Can both surfaces work independently on different sub-tasks?** → Parallel Sessions.
3. **Does the receiving surface need structured context, not just a summary?** → Artifact Bridge.

Patterns may combine. A task might use Sequential Handoff at the macro level with an Artifact Bridge carrying context between phases.

### Orchestrator Responsibilities

- **Declare the pattern** when initiating cross-surface work. Name the pattern in conversation so the principal knows what to expect.
- **Capture carry-forward context** at surface boundaries. What was learned, decided, or produced — and what the next surface needs to continue.
- **Manage session state** across surfaces. When using Parallel Sessions, both sessions register in session state and honor Collision Check.
- **Commit at boundaries.** Work produced on a surface that supports git must be committed before handoff. If the originating surface lacks git, the first action on the receiving session is to commit the carried-forward artifacts.

### Carry-Forward Queue

When a session cannot complete an action due to surface limitations, it records the action in `system/state-carry-forward.md`. This covers the unplanned case — a session discovers mid-work that it needs the other surface. The carry-forward queue bridges the gap.

**Write:** Any session appends entries on close (Session Lifecycle step 7).
**Read and resolve:** Drift Detection checks the queue on initialization. If the current surface can resolve an entry, it executes the action and removes the entry.

This complements the three orchestration patterns (Sequential Handoff, Parallel Sessions, Artifact Bridge) which handle planned cross-surface coordination. The carry-forward queue handles discovered surface gaps.

## Capability and Workflow Documentation

Tool contracts document three levels of operational detail:

| Section | What It Contains | When It's Added |
|---|---|---|
| Capabilities | Verified actions with tool name, parameters, and tested status. | During connector testing or first verified use. |
| Limitations | Actions that are documented or expected but not available. | When a capability gap is discovered during testing. |
| Workflows | Named sequences of capabilities that produce an outcome. | When a repeatable pattern emerges from real work. |

Capabilities are the source of truth for what the system can do with a tool.

Verification status lives in the tool contract, not in environment state files. Environment state declares reachability; tool contracts declare readiness.

Workflows reference capabilities by name. If a workflow requires an action that is a known Limitation, the workflow must document the handoff point (e.g., "principal handles manually").

## Hub-Spoke Mapping Rules

| Role | Criteria |
|---|---|
| Hub | The AI model orchestrating the session. Orchestrates work, produces artifacts, routes data between spokes. |
| Spoke | Any tool with a single defined purpose that interfaces with the hub. |
| Spoke-to-Spoke Exception | Allowed only when: (1) The connection is a native feature of both tools (e.g., VS Code + GitHub), AND (2) The flow is documented with justification. |

## Data Flow Notation

The interface contract table is the required documentation for each integration. Diagrams are optional supplementary material. If a diagram tool is used, it must be registered in the tool registry.

## Execution Profiles

An Execution Profile is a dedicated, bounded environment through which the system performs agentic work via a connection method. Profiles provide containment — when a profile is active, the system operates within that profile's scope and identity.

| Field | Required | Description |
|---|---|---|
| Profile Name | yes | A human-readable name for the profile. |
| Identity | yes | The account or credential that owns the profile. |
| Connection Method | yes | The connection method this profile is associated with. |
| Scope Constraints | yes | What the profile may and may not access when active. |

### Rules

- Agentic browsing must occur within a registered Execution Profile.
- If an agent detects it is not operating within its designated profile, it must warn and not proceed with agentic browsing actions.
- The profile identity is for containment only. It does not grant the profile's account any communication or sending privileges.

## Boundary Framework

Every tool capability operates within two independent constraint layers. Both layers are required — hard boundaries alone don't guide judgment, soft boundaries alone depend on perfect model compliance.

### Hard Boundaries

Implementation-level constraints on what a tool can do. Enforced by credential scopes, API enablement, or platform configuration. Cannot be overridden by model reasoning or agent decision rules.

**Sources:** OAuth scopes, API key permissions, platform configuration, network access controls. Provisioned by the principal. Changed only through deliberate credential re-provisioning.

### Soft Boundaries

Directive-level constraints on what an agent should do within its hard boundary. Enforced through agent decision rules, process constraints (e.g., Communication Boundary), and trust-level gates. Depends on model compliance — the hard boundary is the backstop.

**Sources:** Agent decision rules, process constraints, trust-level gates, session-specific scope declarations. Evolve with trust progression — as an agent earns trust, soft boundaries may relax while hard boundaries remain unchanged.

### Independence Principle

Trust progression relaxes soft boundaries. It never changes hard boundaries. Expanding hard boundaries is always a deliberate principal action — provisioning broader credential scopes. This separation ensures trust progression never accidentally grants capability.

### Blast Radius Principle

When expanding capability through API Connectivity, start with the lowest-blast-radius tool. Internal-facing before external-facing. Read scopes before write scopes. Prove the boundary framework works on low-risk tools before applying it to high-risk ones.

### Named Soft Boundaries

Named soft boundaries are system-wide behavioral constraints that apply across all agents. They are documented here as the authoritative definition. Agent decision rules reference them by name.

**Communication Boundary:** Agents cannot send, post, reply, or engage on any platform. This is the default soft boundary for all Untrusted agents. Trust progression path: Trusted agents may draft for the principal's review. Autonomous agents may send with the principal's pre-authorization. Hard boundary backstop: read-only credential scopes prevent sends even if the soft boundary is violated.

### Auditability

Tool contracts declare both layers. Hard boundaries are auditable via credential scope inspection. Soft boundaries are auditable via agent decision rules and process definitions in the library.

## Notes

- As new integration patterns emerge, this framework will evolve through iterative changes tracked in git.
- This framework does not prescribe how to integrate (that is tool-specific), only how to document integrations.
- **Model portability:** The hub-and-spoke architecture, integration types, interface contracts, and capability documentation are model-agnostic. Connection methods (CLI, MCP, Native) are broadly portable. Connector subtypes and Surface definitions are platform-specific — they document the current AI model's integration mechanisms and would be extended when the system operates on a different model backend. The Environment State file is the bridge: it records what's available on any given platform without embedding platform assumptions into the framework itself.
