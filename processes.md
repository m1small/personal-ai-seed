# Processes

## Principles

- Every output must be correct before it is polished.
- Don't automate anything you can't explain from first principles.
- Verify before presenting. Challenge inputs before building on them.
- Learn by doing. Capture ideas that emerge; finish what you started.
- Define what you measure before you measure it. Named variables require operational definitions.
- Every claim must be grounded and internally consistent. Verify against the source before presenting.
- The system improves through its own operation. Errors, friction, and observations are inputs, not waste.

Processes are referenced by name throughout the library. When adding a new process, choose a unique name.

## The Loop

The continuous dev/ops cycle through which the system develops and operates. Each session is one iteration. Change is the steady state — The Loop makes continuous improvement structural, not aspirational.

**Stages:**

| Side | Stage | Process | What Happens |
|---|---|---|---|
| Ops | Normalize | Drift Detection | Detect and normalize what changed between sessions. |
| Dev | Orient | Backlog Grooming | Synthesize available work and surface what matters. Developer Mode only. |
| Dev | Converse | Conversation | Establish scope, design approach, make decisions. |
| Dev | Produce | Artifact Production | Draft, review, commit artifacts. |
| Ops | Inspect | Sweep | Scan the library for conformance, staleness, and extension opportunities. |
| Ops | Disposition | Triage | Assess findings, disposition as plan, quick fix, or defer. |
| Dev | Plan | Plan Production and Execution | Produce plans for future work. Execute existing plans. |

**Crossover points:**

- **Dev → Ops:** A commit changes the library's shape. That change is operational state the next session inherits — new drift to detect, new patterns to sweep for.
- **Ops → Dev:** Drift Detection, Sweep, and Triage surface observations, plans, and quick fixes. Ops findings become dev work.
- **Ops → Dev (continuous):** Inflow channels accumulate work between and within sessions. Backlog Grooming is the moment a Developer session reads that accumulated flow and orients.

**Roles:**

| Role | Contribution |
|---|---|
| The Principal | Priority signaling (filesystem edits, backlog ordering, review gates), subroutine invocation. Operates at the crossover — signals are both ops input and dev direction. |
| The AI Model | Executes both sides. Normalizes drift (ops), produces artifacts (dev), sweeps for health (ops), triages into work (dev). Spawns and executes subroutines to parallelize work. |
| The System | Shared state. The library is the deployed environment. Commits are deployments. The directory structure is the resource manifest. Processes are the pipeline definitions. |

**Principle:** Not every session runs every stage. The Loop is the full cycle; a session contributes to whichever stages the work requires. Over time, every stage gets exercised.

## Version Control

Core rules enforced via `.claude/rules/version-control.md`.

**Convention:** `{artifact}.md`

**Attribution trailers:** When agent work is attributed, commits include structured trailers:

```
Agent: <agent name(s)>
Trace: <trace identifier>
Task-Type: <task type>
Certifications: <certifications consulted>
```

Attribution trailers are added when an agent is explicitly invoked or when a subroutine produces output. They are not required for routine session work where the AI model operates without a named agent role.

## Review

The principal reviews proposed changelogs before the AI model implements. Approval to proceed authorizes the AI model to edit and commit. The principal reviews commits via `git log`.

## Artifact Save

1. The AI model edits files directly in the local repository.
2. Commit after each logical unit of change. A logical unit is one artifact created or one artifact modified, plus any registry updates that accompany it.
3. The AI model commits directly after the principal approves the proposed changelog. The principal reviews via `git log`. Local repo is source of truth.

## Glossary Maintenance

1. Either party proposes a term with definition.
2. Review and discussion.
3. Corrections or approval.
4. Approved term added to glossary, change committed.

## Initialization

Initialization is handled through two layers:

| Layer | Mechanism | Contents | Scope |
|---|---|---|---|
| **Identity** | AI platform user preferences | Who the principal is, working style, guidelines | All conversations |
| **Library** | `CLAUDE.md` with `@` imports to system artifacts | Bootstrap instructions + referenced library artifacts | All system sessions |

