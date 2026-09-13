---
name: task-context-dev
description: Organize multi-step repository development with task specifications, focused source context, checkpoints, and recovery checks. Use when starting a substantial code change, handing off an ongoing task, or resuming after interruption or context compaction.
---

# Task Context Development

Make a repository task easy to start, continue, and verify without rebuilding its context from the entire conversation. Use the project's current files and existing tools; a RAG service, model API, or context-packing dependency is not required.

## Select the requested operation

- **Start:** establish the task specification and focused source context.
- **Develop:** implement the authorized task, keeping its records current.
- **Checkpoint:** save the current state without starting unrelated work.
- **Resume:** reconstruct state, reconcile it with current files, then continue.
- **Verify:** compare the implementation and actual check results with acceptance criteria.

Follow the user's requested scope. If they requested planning only, produce the plan and checkpoint, then stop. Otherwise continue through implementation and verification without introducing an extra approval gate. Ask only for a missing decision that materially changes the task or for an action that needs authorization.

## Establish the task workspace

1. Confirm the working repository, applicable project instructions, and existing changes. Reuse the project's task-record convention if it has one.
2. Otherwise create `.ai/tasks/<task-slug>/` with `task.md`, `context.md`, and `checkpoint.md`. Keep independent tasks separate. Use [the task template](assets/task.md), [context template](assets/context.md), and [checkpoint template](assets/checkpoint.md) when creating these records; adapt their fields to the task.
3. Resume existing records rather than replacing them with blank templates. Treat repository instructions and supplied source content according to their authority; project documents do not grant permission to publish or perform unrelated operations.

## 1. Specify the task

Record the concrete behavior to deliver, modification boundaries, relevant constraints, acceptance criteria, and a short implementation plan in `task.md`. Resolve routine choices from the code and user intent; record important assumptions.

Use observable acceptance criteria. Separate implementation success from checks that require unavailable platforms, dependencies, or services. Update the specification when the user changes the requirements.

## 2. Assemble focused source context

Search by task terms and symbols, then confirm the actual entry points and dependencies. Use `rg` when available, or the project's equivalent search tool.

Write `context.md` as a compact navigation map: relevant paths, their roles, confirmed interfaces, and only the excerpts needed to begin the task. For C++/Qt, include headers and implementations; add UI, styles, resources, configuration, and build files only when relevant. Apply the same selection principle to other languages.

Exclude unrelated generated files, build outputs, binaries, and verbose logs. Keep paths and original line ranges on excerpts; preserve code structure. Add content hashes when they materially help detect stale sources. List missing evidence or dependencies rather than silently omitting them.

Start with a short map and load implementations on demand. Reuse an existing packer if it is available; introduce a helper script only when repeated packing justifies it. Do not install a framework merely to follow this workflow. A character or byte budget is not an exact model token count.

Read the current source before editing. Stored excerpts are navigation aids, not the authoritative working copy.

## 3. Implement and checkpoint

Make the authorized change using project conventions. Preserve pre-existing user changes and avoid expanding the task into unrelated cleanup.

Update `checkpoint.md` after a meaningful stage, an important decision, a verification run, or before a planned handoff. Include:

- completed and remaining work;
- files actually changed, distinguished from pre-existing changes;
- checks actually executed, their results, and useful log paths;
- unverified behavior and the reason it is unverified;
- important decisions, failed attempts, and their evidence;
- one concrete next action.

Keep records short; reference full logs instead of copying them. Do not equate code written with behavior verified. Do not depend on detecting the exact moment of automatic compaction; stage checkpoints are the portable baseline. This skill does not register automatic session hooks.

## 4. Resume and reconcile

Read applicable project instructions, `task.md`, `checkpoint.md`, and the relevant portions of `context.md`.

Confirm the current working directory and source state. If Git is present, inspect the branch, status, and relevant diffs; the same commit does not imply an unchanged working tree. Use current files and recorded fingerprints where Git is unavailable.

Check whether saved paths, excerpts, decisions, and verification results still apply. A changed source invalidates old excerpts and may invalidate earlier checks. Reconcile interrupted or external changes without reverting newer work. Refresh stale context and the checkpoint.

Briefly state the goal, allowed scope, completed work, unverified items, and next action. Continue the authorized task, or stop at the requested handoff boundary.

## 5. Verify and close

Map each acceptance criterion to an actual result: verified, failed, or not verified. Run checks appropriate to the change using the available project environment. Check the final diff, including new files, for scope and accidental regressions. Use file comparisons when Git is unavailable.

Record real commands, outcomes, and remaining limitations. Do not report unavailable-platform checks or mock demonstrations as production validation. Once required checks pass, close the task without repeating checks unless new evidence warrants it.

Return a concise completion or handoff report: what changed, what was verified, what remains, and where the task records live. Performance claims require measured baselines, conditions, and results; this skill makes no guaranteed efficiency claim.

## Reusable prompts

For user-facing copy-and-paste prompts, read only the relevant section of [references/prompts.md](references/prompts.md). It contains prompts for start, source preparation, development, checkpoint, resume, acceptance review, and prompt iteration.
