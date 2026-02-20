# Data Store Schema

## Purpose

Defines the required fields for any data store artifact. All data stores registered in `system/reg-data-stores.md` must conform to this schema. Extends the Building Block Schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | Human-readable name for the store. (Building Block base field.) |
| 2 | Purpose | text | yes | What this data store holds and why. (Building Block base field.) |
| 3 | Type | enum | yes | State or Collection. Governs behavioral rules. |
| 4 | Format | enum | yes | Storage format. Values: CSV, Markdown, Text. Extensible — new formats are added as needed. |
| 5 | Location | text | yes | File path relative to repo root. |
| 6 | Fields | list | conditional | Column/field definitions. Required when Format is CSV. Optional for Markdown. Not applicable for Text. |
| 7 | Owner | text | yes | The agent with primary Write responsibility. Referenced by agent name. |
| 8 | Dependencies | list | no | Other artifacts this data store relies on. (Building Block base field.) |
| 9 | Notes | text | no | Open questions, context, or operational guidance. (Building Block base field.) |
| 10 | Group | text | no | The Data Store Group this store belongs to, if any. Managed in the Data Store Registry Groups section. |

## Type Rules

| Type | Behavior |
|---|---|
| State | Current snapshot. Updates overwrite. Only the present value matters. No append history. |
| Collection | Records accumulate over time. Supports append, update, and query. Ordering conventions defined per store in Notes. |

## Access Rules

Agents declare default claims (Read or Write) on data stores in their Agent Schema `Data Stores` field. At runtime, active claims are tracked through session state as file-level claims.

- **Write vs. Write** on the same data store is a collision. Warn the principal.
- **Write vs. Read** is not a collision. The reader accepts the data may change.
- An agent may internalize data from a store it reads into its own state. This is a read, not a duplication concern.
