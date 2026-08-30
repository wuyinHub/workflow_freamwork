# workflow_freamwork

AI-assisted development workflow template for a human-in-the-loop ChatGPT + GitHub + Codex development process.

## Core Model

- **ChatGPT** plans, researches, helps make decisions, reviews work, and maintains approved project state.
- **GitHub** is the durable shared state between planning and implementation.
- **Codex** implements explicitly approved tasks.
- **Human approval** remains the gate between planning, execution, and acceptance.

The intended flow is:

`ChatGPT planning -> human approval -> GitHub project state -> manual Codex trigger -> task branch -> implementation and verification -> push -> Pull Request -> human review -> merge -> project-state closeout`

## Repository State

- `AGENTS.md` defines how Codex should work in the repository.
- `docs/PROJECT.md` describes the project purpose, scope, stack, current stage, and priorities.
- `docs/DECISIONS.md` records durable approved decisions and their history.
- `tasks/active/` contains explicitly approved executable tasks.
- `tasks/completed/` contains accepted and closed-out task records.
- `tasks/TASK_TEMPLATE.md` defines the standard task contract.
- `.agents/skills/` is available for reusable skills when a real repeated need appears.
- `.codex/config.toml` is available for project-level Codex configuration without forcing personal model settings into the template.

## Approval Rule

Discussion is not execution permission.

Planning and brainstorming may happen freely, but a task should only become executable after explicit human approval and placement in `tasks/active/`.

## Change Boundaries

After explicit human approval, planning/project-state changes such as `docs/PROJECT.md`, `docs/DECISIONS.md`, and `tasks/` may be maintained directly on `main` by the planning layer.

Product implementation should normally be performed by Codex on a dedicated task branch and delivered through a Pull Request before entering `main`.

## Delivery and Closeout

Implementation success, delivery success, and project-state completion are different milestones.

A task may be implemented and verified locally while push or Pull Request creation is blocked. In that case, preserve the valid work and retry the failed delivery step rather than redoing the implementation.

After a Pull Request is accepted and merged, complete project-state closeout by moving the task from `tasks/active/` to `tasks/completed/` and updating `docs/PROJECT.md` as appropriate.

## Design Principle

Keep the workflow minimal and expandable. Do not add frameworks, automation, MCP servers, hooks, skills, CI systems, or other machinery merely because they are available. Add them when repeated project needs justify the additional complexity.
