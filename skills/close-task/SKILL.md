---
name: close-task
description: Mark a task as completed in the project's task plan and commit the change.
user-invocable: true
argument-hint: [task description to mark as done]
---

Mark a task as completed in the project's task plan.

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

1. **Read the task plan** file found above.

2. **Find the matching task** — search for an unchecked line (`- [ ]`) that best matches: `$ARGUMENTS`
   - Match by substring or fuzzy relevance. If multiple lines could match, show the candidates and ask the user to pick one.
   - If no match is found, tell the user and stop.

3. **Mark the task as done** — change `- [ ]` to `- [x]` on the matched line.
   - If the task has sub-tasks (indented `- [ ]` lines directly beneath it), mark those as done too.

4. **Show the change** to the user for confirmation before committing.

5. **Commit** the task plan file with the message format:
   ```
   plan: complete "<short task description>"
   ```
   Only commit the task plan file — do not stage other files.
