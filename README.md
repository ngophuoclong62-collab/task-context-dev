# Task Context Development

A reusable English skill for repository development that stays easy to resume.

**Specify → prepare focused source context → implement and checkpoint → reconcile on resume → verify acceptance.**

It works with existing project files and tools. It does not require RAG, a vector database, a separate model API, or a custom Agent engine. It does not register automatic compaction hooks or guarantee an efficiency percentage.

## What is included

- `SKILL.md`: the development workflow and recovery rules.
- `agents/openai.yaml`: Codex skill display metadata.
- `assets/`: task specification, source context, and checkpoint templates.
- `references/prompts.md`: copy-and-paste prompts for each operation.

## Use in a project

For Codex, place this repository's files inside `.agents/skills/task-context-dev/` in the target project. Start or refresh skill discovery as required by your client, then invoke:

```text
Use $task-context-dev to implement [the behavior you want].
```

For a planning-only task:

```text
Use $task-context-dev to prepare the specification and focused source context for [task].
Planning only; do not change business code yet.
```

For a new session:

```text
Use $task-context-dev to resume .ai/tasks/[task-slug]/.
```

An assistant that can read files can also use it explicitly:

```text
Read [path-to-this-skill]/SKILL.md and follow it for [task].
```

This fallback does not imply native skill discovery in every client. For native Codex installation details, see [Build skills](https://learn.chatgpt.com/docs/build-skills).

## Task records

Use the project's existing convention, or:

```text
.ai/tasks/<task-slug>/
├── task.md          Goal, scope, acceptance criteria, and plan
├── context.md       Relevant paths, interfaces, and essential excerpts
└── checkpoint.md    Progress, verification, decisions, and next action
```

Keep source authoritative. A fresh session reads the records, checks current files and working-tree changes, refreshes stale information, and continues. Stage checkpoints provide the baseline; no platform-specific automatic hook is installed.

Adapt this to C++/Qt, Python, web projects, or another repository. Do not overwrite existing project instructions, mix separate tasks, or report unexecuted checks as passed. Missing build environments should be recorded as unverified behavior, not simulated success.

## Design references

Original instructions and templates, informed by:

- [Repomix](https://github.com/yamadashy/repomix): task-focused file selection and source packaging.
- [handoff](https://github.com/ddaanet/handoff): persistent task handoffs across session boundaries.
- [OpenAI execution plans](https://developers.openai.com/cookbook/articles/codex_exec_plans): maintained progress and decision records.
- [GitHub Spec Kit](https://github.com/github/spec-kit): specifications that guide implementation and acceptance.

No source code from those projects is bundled. This repository contains only the general skill, templates, and prompts, without business source code or personal performance claims.
