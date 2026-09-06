# Agent Instructions

This repository uses a human-in-the-loop workflow:

ChatGPT -> GitHub project state -> human approval -> Codex implementation -> Pull Request -> human review -> merge -> project-state closeout.

## Communication Language

- Communicate with the user in Simplified Chinese by default.
- Model-generated explanations, progress updates, questions, warnings, approval reasons, and final reports must use Simplified Chinese.
- Keep code, commands, file paths, API names, technical identifiers, and original error messages in their original form when appropriate.

## Before Starting Work

First determine whether this is a new task, continuation, or delivery recovery.

### New task

1. Check the working tree and confirm the local repository can be synchronized safely.
2. Fetch the remote and base the task branch on the latest `origin/main`.
3. Do not overwrite uncommitted work or force conflict resolution. Report any unsafe synchronization problem.

### Continuing an existing task

1. Inspect the current branch, working tree, commits, and existing Pull Request before changing anything.
2. Continue the existing task branch and Pull Request. Do not restart completed work or create a replacement branch merely because the session changed.
3. Integrate the latest `origin/main` only when the task depends on it or a conflict must be resolved safely.

### Recovering delivery

If implementation or verification already succeeded and commit, push, or Pull Request creation failed, preserve the existing work and resume from the failed delivery step. Do not edit product code unless new evidence requires a correction.

For all modes:

1. Read `docs/PROJECT.md`, `docs/DECISIONS.md`, and the requested task under `tasks/active/`.
2. Inspect the relevant existing code before editing.
3. If the task conflicts with an active project decision, report the conflict before implementation continues.

## Implementation Rules

- Make the smallest reasonable change that satisfies the task.
- Follow the existing architecture and conventions of the project.
- Do not refactor unrelated code unless the task explicitly requires it.
- Do not silently introduce new dependencies, frameworks, services, or architectural patterns.
- Do not modify secrets, credentials, environment files, or production configuration unless explicitly requested.
- Preserve backwards compatibility unless the task explicitly says otherwise.

## Verification and Evidence

Before reporting implementation as ready for delivery:

1. Run the relevant tests, checks, or build commands when available.
2. Review the final diff for accidental or unrelated changes.
3. Record evidence in the task or Pull Request: the verified commit, commands or checks and results, material manual checks, and anything not verified.
4. Identify the source of evidence when it matters, such as Codex-reported local checks, reviewer inspection, or CI.
5. For visual changes, include screenshots or equivalent visual evidence when useful and practical.
6. Report changed files and any unresolved problem or assumption.

Do not mark an acceptance criterion complete without supporting evidence. An unavailable check must be reported as not verified rather than treated as passed.

## Delivery Status

Implementation, verification, commit, push, Pull Request, review, merge, and closeout are separate milestones. Report only the milestones relevant to the current state.

If a delivery step fails, identify the failed step and the exact recovery action. Network, authentication, Git, push, or Pull Request failures do not invalidate completed implementation work.

## Git Workflow

For normal implementation work:

- Do not implement feature tasks directly on `main`.
- Create or use a dedicated branch for the task.
- Prefer one task per branch and one task per Pull Request.
- Keep commits focused and understandable.
- Push the task branch and open a Pull Request for human review before merging into `main`.
- Do not merge the Pull Request yourself unless the user explicitly authorizes it.
- If a Pull Request needs revision, update the same task branch and Pull Request when practical.

## Project State

- `docs/PROJECT.md` describes the project, its current stage, and the commands needed to work with it.
- `docs/DECISIONS.md` records durable approved decisions.
- `tasks/active/` contains explicitly approved tasks ready for or undergoing implementation.
- `tasks/completed/` contains accepted and closed-out task records.

Do not treat brainstorming or unapproved discussion as an implementation instruction. A task may be implemented only after explicit approval and placement in `tasks/active/`.

After explicit approval, planning and project-state files may be maintained directly on `main`. Product implementation should normally use a task branch and Pull Request.

After an accepted Pull Request is merged, close out the task by moving its record from `tasks/active/` to `tasks/completed/`, recording delivery evidence, and updating `docs/PROJECT.md` when appropriate. When the user authorizes “merge and close out,” perform both parts of this sequence; if closeout fails, preserve the merge and resume only the closeout.

