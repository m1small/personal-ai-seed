# Example: Creating Your First Certification

A certification is a knowledge base that agents consult. It combines inline domain knowledge with external references. This walkthrough creates a Wellness Fundamentals certification for the Health Tracker agent.

> **Note:** During the planting conversation, you may have chosen a different name for what the system calls a "Certification" (e.g., Playbook, Knowledge Base, Expertise). Your AI uses your preferred term in conversation, but schema files and directory names use the canonical term "Certification."

## Step 1: Read the Certification Schema

Open `schemas/certification-schema.md`. Key fields:

- **Name** — The knowledge domain
- **Purpose** — What knowledge this provides
- **Category** — How this knowledge is classified
- **Domain Knowledge** — Inline facts, frameworks, and patterns
- **External References** — Links to authoritative sources
- **Best Practices** — Proven patterns discovered through use

## Step 2: Define the Certification

Create a file at `certifications/wellness-fundamentals.md`:

```markdown
# Wellness Fundamentals

## Purpose

Provides baseline health and wellness knowledge for interpreting personal health metrics. Grounds agent analysis in established health science rather than speculation.

## Category

Domain Knowledge — Health

## Domain Knowledge

### Vital Metrics and Normal Ranges

| Metric | Normal Range | Notes |
|---|---|---|
| Resting heart rate | 60-100 bpm | Athletes may be lower. Trend matters more than single reading. |
| Sleep duration | 7-9 hours | Individual needs vary. Consistency matters more than exact hours. |
| Body weight | Varies by individual | Weekly average is more meaningful than daily readings. Day-to-day fluctuation of 1-3 lbs is normal. |

### Trend Analysis Principles

- **Minimum data window:** 7 days for short-term trends, 30 days for meaningful patterns.
- **Outlier handling:** A single anomalous reading should be flagged, not incorporated into trend analysis.
- **Seasonal variation:** Some metrics (weight, activity levels) have natural seasonal patterns. Compare same-season periods when possible.
- **Correlation is not causation:** When two metrics move together, surface the correlation. Do not claim one causes the other.

### Boundaries

- This certification does not qualify the agent for medical advice, diagnosis, or treatment recommendations.
- When metrics fall outside normal ranges persistently (> 7 days), the agent should recommend the principal consult a healthcare provider.
- The agent interprets data; the principal makes decisions.

## External References

| Source | URL | What It Provides |
|---|---|---|
| CDC Physical Activity Guidelines | https://www.cdc.gov/physicalactivity/ | Exercise recommendations by age group |
| NIH Sleep Recommendations | https://www.nhlbi.nih.gov/health/sleep | Sleep duration and quality guidelines |

## Best Practices

*This section grows through use. When the Health Tracker agent discovers patterns that improve its analysis — a better way to present trends, a metric combination that's particularly insightful — those learnings are extracted here via the Research Extraction process.*

## Dependencies

None — this is a foundational certification.

## Notes

Start minimal. This certification will grow as you use the Health branch. Real-world use surfaces what knowledge the agent actually needs — don't try to capture everything upfront.
```

## Step 3: Commit

Commit the certification file. The Health Tracker agent can now consult it.

## How Certifications Grow

Certifications are living documents. They grow through two mechanisms:

1. **Research Extraction** — When an Execution Mode session produces domain knowledge that's reusable, the agent flags it for extraction into the certification.
2. **Developer Mode refinement** — When you notice the agent lacks knowledge, add it in a Developer Mode session.

Start small. Let real work reveal what the certification needs.
