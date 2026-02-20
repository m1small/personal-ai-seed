# Persona Schema

## Purpose

Defines the required fields for any persona artifact. All personas in the `personas/` directory must conform to this schema.

A Persona captures how a principal communicates and presents themselves in a specific context. Agents reference a Persona to mirror the principal's voice, positioning, and behavioral patterns.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | The persona's name. Convention: the H1 heading serves as the Name field. |
| 2 | Purpose | text | yes | What this persona governs — the context and platform. |
| 3 | Principal | text | yes | Who this persona represents. |
| 4 | Context | text | yes | The scope in which this persona operates (e.g., professional outreach, conference speaking, internal team). |
| 5 | Sources | list | yes | Data sources that contributed to this persona. Each entry includes source name, date, and what it contributed. Sources accumulate over time. |
| 6 | Refinements | flexible | no | Accumulated observations from comparing agent drafts against the principal's actual communications. Captures voice patterns not present in source data. Entries include the observation, source context, and date. |
| 7 | Voice | flexible | yes | Communication style traits: tone, formality, vocabulary, sentence structure, recurring patterns. |
| 8 | Positioning | flexible | yes | How the principal positions themselves professionally in this context. |
| 9 | Interests | flexible | no | Topics and themes the principal engages with in this context. |
| 10 | Network Profile | flexible | no | Characteristics of the principal's network and engagement patterns. |
| 11 | Constraints | flexible | no | Behavioral boundaries specific to this persona. |
| 12 | Dependencies | list | no | Other artifacts this persona relies on. |
| 13 | Notes | text | no | Open questions, context, or operational guidance. |

## Notes

- Personas are initially produced via the Load process and enriched over time through additional sources and refinements. When an agent drafts a communication and the principal edits it, recurring diff patterns are added as refinements.
- A principal may have multiple personas for different contexts.
- Agents reference personas by name in their decision rules or dependencies.
