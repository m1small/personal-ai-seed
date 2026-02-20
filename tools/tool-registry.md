# Tool Registry

The authoritative index of all tools used in the system. A tool must be registered here before use. Undocumented tool usage is not permitted.

## Registered Tools

| Tool | Integration Type | Connection Method | Purpose |
|---|---|---|---|
| Claude Code | Execution Environment | Native | Primary execution environment for file operations and version control. |
| Git | Execution Environment | CLI | Version control system. Source of truth for artifact history. |

## Tool Dependencies

| Tool | Depends On | How |
|---|---|---|
| Git | Claude Code | Git commands are executed through Claude Code. |
| Claude Code | Git | Claude Code uses git for version control operations. |

## Notes

This is the minimal starter registry. As you connect additional tools (Slack, Notion, Google Drive, etc.), register them here following the Integration Framework's Interface Contract Schema. Each tool gets its own contract file in `tools/`.
