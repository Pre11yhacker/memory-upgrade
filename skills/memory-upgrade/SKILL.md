---
name: memory-upgrade
description: Automatically maintain and restore durable Markdown checkpoints throughout any ongoing project session, including user requests, decisions, actions, results, and next steps, so work survives context-window changes and can transfer between compatible agent systems.
---

# Memory upgrade

Apply this workflow automatically whenever working in an existing project or carrying out multi-step project work; the user does not need to invoke the skill. Keep work recoverable across turns, context changes, and agent handoffs by storing checkpoints in the project itself.

This is an agent instruction package, not a daemon. The active agent must write the checkpoints as it works. For systems that support portable `SKILL.md` files, make the skill discoverable for implicit invocation. For other systems, place the accompanying `AGENTS.md` activation instructions in the project root or translate that short instruction into the system's always-loaded project rules.

## Workflow

1. **Locate memory before work.** Identify the project root and read its `SESSION_MEMORY.md` if present. Follow any project-specific memory path already named by `AGENTS.md` or other project instructions. If no memory exists, create `SESSION_MEMORY.md` in the project root when there is meaningful ongoing project work, using the bundled `templates/SESSION_MEMORY.md` as a starter when available. Do not create project memory for a one-off general conversation.
2. **Restore before acting.** Extract the current objective, constraints, decisions, progress, touched files, outstanding questions, and next concrete action. Check the working tree and relevant files to reconcile the note with the actual project state. Treat the repository as authoritative for current code; mark outdated memory as stale and correct it.
3. **Checkpoint continuously.** Capture each new user request or correction, consequential decision, completed work unit, command or tool action that changes project state, and the result of each check. Update the memory file during the same turn, grouping closely related events into one dated entry. Include failed attempts when they affect the next step. Keep a concise chronological timeline; never imply that an action succeeded if its result is unknown.
4. **Checkpoint at boundaries.** Before ending a work session, handing work to another agent, or when context is getting crowded, update the file. Put the immediate next action first in the current-state section so a fresh session can resume without replaying the whole timeline. A checkpoint is required even if the task is unfinished.
5. **Verify the checkpoint.** Re-read the saved file and ensure it names the actual status, preserves unresolved work, and distinguishes completed, in-progress, and not-yet-started work. Tell the user when the memory file was created or materially updated if useful to the task.

## Memory content

Use one canonical Markdown file, normally `SESSION_MEMORY.md`, with a compact structure such as:

- **Current state:** objective, current status, next action.
- **Project context:** architecture or domain facts needed for this task, with pointers to source files.
- **Decisions and constraints:** decision, reason, and relevant user preference or requirement.
- **Progress log:** dated, chronological material events, including changes made and checks actually run.
- **Open items:** blockers, unanswered questions, risks, and deferred work.

Preserve useful prior context when updating. Keep the current state concise; move older resolved events into a brief history or prune them only after their lasting decisions and outcomes are represented elsewhere in the same file. Prefer links and file paths over copied source code.

## Accuracy and privacy

Write verified facts as facts and label assumptions or inferences. Record validation only when it was actually performed, with its result. Never invent missing session history: mark it unknown and continue from evidence available in the workspace. Capture every material part of the project session as checkpoints rather than copying every message, tool call, or output verbatim. Exclude credentials, access tokens, private keys, and unrelated sensitive personal information; note that a secret exists only when necessary, without copying its value.
