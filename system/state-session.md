# Session State

A live manifest of active sessions. Used for collision detection across concurrent sessions. Each session registers on initialization and removes its entry on close.

## Active Sessions

| Session | Mode | Working On | Reading | Writing | Started |
|---|---|---|---|---|---|

## Rules

- **Session state is exempt from Collision Check.** Every session has implicit write access to this file for its own entry. Sessions only modify their own row. Do not list `system/state-session.md` in Reading or Writing columns.
- On initialization, register the session with mode, task summary, reading files, writing files, and start time.
- Before modifying a file, check this table for Write claims by other sessions on that file.
- **Write vs. Write** on the same file is a collision. Warn the principal with the conflicting session details and wait for their decision.
- **Write vs. Read** on the same file is not a collision. The reader accepts that the file may change under it.
- **Read vs. Read** is not a collision.
- A session may escalate a Read claim to a Write claim mid-session. The escalation triggers a Collision Check at that moment.
- Update the Reading and Writing columns as work proceeds and new files come into scope.
- On session close, remove the session's entry.
- During Drift Detection, sessions that the principal identifies as no longer active are removed as part of normalization.
- This file contains only active sessions — no history.
