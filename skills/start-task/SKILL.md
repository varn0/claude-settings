---
name: start-task
description: Rebase from main, find a task in the project's task/build plan file, and enter plan mode to start implementation.
user-invocable: true
argument-hint: [feature or task name from the task plan]
---

Start implementing a task from the project's task plan.

## Finding the Task Plan

Look for a task/build plan file in these common locations (in order):
- `BUILD_PLAN.md`
- `TODO.md`
- `docs/BUILD_PLAN.md`
- `docs/TODO.md`
- `TASKS.md`
- Any `.md` file with "plan" or "task" in the name under `docs/`

If no task plan file is found, ask the user for the path.

## Steps

1. **Rebase from local main** — bring the current branch up to date with the latest tested state:
   ```
   git rebase main
   ```
   - Rebase against the **local** `main` branch (not `origin/main`), since local main may have commits not yet pushed to remote.
   - If the rebase has conflicts, stop and inform the user. Do NOT force-resolve conflicts.
   - If the branch is already up to date, proceed.

2. **Read the task plan** file found above.

3. **Find the matching task** — search for an unchecked line (`- [ ]`) that best matches: `$ARGUMENTS`
   - Match by substring or fuzzy relevance.
   - If multiple lines could match, show the candidates and ask the user to pick one.
   - If no match is found, tell the user and stop.

4. **Show the matched task** to the user, including any sub-tasks and linked spec if present.

5. **Create a task branch** — create and checkout a new branch for this task:
   - Derive a short kebab-case slug from the task description (e.g., "Add trial license support" -> `trial-license-support`)
   - Choose the prefix based on the nature of the task:
     - `feat/` — new feature or capability
     - `fix/` — bug fix
     - `build/` — build system, CI, packaging changes
     - `test/` — adding or updating tests
     - `chore/` — maintenance, refactoring, docs, config changes
   - Create the branch: `git checkout -b <prefix>/<slug>`
   - If unsure which prefix fits, ask the user.

6. **Check for a linked spec** — if the task line contains a markdown link to a spec (e.g., `See [spec](../specs/some-spec.md)`), read that spec file to understand the full requirements.

7. **Enter plan mode** — use `EnterPlanMode` to begin planning the implementation. In plan mode:
   - Read the spec (if one exists) and any relevant source files
   - Understand the current state of the codebase for the affected areas
   - Design the implementation approach
   - Present a step-by-step plan for user approval
