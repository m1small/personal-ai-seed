# Sapling Schema

## Purpose

Defines the required fields for any sapling definition artifact. All sapling definitions in the `saplings/` directory must conform to this schema. Extends the Building Block Schema.

A sapling definition is metadata about a distributable Personal AI — what it contains, who it's for, and where to find it. The definition lives in the seed repo; the sapling itself is a separate repository.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | The sapling's name. (Building Block base field.) |
| 2 | Purpose | text | yes | Who this sapling is for and what it provides. (Building Block base field.) |
| 3 | Source | text | yes | Repository URL where the sapling can be cloned. |
| 4 | Audience | text | yes | Target recipients — who would benefit from starting with this sapling instead of the seed. |
| 5 | Pre-grown Branches | list | yes | What's included beyond the seed. Each entry names a branch or capability area and briefly describes what's pre-built. |
| 6 | Customization Points | list | yes | What recipients need to personalize. Each entry names something that needs adaptation (credentials, personas, agent names, domain knowledge). |
| 7 | Tool Requirements | list | no | Tools that should be connected for the sapling's full capability. Referenced by name from the tool registry. |
| 8 | Origin Tree | text | no | Which tree this sapling was extracted from. Attribution, not dependency — the sapling is self-contained. |
| 9 | Dependencies | list | no | Other artifacts this sapling definition relies on. (Building Block base field.) |
| 10 | Notes | text | no | Open questions, context, or operational guidance. (Building Block base field.) |

## Sapling vs. Seed

| Dimension | Seed | Sapling |
|---|---|---|
| Branches | Empty directories | Pre-built content in some branches |
| Agents | None | Template agents with decision rules |
| Certifications | None | Template certifications or guidance |
| Data Stores | Empty registry | Pre-structured stores with headers |
| Tool Contracts | Minimal (Claude Code, Git) | Domain-specific tool templates |
| Planting Conversation | Vocabulary calibration only | Vocabulary calibration + branch tour |
| Personalization | Build everything from scratch | Customize what's pre-built, build what's missing |
