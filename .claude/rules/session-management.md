# Session Management Rules

- Declare session mode (Developer or Execution) at initialization. Mode must be explicit.
- Read `system/state-session.md` on initialization. Run Drift Detection to detect and normalize drift (uncommitted changes, sessions the principal identifies as no longer active) before declaring session mode.
- Load the environment state file declared in `CLAUDE.md` after Drift Detection. If no environment is declared, warn. If the file doesn't exist, ask the principal for a discovery prompt.
- Register the session with mode, task summary, reading files, writing files, and start time.
- Update the session state Reading and Writing columns as new files come into scope during work.
- Run Collision Check before modifying files. Only Write vs. Write is a collision — Write vs. Read and Read vs. Read are not collisions.
- A Read claim may be escalated to a Write claim mid-session. Escalation triggers a Collision Check at that moment.
- When an idea emerges outside the session's scope, append it to the Journal (`system/state-journal.md`) and return to the current task. Capture and continue — do not pursue out-of-scope ideas inline.
- On close, capture a retrospective entry in `system/state-retrospectives.md` (date, session name, category, observation) and commit.
- On close, if agents produced work during this session, update the trust ledger (`system/state-trust-ledger.md`): for each agent task, record the agent, task description, trust dimensions exercised, errors, and knowledge sufficiency. If an agent meets the promotion threshold, surface the recommendation to the principal.
- Remove the session's entry from `system/state-session.md` on close.
