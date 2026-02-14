---
name: merge-workspace
description: Merge changes from a git worktree into the main branch for integration testing.
user-invocable: true
argument-hint: [worktree name, branch, or directory]
---

Merge completed work from a worktree into the main branch.

**This skill should be run from the main worktree** (on the `main` branch).

## Steps

1. **Verify we are on main** — run `git branch --show-current`.
   - If not on `main`, stop and tell the user this skill must be run from the main worktree.

2. **Discover worktrees** — run `git worktree list` to see all available worktrees and their checked-out branches.
   - Show the user the list of worktrees.

3. **Identify the target worktree** from `$ARGUMENTS`:
   - Match by worktree name, directory path, or branch name (case-insensitive).
   - If not provided or unclear, show the available worktrees and ask the user which one to merge from.

4. **Detect the worktree branch** — identify the branch currently checked out in the target worktree.
   - This may be a long-lived branch (e.g., `workspace-A`) or a task branch (e.g., `feat/something`).
   - Show the user which branch was detected.

5. **Preview the incoming changes** — show the user:
   - `git log --oneline main..<branch>` — commits that will be merged
   - `git diff --stat main..<branch>` — files affected
   - If there are no commits ahead of main, tell the user and stop (nothing to merge).

6. **Confirm with the user** — show the summary and ask for confirmation before merging.

7. **Merge into main** — use a regular merge (NOT squash) to preserve commit identity across worktrees:
   ```
   git merge <branch>
   ```
   - Regular merges keep original SHAs, which allows other workspaces to rebase cleanly without duplicate commits.
   - If the merge has conflicts, stop and inform the user. Do NOT force-resolve conflicts.

8. **Report the result** — show `git log --oneline -5` so the user can verify the merge landed correctly.
