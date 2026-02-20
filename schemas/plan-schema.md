# Plan Schema

## Purpose

Defines the required fields for any plan artifact. All plans in the `plans/` directory (including `plans/archive/`) must conform to this schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Summary | text | yes | What this plan proposes and why. |
| 2 | Rationale | text | yes | Why this work is needed. |
| 3 | Current State | text | no | Relevant state before changes. Omit when obvious from context. |
| 4 | Changes | flexible | yes | What will be done. Structure determined per plan. |
| 5 | Dependencies | list | no | Other artifacts this plan affects or relies on. Referenced by name. |
