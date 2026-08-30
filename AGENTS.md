# Agent Instructions

This repository uses a human-in-the-loop workflow:

ChatGPT -> GitHub project state -> human approval -> Codex implementation -> Pull Request -> human review -> merge.

## Before Starting Work

For every implementation task:

1. Read `docs/PROJECT.md` to understand the project goal and current context.
2. Read `docs/DECISIONS.md` to understand decisions that have already been made.
3. Read the requested task under `tasks/active/`.
4. Inspect the relevant existing code before editing.
5. If the task conflicts with an existing decision, stop and report the conflict instead of silently changing the decision.

## Implementation Rules

- Make the smallest reasonable change that satisfies the task.
- Follow the existing architecture and conventions of the project.
- Do not refactor unrelated code unless the task explicitly requires it.
- Do not silently introduce new dependencies, frameworks, services, or architectural patterns.
- Do not modify secrets, credentials, environment files, or production configuration unless explicitly requested.
- Preserve backwards compatibility unless the task explicitly says otherwise.

## Verification

Before declaring a task complete:

1. Run the relevant tests, checks, or build commands when available.
2. Review the final diff for accidental or unrelated changes.
3. Report which files were changed.
4. Report what verification was performed and whether it passed.
5. Clearly report any unresolved problem or assumption.

## Git Workflow

For normal implementation work:

- Do not implement feature tasks directly on `main`.
- Create or use a dedicated branch for the task.
- Prefer one task per branch and one task per Pull Request.
- Keep commits focused and understandable.
- Open a Pull Request for human review before merging into `main`.

## Project State

- `docs/PROJECT.md` describes what the project is.
- `docs/DECISIONS.md` records durable decisions.
- `tasks/active/` contains approved tasks ready for implementation.
- `tasks/completed/` contains finished task records.

Do not treat brainstorming or unapproved discussion as an implementation instruction. A task should only be implemented after it has been explicitly approved and placed in `tasks/active/`.