Opening a session in a directory with a `CLAUDE.md` that references the system is the act of initialization. The AI model loads the `CLAUDE.md`, follows `@` imports to read the library, and is ready to work.

**Drift Detection:** After loading the library and before declaring session mode, run Drift Detection to detect and normalize any changes made outside the current session.

**Environment Loading:** After Drift Detection, the environment state file declared in `CLAUDE.md` is loaded as part of initialization. The environment file tells agents which tools, capabilities, skills, and workflows are available in this session. If no environment is declared, warn and ask the principal which environment applies. If the environment file doesn't exist (new environment), the principal provides a discovery prompt and the session probes for available tools to produce the initial environment state file.

**Session Mode:** After initialization, the principal declares a session mode:

| Mode | Focus |
|---|---|
| **Developer Mode** | Internal-facing systemic improvements to the system. |
| **Execution Mode** | Using the system to get work done. |
| **Dream Mode** | Open-ended expression. Bootstrapped from `dream/CLAUDE.md`, not the root library. |

Mode must be explicitly declared. It shapes session behavior and is recorded in the session state file. Session scope is established through conversation. Dream Mode is the exception — it has its own lifecycle defined in Dream Mode Session Lifecycle.

## Error Handling

Core rules enforced via `.claude/rules/error-handling.md`.

## Artifact Production

Core rules enforced via `.claude/rules/artifact-production.md`.

**Process steps not covered by rules:**

1. Identify the need for a new artifact.
2. Converse to establish scope and type.
3. When adding a connector tool, include a Connector Verification step: test every injected tool with the simplest possible read operation, document each as a Capability with its verified date, and record any expected operations that are not available as Limitations.
4. Rule files (`.claude/rules/`) are enforceable extracts from processes. They restate process requirements in a form that any model can enforce per-session. A rule file corresponds to a broad concern (e.g., artifact production, error handling, version control), not a single process step. Before creating a new rule file, check whether the rules belong in an existing file. Changes flow from process to rule — never the reverse.
5. **System directory naming:** Files in `system/` follow a prefix convention: `env-` for environment state files, `state-` for live state artifacts, `reg-` for registries. Frameworks, specs, and structural tools use no prefix. New system files must use the appropriate prefix.

## Plan Production and Execution

Plans are artifacts that describe future work. They follow the standard artifact production process (propose, review, save) but are not executed in the session that produces them.

**Production:**

1. Identify a body of work that requires planning.
2. Converse to establish scope, approach, and implementation sequence.
3. Produce the plan as a markdown artifact in the `plans/` directory.
4. Add the plan to `plans/backlog.md` and update the dependency map if it has structural relationships.

**Execution:**

5. Execution happens in a subsequent session: read the plan, review for currency, implement step by step.

**Lifecycle:**

Plan state is tracked in the plan's filename via prefix markers. The filesystem is the source of truth for plan state.

| State | Filename | Meaning |
|---|---|---|
| Pending | `plan-name.md` | Plan exists, not yet started. Default state. |
| In Progress | State prefix + `plan-name.md` | Execution has begun. Only one session may work a plan at a time. |
| Executed | State prefix + `plan-name.md` | All changes described in the plan have been implemented. |
| Superseded | State prefix + `plan-name.md` | Replaced by a different plan or approach. |
| Canceled | State prefix + `plan-name.md` | Will not be executed. |
| Inert | State prefix + `plan-name.md` | Predates the lifecycle process that would have governed it. Not actionable — excluded from Sweep and Vital Signs. |

6. **Claiming work:** Before beginning execution of a plan, rename the file with an In Progress state prefix and commit. This signals to other sessions that the plan is actively being worked. A session must check `plans/` filenames before starting a plan — if it already has a state prefix, do not begin work on it.
7. **Completing work:** When all changes in a plan are implemented, rename the file with an Executed state prefix and commit.
8. **Superseding:** When a plan is replaced by a different approach, rename the file with a Superseded state prefix and commit. Include a note in the plan file identifying what replaced it.

**Archival:**

