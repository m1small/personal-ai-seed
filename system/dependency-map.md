# Dependency Map

Structural relationships between artifacts. Used to assess impact before changes.

This map holds structural relationships that are not declared in individual artifact Dependencies sections. For the complete dependency picture, also check artifact Dependencies sections. Artifact types with self-declared dependencies: agents, certifications, personas, plans, specs, data stores, environment state files.

## Relationship Types

| Relationship | Meaning |
|---|---|
| **depends on** | Cannot be produced without the other artifact existing. |
| **constrains** | Defines the structure another artifact must follow. |
| **references** | Mentions another artifact without structural dependency. |

## Map

| Artifact | Relationship | Target |
|---|---|---|
| Spec Schema | constrains | all specs |
| Plan Schema | constrains | all plans |
| Building Block Schema | constrains | Agent Schema |
| Building Block Schema | constrains | Certification Schema |
| Building Block Schema | constrains | Persona Schema |
| Building Block Schema | constrains | Environment State Schema |
| Building Block Schema | constrains | Data Store Schema |
| Agent Schema | constrains | all agents (`agents/`) |
| Agent Schema | depends on | Integration Framework |
| Agent Schema | references | Data Store Schema |
| Certification Schema | constrains | all certifications (`certifications/`) |
| Persona Schema | constrains | all personas (`personas/`) |
| Environment State Schema | constrains | all environment state files (`system/env-*.md`) |
| Environment State Schema | references | Tool Registry |
| Environment State Schema | references | Integration Framework |
| Data Store Schema | constrains | all data stores (`data/`) |
| Integration Framework | constrains | all tool contracts (`tools/`) |
| Integration Framework Reference | depends on | Integration Framework |
| Tool Registry | references | all tools |
| Tool Registry | depends on | Integration Framework |
| Glossary | references | all artifacts |
| Processes | references | Glossary |
| Processes | references | Artifact Production |
| CLAUDE.md | references | all library artifacts |
| `.claude/rules/` | depends on | Processes |
| Credential Storage Spec | depends on | Integration Framework |
| Credential Storage Spec | references | Tool Registry |
| Session State | references | Processes |
| Session Lifecycle | references | Initialization |
| Session Lifecycle | references | Session State |
| Session Lifecycle | references | Artifact Production |
| Session Lifecycle | references | Error Handling |
| Session Lifecycle | references | Backlog Grooming |
| Session Lifecycle | references | Retrospectives |
| Session Lifecycle | references | Trust Ledger |
| Session Lifecycle | references | Carry-Forward Queue |
| Collision Check | references | Session State |
| Triage | references | Sweep |
| Triage | references | Artifact Production |
| Triage | references | Plan Production and Execution |
| Triage | references | Retrospectives |
| Vital Signs Read | references | Retrospectives |
| Vital Signs Read | references | Carry-Forward Queue |
| Vital Signs Read | references | Plan Backlog |
| Vital Signs Read | references | Backlog Grooming |
| Health Check | references | Vital Signs Read |
| Health Check | references | Triage |
| Health Check | references | Sweep |
| Health Check | references | Retrospectives |
| Health Check | references | Dependency Map |
| Trust Ledger | references | Trust Progression |
| Trust Progression | references | Trust Ledger |
| Drift Detection | references | Dependency Map |
| Drift Detection | references | Plan Backlog |
| Drift Detection | references | Session Lifecycle |
| Drift Detection | references | Carry-Forward Queue |
| Initialization | references | Drift Detection |
| Initialization | references | Environment State |
| Agent Orchestration | references | Agent Schema |
| Agent Orchestration | references | Integration Framework |
| Backlog Grooming | references | Plan Backlog |
| Backlog Grooming | references | Carry-Forward Queue |
| Backlog Grooming | references | Retrospectives |
| Backlog Grooming | references | Vital Signs Read |
| Subroutine | references | Artifact Production |
| Subroutine | references | Drift Detection |
| Subroutine | references | Session Lifecycle |
| Subroutine | references | Collision Check |
| Dream Mode Session Lifecycle | references | Dream (`dream/`) |
| Dream (`dream/`) | references | Processes (Dream Mode Session Lifecycle) |
| Sweep | references | `outputs/` (exclusion) |
| Sweep | references | `tools/worktools/` (inclusion) |
| Sweep | references | `tools/utilities/` (inclusion) |
| Drift Detection | references | `outputs/` |
| Drift Detection | references | `tools/worktools/` |
| Bootstrap | references | Glossary |
| Bootstrap | references | Processes |
| Bootstrap | references | Environment State Schema |
