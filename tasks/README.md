# Tasks

This directory is the handoff layer between planning and implementation.

## Workflow

1. Discuss requirements and alternatives in ChatGPT.
2. Record durable decisions in `docs/DECISIONS.md` when they are approved.
3. Create a task from `TASK_TEMPLATE.md`.
4. Only after human approval, place the task in `tasks/active/`.
5. Manually tell Codex to execute the approved task, for example:

   `Execute tasks/active/T001-example.md according to AGENTS.md.`

6. Codex implements the task on a dedicated branch, verifies the work, and opens a Pull Request.
7. A human reviews the Pull Request.
8. After the work is accepted and merged, move the task record to `tasks/completed/`.

## Status Meaning

- Draft: still being discussed; Codex must not implement it.
- Ready: explicitly approved for implementation.
- In Progress: currently being implemented.
- Done: implementation was accepted and merged.

The important safety rule is simple: discussion does not automatically trigger implementation. Human approval remains the final execution gate.
