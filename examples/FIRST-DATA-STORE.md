# Example: Creating Your First Data Store

A data store is persistent, schema-constrained storage that agents read and write. This walkthrough creates a Health Metrics data store for the Health Tracker agent.

> **Note:** During the planting conversation, you may have chosen a different name for what the system calls a "Data Store" (e.g., Dataset, Records, Collection). Your AI uses your preferred term in conversation, but schema files and directory names use the canonical term "Data Store."

## Step 1: Read the Data Store Schema

Open `schemas/data-store-schema.md`. Key fields:

- **Name** — What this data store contains
- **Type** — State (current snapshot, overwritten) or Collection (accumulates records)
- **Format** — CSV or Markdown
- **Location** — Path in `data/`
- **Columns/Fields** — The data structure
- **Access** — Which agents can Read/Write

## Step 2: Choose Your Data Store Type

- **State** — Overwritten on each update. Use for current snapshots (e.g., "current fitness goals").
- **Collection** — Accumulates records over time. Use for logs and history (e.g., "daily health readings").

Health metrics are a time series — each day adds a row. This is a **Collection**.

## Step 3: Define the Schema

Create the data directory and file:

```
data/health/health-metrics.csv
```

With columns:

```csv
date,weight_lbs,sleep_hours,resting_hr,exercise_minutes,exercise_type,notes
```

Example rows:

```csv
date,weight_lbs,sleep_hours,resting_hr,exercise_minutes,exercise_type,notes
2026-02-20,175.2,7.5,68,30,running,Morning 5K
2026-02-21,174.8,8.0,65,0,,Rest day
```

## Step 4: Register the Data Store

Add an entry to `system/reg-data-stores.md`:

```markdown
| Health Metrics | Collection | CSV | data/health/health-metrics.csv | Health | Daily health readings — weight, sleep, heart rate, exercise |
```

Key fields in the registry:

- **Name** — Health Metrics
- **Type** — Collection
- **Format** — CSV
- **Location** — data/health/health-metrics.csv
- **Group** — Health (create this group if it's your first health data store)
- **Description** — What it contains

## Step 5: Update Agent Data Store Claims

In `agents/health-tracker.md`, the Data Stores section should reference this store:

```markdown
| Health Metrics | Read/Write | Daily health data (weight, exercise, sleep) |
```

This claim is checked at runtime for collision detection — if two agents try to write the same store simultaneously, the system catches it.

## Step 6: Commit

Commit:
1. The data store file (even if empty — the schema row establishes the structure)
2. The registry update
3. The agent update (if not already committed)

## Design Principles

- **Start with fewer columns.** You can always add columns. Removing them is harder because existing data references them.
- **Use consistent date formats.** ISO 8601 (`YYYY-MM-DD`) everywhere.
- **One concern per store.** Health metrics and financial data belong in separate stores, even if the same agent reads both.
- **Version control is your backup.** `data/` is version-controlled. Every commit preserves history. You can always recover or analyze historical data through git.