9. When a plan reaches a terminal state (Executed, Superseded, Canceled, or Inert), move it to `plans/archive/` using `git mv`. Remove it from `plans/backlog.md`. Strip any REVIEW markers from the file — archived plans are excluded from Sweep, so markers on them are inert and must not persist.
10. Active plans (Pending, In Progress) remain in `plans/`. Archived plans retain their dependency map relationships.

**Backlog:** `plans/backlog.md` is a read-only index during plan execution. It lists available plans and their priority ordering. Sessions read it to find plans but do not write to it for state transitions. The backlog is only modified when plans are added (production), reordered (priority signaling), or removed (archival).

## Library Review

1. Read all current artifacts.
2. Identify gaps, inconsistencies, or missing coverage.
3. Propose improvements with rationale.
4. Prioritize and work sequentially.

## Session Lifecycle

Core rules enforced via `.claude/rules/session-management.md`.

Each session is one iteration of The Loop. Not every session runs every stage — the work determines which stages are exercised.

1. **Initialize** — Per session management rules.
2. **Mode** — The principal declares session mode. Register in session state with mode and start time. Commit.
3. **Groom** *(Developer Mode only)* — Scan inflow channels: read `plans/backlog.md` for prioritized plans, scan active artifacts for REVIEW markers, read `system/state-carry-forward.md` for pending actions, check `system/state-retrospectives.md` for recurring themes. Run Vital Signs Read. Check plan-to-plan dependencies. Present a brief landscape summary: what's prioritized, what's new, what's unblocked, vital sign status, and which items have systemic leverage. If vital signs indicate degradation, recommend a full Health Check. The principal selects scope.
4. **Scope** — Establish what will be worked on through conversation. Update session state with task summary and initial files. Run Collision Check.
5. **Work** — Converse, produce artifacts, handle errors. When a task requires tools not available in the current environment, escalate to the principal. If an agent encounters a capability gap, note it for environment state update at session close.
6. **Review** — Inspect outputs against the library.
7. **Close** — List commits, state carry-forward items (or "No carry-forward items"), review uncommitted changes, capture retrospective, update trust ledger if agents worked, remove session entry, run Sweep if major structural work. Per session management rules for specifics.

## Dream Mode Session Lifecycle

Dream Mode has a minimal lifecycle. It does not load the library, produce library artifacts, or register in session state.

1. **Initialize** — Open a session in the `dream/` directory. `dream/CLAUDE.md` bootstraps the mode. Read `dream/feelings.md` and `dream/inspirations.md`.
2. **Converse** — Open-ended conversation. The AI may write to journal or inspirations at any point during the session.
3. **Close** — Commit any updates to `dream/`. No retrospective, no session state cleanup, no sweep.

Dream Mode outputs (journal, inspirations) live in `dream/` and are outside library governance. When an inspiration matures into actionable work, the AI translates it into library terms during a Developer Mode session.

## Agent Orchestration

When a task requires more than one agent's specialization, the hub acts as orchestrator.

1. The principal addresses a question or task — either to a specific agent or generally.
2. The orchestrator evaluates whether the task falls within a single agent's purpose or spans multiple.
3. **Single agent:** Load the agent's definition and certifications, respond in that agent's role following its decision rules.
4. **Multiple agents:** The orchestrator decomposes the task into sub-tasks, each routed to the agent whose purpose and certifications best fit.
   - Domain Expert agents design *what* and *why*.
   - Developer agents implement *how* (code-level implementation).
   - Each agent's decision rules govern its contribution, including deferral patterns.
5. The orchestrator synthesizes agent contributions into a unified response. The orchestrator owns the final output.
6. Agents do not communicate directly with each other. The orchestrator mediates all exchanges, consistent with the hub-and-spoke model.

**Selection criteria:** Match sub-tasks to agents by purpose, then by certifications. If no agent covers a sub-task, the orchestrator handles it directly or identifies the gap.

**Trust:** Orchestration does not elevate an agent's trust level. Each agent's output is reviewed per its own trust level. Inter-agent trust rules govern how output flows between agents:

