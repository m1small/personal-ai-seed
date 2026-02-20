# Spec Schema

## Purpose

Defines the required fields for any spec artifact. All specs in the library must conform to this schema.

## Fields

| # | Field | Type | Required | Description |
|---|---|---|---|---|
| 1 | Name | text | yes | What this spec defines. |
| 2 | Scope | text | yes | What is and is not included. |
| 3 | Requirements | flexible | yes | What this thing must do or contain. Structure determined per spec. |
| 4 | Dependencies | list | no | Other artifacts this spec relies on. Referenced by name. |
| 5 | Notes | text | no | Open questions, context, or decisions made. |
