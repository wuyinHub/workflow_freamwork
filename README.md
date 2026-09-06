# workflow_freamwork

AI-assisted development workflow template for a human-in-the-loop ChatGPT + GitHub + Codex development process.

## Core Model

- **ChatGPT** plans, researches, helps make decisions, reviews work, and maintains approved project state.
- **GitHub** is the durable shared state between planning and implementation.
- **Codex** implements explicitly approved tasks.
- **Human approval** remains the gate between planning, execution, and acceptance.

The intended flow is:

`ChatGPT planning -> human approval -> GitHub project state -> Codex -> task branch -> implementation and verification -> Pull Request -> human review -> merge -> project-state closeout`

## Everyday Prompts

Most work can use these four prompts:

```text
规划 Txxx，先不要写入项目。

确认 Txxx，写入项目。

按照 AGENTS.md 执行 Txxx，交付 PR。

检查 Txxx 的 PR 和验收证据，无阻塞问题后合并并收尾。
```

To resume interrupted work:

```text
继续 Txxx。先核对已有分支、提交和 PR，从未完成的步骤恢复。
```

The final review prompt authorizes merge and closeout only when review finds no blocking problem. If a check is unavailable or evidence is insufficient, report the gap instead of treating it as passed.

## Repository State

- `AGENTS.md` defines how Codex should work in the repository.
- `docs/PROJECT.md` describes the project, scope, stack, current stage, priorities, and working commands.
- `docs/DECISIONS.md` records durable approved decisions and their history.
- `tasks/active/` contains explicitly approved executable tasks.
- `tasks/completed/` contains accepted and closed-out task records.
- `tasks/TASK_TEMPLATE.md` defines the standard task contract and evidence record.
- `.agents/skills/` is available when a repeated project workflow justifies a reusable skill.
- `.codex/config.toml` is available for project-level configuration without forcing personal model settings into the template.

## Approval Rule

Discussion is not execution permission. A task becomes executable only after explicit human approval and placement in `tasks/active/` with status `READY`.

## Change Boundaries

After explicit approval, planning and project-state changes may be maintained directly on `main`. Product implementation should normally use a dedicated task branch and Pull Request.

## Delivery and Closeout

Implementation success, delivery success, and project-state completion are different milestones. If delivery is interrupted, preserve valid work and continue from the failed step.

After a Pull Request is accepted and merged, move the task from `tasks/active/` to `tasks/completed/`, record the evidence, and update `docs/PROJECT.md` as appropriate. A single explicit instruction to “merge and close out” may authorize both actions.

## Design Principle

Keep the workflow minimal and expandable. Add automation, CI, hooks, integrations, or skills only when a repeated project need justifies them.

