---
name: architect
description: Start an architectural discussion about a feature or problem. Use when planning features, evaluating solutions, or designing system interactions.
user-invocable: true
argument-hint: [feature or problem description]
---

Start an architectural discussion about: $ARGUMENTS

Use the architect subagent. Begin by:

1. **Understanding the current relevant systems** (read code if needed)
   - Look at related components across the codebase
   - Read project documentation (CLAUDE.md, README, docs/) for architectural context and constraints

2. **Ask clarifying questions** about requirements and constraints
   - What are the success criteria?
   - What are the failure modes?
   - How does this interact with existing systems?

3. **Do NOT propose solutions** until the problem is well-understood

This is a dialogue, not a one-shot answer. We explore the problem space together before designing.

When ready to formalize, create a spec in `docs/specs/` (or wherever the project keeps specifications).