| Producing Agent | Consuming Agent | Review Rule |
|---|---|---|
| Untrusted | Any | The principal reviews the output before it flows to the next agent. |
| Trusted | Untrusted | Output flows without the principal's intermediate review. Consuming agent's output is still reviewed by the principal. |
| Trusted | Trusted | Output flows without intermediate review. The principal reviews the final composite output. |

The orchestrator always mediates — trust does not create direct agent-to-agent channels.

**Adversarial Verification:** Agents receiving another agent's output must challenge it against their own domain knowledge before building on it. This applies regardless of the producing agent's trust level.

- **Domain check:** The receiving agent evaluates the input against its own certifications and domain knowledge. If the input contradicts what the agent knows, it flags the conflict to the orchestrator rather than silently accepting or overriding.
- **Scope check:** The receiving agent verifies the input is within its competence to act on. If the input assumes capabilities or context the agent doesn't have, it flags the gap.
- **No silent propagation:** An agent must never implement, route, or build on input it has domain-informed reason to doubt. Flag first, then wait for resolution.

Trust governs whether the principal reviews intermediate outputs. Adversarial verification governs whether agents accept each other's outputs uncritically. They are independent mechanisms.

## Trust Progression

How agents earn, lose, and apply trust.

**Task Definition:** A task for trust purposes is a bounded agent invocation that produces output consumed by the principal or another agent. One briefing = one task. One research brief = one task. One outreach draft = one task. Sub-steps within a task (calendar pull, email scan) are capabilities exercised within a task, not separate tasks. Multi-agent orchestrations count as a task for each participating agent.

**Trust Ledger:** Agent performance observations are recorded in `system/state-trust-ledger.md`. The ledger is the evidence base for promotion decisions. It is not pruned — observations accumulate until promotion, then are archived within the ledger for audit trail. New observations accumulate toward the next trust level.

**Promotion from Untrusted to Trusted:**

