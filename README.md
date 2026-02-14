# Claude Code Agents & Skills Library

Reusable, project-agnostic agents and skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Drop them into any project's `~/.claude/` directory to get a consistent set of workflows.

## Setup

Symlink into your Claude Code config:

```bash
ln -sf ~/Documents/myclaude/agents ~/.claude/agents
ln -sf ~/Documents/myclaude/skills ~/.claude/skills
```

Or copy individual files into an existing `~/.claude/` setup.

## Agents

| Agent | Model | Description |
|-------|-------|-------------|
| `architect` | opus | Senior software architect for feature design, architecture decisions, and spec writing. Dialogue-first — explores the problem before proposing solutions. |
| `frontend-engineer` | sonnet | Implements frontend features from specs with comprehensive testing. React/TypeScript focused, but adapts to the project's stack. |

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| `architect` | `/architect` | Start an architectural discussion about a feature or problem |
| `start-task` | `/start-task` | Rebase, find a task in the project's plan file, create a branch, enter plan mode |
| `close-task` | `/close-task` | Mark a task as done in the plan file and commit |
| `merge-workspace` | `/merge-workspace` | Merge a git worktree branch into main with preview and confirmation |
| `visual-qa` | `/visual-qa` | Visual QA testing with Playwright screenshots |

## Design Principles

- **Discover, don't hardcode** — Skills detect project structure (test frameworks, task files, worktrees) rather than assuming paths
- **Methodology over configuration** — The workflows and checklists are the value; project details are discovered at runtime
- **Self-contained** — Each file works standalone without requiring a project-specific CLAUDE.md
