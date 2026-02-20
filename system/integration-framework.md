# Integration Framework

## Purpose

Defines how the system integrates with external tools using a hub-and-spoke architecture. Establishes patterns for documenting data flows, interface contracts, and integration types.

## Principles

- **Hub Centralization** — The AI model is the hub. All orchestration, reasoning, and artifact production flows through it.
- **Spoke Specialization** — Each external tool has a defined purpose and interface. Spokes execute within their domain.
- **Minimal Coupling** — Spoke-to-spoke connections are avoided unless explicitly justified and documented.
- **Explicit Contracts** — Every integration has a documented interface defining inputs, outputs, triggers, and authentication.

## Integration Types

| Type | Purpose | Examples |
|---|---|---|
| Data Source | Provides information to the hub | Google Drive, Notion, Slack |
| Execution Environment | Runs code or commands | Claude Code, Cursor, terminal |
| Output Destination | Receives artifacts or data | Local repo, Google Workspace, GitHub |
| Rendering Tool | Transforms data into visual formats | Mermaid, Gamma |
| Development Tool | Supports code creation/management | VS Code, GitHub |

## Connection Methods

Connection Method describes *how* a spoke interfaces with the hub. This is orthogonal to Integration Type, which describes *why* (purpose).

| Method | Description |
|---|---|
| CLI | Commands executed through a shell. |
| MCP | Tools exposed via a Model Context Protocol server. |
| Native | Built-in to the execution environment (e.g., filesystem access through Claude Code). |
| Connector | OAuth-linked services exposed through the AI platform. Platform-specific — subtypes in reference file. |
| API | Direct API calls using credentials retrieved at runtime. Extends tool capability beyond connector surfaces. Governed by hard and soft boundaries. |
| Manual | Requires human interaction to operate. |

A tool may support more than one connection method. The interface contract documents the method(s) in use.

Connector subtypes, API Connectivity patterns, Surface Availability, and Cross-Surface Orchestration are documented in `system/integration-framework-reference.md`.

## Interface Contract Schema

Every integration must document:

| Field | Required | Description |
|---|---|---|
| Tool Name | yes | Name and version if applicable. |
| Integration Type | yes | From the integration types table above. |
| Connection Method | yes | From the connection methods table above. |
| Data Flow Direction | yes | hub → spoke, spoke → hub, or bidirectional. |
| Data Types | yes | What formats are exchanged (e.g., markdown, JSON, API responses). |
| Authentication | no | How access is managed (OAuth, API key, local filesystem, none). |
| Trigger Conditions | yes | What initiates the flow (manual, event-driven, scheduled). |
| Hard Boundary | if API method | Credential scopes provisioned. What is physically possible. Declared per the Credential Storage Spec boundary declaration convention. |
| Soft Boundary | if API method | Agent behavioral constraints within the hard boundary. References named soft boundaries (e.g., Communication Boundary) and agent-specific decision rules. |

Capability and Workflow Documentation, Hub-Spoke Mapping Rules, Data Flow Notation, Execution Profiles, and the Boundary Framework (Hard/Soft Boundaries, Independence Principle, Blast Radius Principle, Named Soft Boundaries including Communication Boundary) are documented in `system/integration-framework-reference.md`.

## Governance

- All tools used in the system must be registered in the tool registry (`tools/tool-registry.md`). Undocumented tool usage is not permitted.
- Atomic files must contain only content within their own scope. Dependencies on other tools must not be embedded — they are declared in the tool registry.
- **Data Boundary:** All data produced or consumed during system work must remain within registered tools and artifacts. No data may be stored in, sent to, or retrieved from tools not registered in the tool registry. This applies to all agents and sessions.

## Tool Registry

Individual interface contracts are stored in the `tools/` directory. Each file documents one spoke following the Interface Contract Schema above. The authoritative index and dependency map is `tools/tool-registry.md`.

## Notes

See `system/integration-framework-reference.md` for model portability notes and framework evolution guidance.
