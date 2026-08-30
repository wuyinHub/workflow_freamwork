# Tasks

This directory is the handoff layer between planning and implementation.

The key rule is that an unfinished idea is not automatically an executable task. `tasks/active/` contains only work that has been explicitly approved for Codex implementation.

## Workflow

1. Discuss requirements and alternatives in ChatGPT.
2. Record durable decisions in `docs/DECISIONS.md` only after they are approved.
3. Create a task from `TASK_TEMPLATE.md`.
4. Only after explicit human approval, place the task in `tasks/active/` and mark it Ready.
5. Manually tell Codex to execute the approved task, for example:

   `Execute tasks/active/T001-example.md according to AGENTS.md.`

6. Codex synchronizes safely with the latest remote `main`, works on a dedicated task branch, verifies the implementation, commits it, pushes the branch, and opens a Pull Request.
7. A human reviews the Pull Request. If revisions are required, Codex normally updates the same branch so the existing Pull Request updates automatically.
8. After the implementation is accepted and merged, perform task closeout.

## Task Lifecycle

Discussion and planning do not grant execution permission.

Typical lifecycle:

`Discussion -> Approved -> Ready/Active -> Implementation -> Verification -> Commit -> Push -> Pull Request -> Review -> Merge -> Closeout -> Completed`

Implementation, delivery, and closeout are separate milestones. A task is not fully completed merely because the code was written locally.

## Directory Meaning

### `tasks/active/`

Contains tasks that have been explicitly approved and may be executed by Codex.

It is not a backlog of every unfinished idea. Draft ideas and unapproved discussions should remain outside the executable task queue.

### `tasks/completed/`

Contains tasks whose implementation has been accepted, merged into the formal project state, and closed out.

Completed task files are durable project history, not disposable logs.

## Status Meaning

- **Draft**: still being discussed; Codex must not implement it.
- **Ready**: explicitly approved and available for implementation under `tasks/active/`.
- **In Progress**: currently being implemented or delivered.
- **Completed**: accepted, merged, and project-state closeout finished.

A task may also be locally implemented or verified while delivery is temporarily blocked. In that situation, preserve the completed local work and report the blocked delivery step rather than restarting implementation.

## Task Closeout

After an accepted Pull Request is merged:

1. Confirm the implementation is present on `main`.
2. Confirm the task acceptance criteria were satisfied based on the available review and verification evidence.
3. Move the task record from `tasks/active/` to `tasks/completed/`.
4. Set its status to `COMPLETED` and record the completion date.
5. Record useful delivery evidence such as the Pull Request and key verification results when appropriate.
6. Update `docs/PROJECT.md` so the current stage and priorities reflect the new project state.
7. Determine the next task or project phase separately; do not automatically expand scope.

The important safety rule remains simple: discussion does not automatically trigger implementation, and merge does not automatically replace project-state closeout. Human approval remains the execution gate.