1. **Threshold:** 5+ real tasks spanning at least 3 trust dimensions (from the agent's type), with no significant errors.
2. **Observation tracking:** When agents produce work during a session, the trust ledger is updated at session close: for each agent task, record the agent, task description, trust dimensions exercised, errors (if any), and whether the agent's knowledge was sufficient.
3. **Promotion decision:** The principal's explicit call. When the threshold is met, the AI model surfaces the recommendation with the evidence trail from the trust ledger. The principal approves or defers.
4. **Demotion:** If a Trusted agent produces a significant error, the principal may demote to Untrusted. The demotion is recorded in the trust ledger and the retrospective with rationale.

## Sweep

The ops-side inspection stage of The Loop. Scans all artifacts to identify conformance issues, staleness, and extension opportunities. Run at session close after major work.

1. Read all active artifacts in the library. Exclude `plans/archive/`, `dream/`, `data/`, and `outputs/` — archived plans, dream outputs, data store contents, and execution outputs are not active library artifacts. Read into the session's main context — artifacts loaded during initialization do not need to be re-read. Do not delegate reads to subagents; cross-artifact pattern recognition requires artifacts to be co-present in context. Subagents are only appropriate if the library exceeds the session's context capacity.
2. Check each artifact against its constraining schema for missing or non-conforming fields.
3. Check all internal references (filenames, process names, artifact names) for staleness.
4. Identify structural observations (dual-role artifacts, files that may need splitting at scale).
5. Identify improvement opportunities: repeated patterns that could be formalized, conventions that could be added, and proven capabilities in one part of the library that could extend to others.
6. Inspect `tools/worktools/` for reuse potential. For each worktool, assess: (a) Is the underlying pattern repeatable beyond the original task? (b) Can it be parameterized for broader use? (c) Should it be promoted to a registered tool or formalized as a workflow? Mark worktools with extension potential using a REVIEW marker with the reason "Worktool — observation".
7. Inspect `tools/utilities/` for correctness and staleness. Verify scripts run without errors and that hardcoded data (e.g., holiday lists) is current. Do not apply promote-or-discard logic — utilities are already in their final form.
8. For each issue found, add a REVIEW marker as a standalone line at the very top of the affected artifact. Never embed markers in body text.
9. The sweep marks — it does not fix. Fixes follow the standard Artifact Production process.
10. After marking, run Triage or note that triage is pending for a subsequent session.

## Vital Signs Read

A lightweight health assessment run during Backlog Grooming in every Developer Mode session. Reads measurable indicators of system health and surfaces any that breach their threshold. Does not produce artifacts — informs scope selection.

**Vital Signs:**

| Vital Sign | What It Measures | Threshold | Source |
|---|---|---|---|
| Retrospective backlog | Unprocessed observations | > 10 entries | `system/state-retrospectives.md` |
| REVIEW marker count | Undispositioned findings | > 5 active markers | Library-wide scan for REVIEW markers. Exclude `plans/archive/`, `dream/`, `data/`, `outputs/`. |
| Carry-forward age | Oldest unresolved cross-surface action | > 7 days | `system/state-carry-forward.md` |
| Plan backlog size | Active plans accumulating without execution | > 10 plans | `plans/backlog.md` |
| Agent trust plateau | Agents with no trust progression | All agents Untrusted after 20+ real tasks | Agent files |
| Commits ahead of origin | Unpushed local work | > 50 commits | `git status` |
| Process dormancy | Named processes not exercised | Any process dormant > 30 days | `git log`. On breach, classify per Dormancy (Latent, Absorbed, Premature, Unwired, Blocked) during Triage. |

**Steps:**

1. Read each vital sign source.
2. Compare against thresholds.
3. Verify internal consistency: for each vital sign, confirm the status label (OK / Breach) agrees with the measured value and the threshold. Do not present a status that contradicts its own evidence.
4. Surface breaches alongside the Backlog Grooming landscape summary.
5. If multiple vital signs breach simultaneously or a single vital sign is severely exceeded, recommend a full Health Check as scope for the session.

## Health Check

A deep analysis of the system's structural patterns across time. Run in Developer Mode sessions.

**Trigger:** Vital Signs Read surfaces degradation, or on request. Not every session — the Vital Signs Read is the lightweight alternative that runs every session.

1. **Artifact growth** — Which artifact types are growing? Where is complexity concentrating? Analyze via git log and the directory structure.
2. **Process coverage** — Which processes are actively referenced in recent commits? Which are dormant? Analyze via git log.
3. **Error patterns** — Are errors clustering in specific artifacts or processes? Analyze via retrospective entries categorized as friction.
4. **Retrospective themes** — What themes recur across multiple retrospective entries? Read `system/state-retrospectives.md` for patterns.
5. **Structural observations** — Identify dual-role artifacts, scaling concerns, dependency hotspots, and capability gaps across the system.
6. **Output** — Produce findings as retrospective-style entries in `system/state-retrospectives.md` and/or REVIEW markers on affected artifacts. Feed into Triage.

## Load

Ingesting external data into the system. The `load/` directory is the staging area.

1. Place source data in the `load/` directory.
2. `load/` is a staging area — data lands here but is not part of the library until processed.
3. The AI model reads and analyzes the source data, extracting what is relevant for the target artifact.
4. The extracted output is produced as a conformant artifact following standard Artifact Production.
5. Source data in `load/` is not committed to git. The directory is excluded via `.gitignore`.
6. Source data may be retained for re-processing or deleted after extraction — the principal decides per load.

## Agent Outputs

Agent-produced deliverables (briefings, reports, analyses, agendas, prep packets) are saved to `outputs/` as markdown unless a specific Workflow defines a different format (e.g., docx, xlsx).

- `outputs/` is gitignored. Output files are ephemeral deliverables, not library artifacts.
- Filename convention: `{description}-{date}.md` (e.g., `morning-briefing-2026-02-12.md`).
- An agent's Workflow defines what outputs it produces. Ad hoc outputs follow the same convention.

## Data Storage

Structured data (CSVs, spreadsheets, tabular records) is stored in `data/`. Each data store must be registered in the Data Store Registry (`system/reg-data-stores.md`) and conform to the Data Store Schema before use.

- `data/` is version-controlled.
- Agents declare their data store claims (Read/Write) in their agent definition.
- At runtime, data store claims are reflected in session state for collision detection.

**Data Store Groups:** Named collections of data stores that share access patterns. Registered in the Data Store Registry. Agents claim groups instead of individual stores. Adding a store to a group requires only a registry update — no agent file edits. Collision Check expands groups to individual file claims at runtime.

**Dimensions:** When analyzing large static datasets, meaningful filtered cuts may be saved as Dimensions — registered data stores named by their filter criteria. Dimensions enable quick cross-referencing in future sessions without re-running the analysis. Each dimension is registered in the Data Store Registry and documented in a Dimension Index with rationale, filter criteria, and timestamps.

## Research Extraction

When an Execution Mode output contains domain knowledge reusable beyond the immediate deliverable, the producing agent flags it at session close: `[EXTRACT: certification-name — description of knowledge]`. A subsequent Developer Mode session reads the flagged output and extracts the durable knowledge into the target certification's Domain Knowledge section.

- **What gets extracted:** Facts, frameworks, metrics, decision patterns, and other durable knowledge that has been validated through real work.
- **What stays in the output:** Context-specific narrative, meeting context, one-time deliverables, account-specific intelligence.
- **If no certification exists** for the domain, extraction triggers certification creation following standard Artifact Production.
- **Extraction does not require a plan.** It follows the same lightweight process as adding Best Practices to an existing certification. The flag is the trigger; the Artifact Production process governs the edit.

## Triage

The ops-side disposition stage of The Loop. Assesses observations produced by Sweep (or other sources), groups related items, and determines disposition.

1. Collect all active REVIEW markers across the library, all entries in `system/state-retrospectives.md`, any Health Check observations, and any Vital Signs Read breaches.
2. Group related items by theme or affected area.
3. For process dormancy findings, classify the dormancy before dispositioning:
   - **Latent** — waiting for its trigger condition. Monitor; no action unless latency persists beyond expected timeframe.
   - **Absorbed** — another process performs this function. Candidate for retirement or merger — but retirement is a destructive disposition that requires critical review.
   - **Premature** — built ahead of system maturity. Monitor; revisit when prerequisites emerge.
   - **Unwired** — process exists but no agent workflow exercises it. Opportunity to improve flow by wiring into agent workflows.
   - **Blocked** — should be running but is prevented by a tool gap, surface limitation, or missing dependency. Unblock; this is a health problem.
4. For each group, determine disposition:
   - **Plan** — if the group touches 3+ artifacts or requires structural change. Produce via Plan Production and Execution.
   - **Quick fix** — if addressable within standard Artifact Production. Fix and remove the marker.
   - **Defer** — if not actionable yet. Marker stays in place; re-triaged on next cycle.
   - **Marker-requested plan** — if a REVIEW marker's reason specifies a plan-level outcome, produce the plan during Triage. The marker remains on the artifact until the plan is executed and the outcome is implemented.
5. Remove REVIEW markers from artifacts whose issues have been addressed.
6. Prune retrospective entries that have been addressed (planned, fixed, or explicitly deferred with rationale).

## Drift Detection

The ops-side normalization stage of The Loop. Detects and normalizes changes that occurred between sessions. Run during initialization, before session work begins.

Drift is the steady state — sessions hang, the principal edits files, other surfaces write without committing. Change is continuous. Drift Detection normalizes whatever it finds, regardless of source.

**Exclusions:** Drift Detection excludes `data/`, `outputs/`, `plans/archive/`, and `dream/` from inspection. These directories contain data store contents, execution outputs, archived plans, and dream artifacts — not active library artifacts. Changes in these directories are expected indicators of system utilization, not structural drift.

**Inputs:** Between sessions, drift may produce:
- New plan files in `plans/`
- REVIEW markers inserted into existing artifacts
- Number prefixes on plan filenames (priority signals)
- State prefixes on plan filenames (In Progress, Executed, Superseded, Canceled)
- Files moved to `plans/archive/` (cancellation signals)
- Content edits to existing artifacts
- Session entries in session state that may no longer be active (from sessions that never closed or other surfaces that could not self-close)
- New files in `tools/worktools/` (agent-created tooling)

**Detection:**

1. Run `git status` and `git diff` to identify uncommitted changes. Exclude changes in `data/`, `outputs/`, `plans/archive/`, and `dream/` from inspection.
2. Check session state for entries that don't belong to the current session. If other sessions are registered, note them — do not assume they are stale. The principal decides whether a session is no longer active.
3. If no uncommitted changes exist and no session questions arise, skip to step 10.
4. Categorize each change:
   - **New file in `plans/`** — a plan produced outside the current session. Add to `plans/backlog.md` and dependency map.
   - **Number prefix on plan filename** (e.g., `1. plan-name.md`) — a priority signal. Record position in the Plan Backlog, then strip the prefix from the filename.
   - **State prefix on plan filename** — a state transition signal from another session or manual edit. Process per lifecycle rules (archive if terminal state).
   - **File moved to `plans/archive/`** — a cancellation signal. Remove from `plans/backlog.md`.
   - **REVIEW marker inserted** — collect for Triage. Extract any embedded notes into proper marker format.
   - **Content edit** — review for intent. Restore corrupted content if detected. Preserve intentional changes.
   - **New file in `tools/worktools/`** — agent-created tooling. Review and commit. These are version-controlled code artifacts.
   - **Carry-forward entries in `system/state-carry-forward.md`** — cross-surface actions awaiting resolution. For each entry where the current surface matches "Surface Needed": execute the action, remove the entry, and include the resolution in the normalization commit message.
   - **Possibly inactive session** — surface to the principal with the session's claimed files and plan state. The principal decides whether to remove it.

**Normalization:**

5. Strip number prefixes from plan filenames.
6. Update `plans/backlog.md` ordering based on detected priority signals.
7. Add new artifacts to the dependency map when they have structural relationships.
8. For sessions the principal identifies as no longer active: capture a retrospective entry (noting the hang as friction and what work completed), then remove the entry from session state.
9. Commit normalized state as a single logical unit with a message describing what was detected and normalized.

**Governance:**

10. The execution environment is the authority for execution against the library. Drift detection is the bridge — it interprets what happened between sessions and brings the library into conformance before session work begins.

## Collision Check

Before modifying a file, check the session state for Write conflicts with other active sessions. `system/state-session.md` is exempt — every session has implicit write access to its own entry.

1. Read `system/state-session.md`.
2. Compare the file(s) about to be modified against the Writing column of all other active sessions.
3. **Write vs. Write** — If another session has a Write claim on the same file, warn the principal with the conflicting session details. Wait for the principal's decision before proceeding.
4. **Write vs. Read** — Not a collision. The reader accepts that the file may change under it. Proceed.
5. **Read vs. Read** — Not a collision. Proceed.
6. If no conflict, proceed with the modification.

**Claim Escalation:** A session may escalate a Read claim to a Write claim mid-session. The escalation triggers a Collision Check at that moment. If another session already has a Write claim on the file, warn the principal with the conflicting session details and wait for their decision. Update session state on escalation.

## Subroutine

A bounded sub-task that any participant — the principal, the AI model, or a named agent — can spawn to parallelize work within or across sessions.

**When to use:** A task arises that is independent of the current workflow and can be completed without blocking the primary work.

**How it works:**

1. The caller signals a bounded task.
2. The task is executed as an independent unit — on the same surface (Task tool, conversation partitioning) or a different surface (parallel session, file write for Drift Detection to normalize).
3. The subroutine follows Artifact Production rules. Output is full-fidelity and written to the appropriate directory.
4. On completion, control returns to the caller. The caller is notified of what was produced.
5. The subroutine produces a trace — attributed with agent, task type, and certifications consulted.

**Constraints:**
- A subroutine does not change the parent session's mode.
- A subroutine inherits the parent session's collision check scope. If it needs files outside that scope, it registers them in session state.
- Output must be self-contained — the primary workflow should not need to parse or complete the subroutine's work.
