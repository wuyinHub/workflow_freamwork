# Tasks

This directory is the handoff layer between planning and implementation. `tasks/active/` contains only work explicitly approved for Codex implementation.

## Workflow

1. Discuss requirements and alternatives.
2. Record approved durable decisions in `docs/DECISIONS.md`.
3. Draft a task from `TASK_TEMPLATE.md`.
4. After explicit approval, place it in `tasks/active/` with status `READY`.
5. Tell Codex to execute the task according to `AGENTS.md`.
6. Codex works on a dedicated branch, verifies the result, records evidence, pushes, and opens a Pull Request.
7. A human reviews the diff and evidence. Revisions normally continue on the same branch and Pull Request.
8. After explicit authorization, merge and close out the task. These may be requested together.

## Task Lifecycle

Use these status values consistently:

- `DRAFT`: still being discussed and not executable.
- `READY`: explicitly approved and available under `tasks/active/`.
- `IN_PROGRESS`: implementation or delivery is underway.
- `IN_REVIEW`: a Pull Request is ready for human review.
- `COMPLETED`: accepted, merged, and closed out under `tasks/completed/`.

If work is blocked, keep the current lifecycle status and record the blocked step, cause, and recovery action. Do not invent an additional status that hides how far the task progressed.

## Directory Meaning

### `tasks/active/`

Contains approved work in `READY`, `IN_PROGRESS`, or `IN_REVIEW`. Draft ideas stay outside this executable queue.

### `tasks/completed/`

Contains accepted, merged, and closed-out tasks. These files are concise project history rather than disposable logs.

## Continuation and Recovery

When continuing a task, inspect its existing branch, commits, working tree, and Pull Request before acting. Reuse them when safe. If only push or Pull Request creation failed, retry that delivery step without reimplementing the task.

## Evidence

Before review, record:

- the commit that was verified;
- automated commands and their results;
- material manual or visual checks;
- checks that were unavailable or not run;
- the Pull Request link when available.

Identify whether evidence came from local Codex execution, CI, or reviewer inspection. Evidence supports acceptance; it does not replace review of the actual diff.

## Task Closeout

After an accepted Pull Request is merged:

1. Confirm the implementation is present on `main`.
2. Confirm acceptance criteria using the diff and available evidence.
3. Move the task from `tasks/active/` to `tasks/completed/`.
4. Set status to `COMPLETED` and record the completion date.
5. Record the Pull Request, merge commit, and useful verification evidence.
6. Update `docs/PROJECT.md` when the stage, priorities, or working commands changed.
7. Determine the next task separately; do not expand scope automatically.

If merge succeeds but closeout fails, preserve the merge and resume only the closeout.

