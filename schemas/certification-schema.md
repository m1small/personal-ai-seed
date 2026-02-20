# Certification Schema

## Purpose

Defines the required fields for any certification artifact. All certifications in the `certifications/` directory must conform to this schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | The certification name. |
| 2 | Purpose | text | yes | What this domain solves and why certification in it matters. |
| 3 | Scope | text | yes | What domain knowledge is and is not covered. |
| 4 | Domain Knowledge | flexible | yes | Inline knowledge: concepts, models, patterns, and rules for this domain. |
| 5 | API Reference | flexible | no | Organized index of API services by feature area. Not a recreation of docs — a table of contents for finding the right API for the job. |
| 6 | References | list | yes | External sources: URLs, documentation, APIs. Each with a summary of what it provides. |
| 7 | Best Practices | flexible | no | Accumulated patterns for effective use. Grows organically through work. |
| 8 | Dependencies | list | no | Other artifacts this certification relies on. Referenced by name. |
| 9 | Notes | text | no | Open questions, context, or maintenance guidance. Category, decomposition rationale, and refresh cadence live here. |

## Certification Taxonomy

Certifications fall into distinct categories. The category is informational — the schema is the same — but it guides scoping and decomposition decisions. Record a certification's category in its Notes section.

| Category | Scope | Examples |
|---|---|---|
| Product | What you build and sell | Your product's architecture, capabilities, competitive positioning |
| Framework | Industry standards and vocabulary | FinOps, ITIL, compliance frameworks |
| Platform | Managed services from platforms — APIs, hosting, infrastructure | Cloud AI services, SaaS platforms |
| Developer | Open-source toolchains for building applications | Orchestration runtimes, agent frameworks, model composition |
| Vertical | Buyer segment dynamics, economics, personas | Industry verticals, market segments |

## Decomposition Principles

A certification should be an independently valuable knowledge domain reusable across multiple agents. Split when:

1. **Different agents need different subsets.** If loading the whole block wastes context or creates noise for some consumers, the block contains more than one domain.
2. **Independent refresh cycles.** If one section changes weekly (market data) and another is stable for months (framework principles), they're probably different domains.
3. **The reuse graph diverges.** When one part of the cert is referenced by agents A, B, C and another part only by agent B — that's a seam.

**Corollary:** If only one agent would ever load a certification, that knowledge probably belongs in the agent's decision rules or state, not a certification.
