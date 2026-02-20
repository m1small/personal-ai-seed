# Environment State Schema

## Purpose

Defines the required fields for any environment state artifact. All environment state files (`system/env-*.md`) must conform to this schema. Extends the Building Block Schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | Environment name. Matches the filename stem (e.g., `claude-code-ms`). (Building Block base field.) |
| 2 | Purpose | text | yes | What this environment is for. (Building Block base field.) |
| 3 | Surface | text | yes | The runtime platform this environment operates on (e.g., Claude Code, LM Studio, Cursor). Determines connection methods and tool availability. |
| 4 | Model | table | no | The language model backing this environment. Includes model name, context window, and relevant constraints. Omit when the surface fixes the model and the model is implicit (e.g., hosted API surfaces where the provider controls model selection). |
| 5 | Tools | table | yes | Each Tool Registry entry mapped to reachability status, connection method, and account identity. Status indicates reachability, not verification. See Tool Status Values. |
| 6 | Capabilities | table | yes | Verified actions available in this environment. Each entry references a capability from a tool contract by name. |
| 7 | Skills | table | no | Plugin skills available in this environment. Each entry names the skill and the agent(s) it is mapped to. Omit if no skills are available. |
| 8 | Workflows | table | yes | Per-agent workflow status. Each entry names the agent, workflow, availability (Available, Partially Blocked, Unavailable), and gap description if blocked. |
| 9 | Limitations | table | no | Environment-specific constraints beyond individual tool limitations. |
| 10 | Dependencies | list | no | Other artifacts this environment state relies on. (Building Block base field.) |
| 11 | Notes | text | no | Open questions, context, or operational guidance. (Building Block base field.) |

## Tool Status Values

| Status | Meaning |
|---|---|
| Connected | Tool is reachable from this environment via its connection method. |
| Not Connected | Tool is not reachable from this environment. |

Status indicates reachability, not verification. Verification status lives in tool contracts (Capabilities sections with verified dates).

## Identity Convention

The Identity column in the Tools table records the account or credential that distinguishes this environment's connection to a tool. When the same tool connects to different accounts in different environments, the identity is what differentiates them.

- For credential-backed tools, name the credential source and item.
- For CLI-authenticated tools, name the account.
- Use `—` when identity is not applicable (e.g., local-only tools).

## Model Table Columns

When the Model field is present, use this structure:

| Column | Description |
|---|---|
| Name | Model identifier (e.g., Claude Opus, GPT-4, Llama 3). |
| Context Window | Token capacity. Determines how much library can be loaded per session. |
| Notes | Relevant constraints — instruction following fidelity, tool use support, training cut-off. |

## Maintenance

Environment state files are declared, not probed. Accuracy is maintained through two feedback loops:

- **Developer Mode verification:** A Developer Mode session periodically tests tool connectivity and updates the environment file. This is a task type, not a dedicated agent.
- **Execution agent feedback:** When an agent encounters a capability gap or limitation during real work, it produces a plan recommending environment improvements. The plan enters the backlog for Developer Mode execution.

## Model Portability

This schema is model-agnostic by design. Surface and Model are independent axes — Surface determines tool availability, Model determines reasoning capability. The remaining fields (Tools, Capabilities, Skills, Workflows, Limitations) describe what is available in a runtime environment without assuming either. When the system operates on a different surface or model, the schema holds; only the values change.
