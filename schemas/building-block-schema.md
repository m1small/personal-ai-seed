# Building Block Schema

## Purpose

Defines the base fields for any building block artifact type. All type-specific building block schemas (Agent Schema, Certification Schema, and future types) must include these fields. Type-specific schemas add their own fields on top of these.

## Conformance

Strict. Each field listed below must appear by name in every type-specific building block schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | The building block's name. Convention: the H1 heading serves as the Name field. No separate `## Name` section is needed. |
| 2 | Purpose | text | yes | What this building block does. Its unit of reuse. |
| 3 | Dependencies | list | no | Other artifacts this building block relies on. Referenced by name. |
| 4 | Notes | text | no | Open questions, context, or operational guidance. |
