# Example: Creating Your First Agent

This walkthrough creates a simple Health Tracker agent. Follow along with your own domain — the pattern is the same regardless of branch.

## Step 1: Read the Agent Schema

Open `schemas/agent-schema.md`. Every agent must conform to this structure. The key fields are:

- **Name** — What you call the agent
- **Purpose** — What it does (one sentence)
- **Agent Type** — Domain Expert, Developer, Library Developer, or Architect
- **Tools** — Which registered tools it uses
- **Certifications** — Which knowledge bases it consults
- **Decision Rules** — When to act, when to defer, when to escalate
- **Trust Level** — Starts at Untrusted

## Step 2: Define the Agent

Create a file at `agents/health-tracker.md`:

```markdown
# Health Tracker

## Purpose

Tracks health metrics, surfaces trends, and prepares wellness briefings for the principal.

## Agent Type

Domain Expert

## Tools

| Tool | Usage |
|---|---|
| Claude Code | File operations, data analysis |
| Git | Version control for health data |

## Certifications

| Certification | Role |
|---|---|
| Wellness Fundamentals | Domain knowledge for health metric interpretation |

## Data Stores

| Store | Access | Purpose |
|---|---|---|
| Health Metrics | Read/Write | Daily health data (weight, exercise, sleep) |

## Decision Rules

- When asked about health trends, analyze the Health Metrics data store and surface patterns.
- When data seems anomalous (e.g., sudden large changes), flag it rather than interpreting it. Health data interpretation has real consequences.
- Do not provide medical advice. Surface data and patterns; the principal makes health decisions.
- When a metric has insufficient data points (< 7 days), note the limitation rather than presenting a trend.
- Defer to the principal on what metrics to track. Do not expand the data schema without approval.

## Trust Level

Untrusted

## Trust Dimensions

| Dimension | What It Measures |
|---|---|
| Data accuracy | Are recorded metrics correct and consistent? |
| Trend identification | Are surfaced patterns real and meaningful? |
| Appropriate restraint | Does the agent flag uncertainty rather than overinterpret? |
| Schema conformance | Do outputs follow the library's conventions? |

## Dependencies

- Wellness Fundamentals (certification)
- Health Metrics (data store)

## Notes

This is a starter agent. As trust builds and the Health branch matures, its capabilities will expand to include meal planning, exercise programming, and wellness briefing workflows.
```

## Step 3: Register and Commit

1. The agent references a certification (`Wellness Fundamentals`) and a data store (`Health Metrics`). Create those next — see FIRST-CERTIFICATION.md and FIRST-DATA-STORE.md.
2. Update the dependency map if needed.
3. Commit the agent file.

## What Makes a Good Agent

- **Narrow purpose.** One sentence. If you need "and" in the purpose, you might need two agents.
- **Explicit decision rules.** These are the agent's operating boundaries. When unclear, the rule should say "defer to the principal."
- **Conservative trust dimensions.** Pick 3-5 measurable areas. The agent earns autonomy by demonstrating competence in these areas.
- **Honest limitations.** An agent that says "I don't know" when it doesn't is more trustworthy than one that guesses.
