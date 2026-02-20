# Artifact Production Rules

- Propose all changes before implementing. Do not write artifacts until approved in conversation.
- Draft following the constraints for the artifact type.
- Review against the library for correctness, completeness, and consistency.
- When modifying an existing artifact, assess impact: (a) check the dependency map for structural relationships, and (b) search artifact Dependencies sections for artifacts that declare a dependency on the modified artifact.
- When an artifact needs future attention, add a REVIEW marker as a standalone line at the very top of the artifact (first non-blank line). Never embed markers in body text. Categories: conformance gap, structural observation, stale reference, improvement opportunity.
- **Signal hygiene:** When documentation references a searchable signal (REVIEW markers, state prefixes, or any grep-scanned pattern), never reproduce the literal signal string in body text. Describe the signal without emitting it. Every false positive is wasted tokens.
- Any tool used must be registered in the tool registry.
- New artifacts with Dependencies sections (agents, certifications, personas, plans, specs, data stores, env state files) declare relationships there — not in the dependency map. New artifacts without Dependencies sections (tools, processes, rules, infrastructure) are added to the dependency map.
- Use targeted edits rather than full rewrites when modifying existing artifacts.
- Before executing a plan, check `plans/` filenames for state prefixes. If a plan already has a state prefix, do not begin work on it.
- Claim a plan by renaming with an In Progress state prefix and committing before starting execution.
- Mark a plan Executed, Superseded, Canceled, or Inert by renaming with the corresponding state prefix. Inert marks a plan that predates the lifecycle process — not actionable, excluded from Sweep and Vital Signs.
- When a plan reaches a terminal state (Executed, Superseded, Canceled, Inert), move it to `plans/archive/` and remove it from `plans/backlog.md`.
- `plans/backlog.md` is read-only during plan execution. Only modify it when adding, reordering, or removing plans.
- Sweep excludes `plans/archive/`, `dream/`, `data/`, and `outputs/`. These are not active library artifacts.
- Sweep inspects `tools/worktools/` for reuse potential. Mark worktools with extension potential using a REVIEW marker with the reason "Worktool — observation".
- When archiving a plan, strip any REVIEW markers from the file. Archived plans must not carry inert markers.
- REVIEW markers that specify a plan-level outcome (workflow definition, structural change) generate a plan during Triage. The marker remains until the plan is executed.
