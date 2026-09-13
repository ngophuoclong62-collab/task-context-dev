# Reusable Task Development Prompts

Replace bracketed task details with the real request. These are user-facing prompts, not commands that automatically register hooks or permissions. Select the operation you need; do not load every prompt on every task.

## 1. Start a task

```text
Use $task-context-dev for this task: [describe the requested behavior].
Use the project's existing task-record convention, or create .ai/tasks/[task-slug]/.
Record the goal, modification boundaries, constraints, acceptance criteria, and a short plan in task.md.
Locate the actual source entry points and prepare focused context before implementation.
Continue through the authorized implementation and verification; if I explicitly requested planning only, stop after the plan and checkpoint.
Distinguish completed implementation from checks actually performed.
```

## 2. Prepare focused source context

```text
Prepare source context for [task-record directory] using its task.md.
Confirm the relevant entry points, interfaces, and dependencies before selecting files.
Write a compact context.md with repository-relative paths, file roles, and essential source excerpts with original line ranges.
Include configuration, build, UI, styles, and resources only where the task needs them.
Exclude unrelated generated files, build outputs, binaries, and verbose logs.
Keep large implementations available for on-demand reading and identify missing evidence.
Read current source before editing; saved excerpts may become stale.
```

## 3. Develop from the specification

```text
Use $task-context-dev to implement the task in [task-record directory].
Read the specification, relevant context, and any existing checkpoint.
Confirm current source and pre-existing work before editing.
Implement the authorized behavior within the recorded boundaries using project conventions.
Run checks appropriate to the change and available environment.
Update the checkpoint at meaningful stages and report unverified behavior explicitly.
```

## 4. Save a checkpoint or handoff

```text
Use $task-context-dev to save a checkpoint for [task-record directory].
Update checkpoint.md with completed and remaining work, actual changed files, verification commands and results, unverified behavior, important decisions, and failed attempts with reasons.
Separate this task's changes from pre-existing work.
Retain useful source and log paths instead of copying large code blocks or the conversation.
Record one concrete next action and stop at this handoff boundary.
```

## 5. Resume after interruption or compaction

```text
Use $task-context-dev to resume [task-record directory].
Read the applicable project instructions, task.md, checkpoint.md, and relevant context.md sections.
Check the current working directory, source files, and relevant working-tree changes.
Reconcile stale excerpts, interrupted edits, external changes, and earlier verification results against current evidence.
Refresh the records without reverting newer work.
Briefly confirm the goal, allowed scope, completed work, unverified items, and next action; then continue the authorized task.
```

## 6. Verify acceptance and close

```text
Use $task-context-dev to review acceptance for [task-record directory].
Compare each criterion in task.md with the current implementation and actual verification evidence.
Run appropriate available checks and review the final changes, including new files.
Mark each criterion verified, failed, or not verified; explain concrete gaps.
Update checkpoint.md and report what changed, what was verified, what remains, and the record paths.
Do not present unavailable-platform checks, mocks, or estimates as measured production results.
```

## 7. Improve a task prompt after a demonstrated failure

```text
Improve this task prompt: [current prompt].
Observed failure: [incorrect location, scope expansion, unsupported completion claim, repeated exploration, or other actual failure].
Preserve the user's intended behavior and existing authorization.
Add only the missing goal, scope, evidence requirement, acceptance criterion, or output distinction that addresses the failure.
Return a concise reusable prompt and suggest an observable comparison on equivalent tasks.
Do not add unrelated process requirements or claim unmeasured improvements.
```
