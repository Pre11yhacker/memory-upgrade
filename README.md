<div align="center">

# 🧠 Memory Upgrade

### Project context that survives the context window.

A portable agent skill for saving the decisions, progress, and next steps that make a project easy to resume.

[Agent Skills standard](https://agentskills.io/) · [Install](#-install) · [How it works](#-how-it-works)

</div>

---

## The problem

Long-running project work gets split across chats, context windows, and agents. Important choices and unfinished steps can disappear between sessions. **Memory Upgrade** keeps a small, readable SESSION_MEMORY.md in the project so the next session can pick up from the real state of the repository.

## What it records

- The current objective, status, and next concrete action
- Decisions, constraints, and user corrections
- Meaningful changes, commands, and checks, with their actual outcomes
- Open questions, blockers, and deferred work

The result is a checkpoint trail, not a transcript. It stays concise and points to project files instead of copying large code or tool output.

## ⚡ Install

### One command for multiple agents

Install with the [GitHub CLI skill command](https://cli.github.com/manual/gh_skill_install) (requires a version that includes gh skill):

    gh skill install Pre11yhacker/memory-upgrade memory-upgrade --agent codex --agent claude-code --agent cursor --agent github-copilot --agent opencode --scope user

Remove any --agent entries for tools you do not use. To install only for the current project, change --scope user to --scope project. See [gh skill install](https://cli.github.com/manual/gh_skill_install) for supported agents and options.

### Make checkpoints part of every project session

Skills are commonly selected when relevant. For a stronger always-on workflow, copy [skills/memory-upgrade/AGENTS.md](skills/memory-upgrade/AGENTS.md) into each project root, merging it with existing instructions. This makes the checkpoint rule visible at the start of project sessions in agents that load AGENTS.md. If your agent uses another always-loaded rules file, add the same short instruction there.

The skill and bootstrap are complementary: the skill contains the full workflow; the project rule reminds the agent to keep applying it.

## 🔄 How it works

    New session
        ↓
    Read SESSION_MEMORY.md and reconcile it with the repository
        ↓
    Work in small units and save dated checkpoints as the state changes
        ↓
    Update the current status and next action before a handoff or pause
        ↓
    Next session resumes from the checkpoint

Memory lives in one Markdown file, normally at the project root. If it does not exist, the skill can start from [templates/SESSION_MEMORY.md](skills/memory-upgrade/templates/SESSION_MEMORY.md).

## 🧭 Agent compatibility

The skill uses the open SKILL.md format rather than a platform-specific API. GitHub CLI installs skills for many hosts, including Codex, Claude Code, Cursor, GitHub Copilot, Gemini CLI, and OpenCode. The exact location and whether skills are automatically considered depend on each host; use the host's always-loaded project instructions for the most reliable per-session checkpointing.

- [Agent Skills specification](https://agentskills.io/specification)
- [GitHub Copilot: add agent skills](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)
- [Cursor: project instructions and AGENTS.md](https://docs.cursor.com/context/rules-for-ai)
- [OpenCode: agent skills](https://opencode.ai/docs/skills/)

## 🔒 Accuracy and privacy

The memory is a normal project file. Keep verified facts separate from assumptions, record checks only after they run, and treat the repository as authoritative when resuming. Never copy credentials, private keys, or unrelated sensitive information into the checkpoint. Decide whether to commit SESSION_MEMORY.md based on whether the project context should be shared with collaborators.

> **A note on “background” behavior:** this is an instruction workflow, not a separate process watching the session. The active agent writes checkpoints as it works. It summarizes material project events instead of capturing every token or raw tool output, and it cannot record work while the agent is inactive.

## 📁 Repository layout

    AGENTS.md                          # instructions for agents working on this repository
    README.md
    skills/
    └── memory-upgrade/
        ├── AGENTS.md                  # portable always-loaded project bootstrap
        ├── SKILL.md                   # reusable workflow
        └── templates/
            └── SESSION_MEMORY.md      # starter for a project's memory file

## Contributing

Improvements to the workflow should keep the skill portable, concise, and honest about what an agent can verify. Please include the relevant agent host and installation context when reporting compatibility issues.
