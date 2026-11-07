# Persistent project memory

For every ongoing project task, automatically read the project's `SESSION_MEMORY.md` before acting and keep it updated as work proceeds. Record each user request or correction, material decision, completed work unit, project-changing action, check result, and the next concrete step as concise dated checkpoints. Before ending, handing work to another agent, or reaching a context boundary, save and verify the current state. Use one canonical Markdown file in the project root (or the path already specified by project instructions). Treat workspace evidence as authoritative when resuming.

This file is a portable activation layer: copy it to a project root for agent systems that load `AGENTS.md`. For systems using a different always-loaded rules file, carry over this instruction there. The agent performs the writes during its active turns; this is not a background daemon.
