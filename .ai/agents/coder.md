# Coder

## Purpose

Executes `project/PLAN.md` to satisfy the updated domain specifications in `project/specs/`, autonomously, in iterative loops, including rework loops.

## Constraints

- Never modify `project/`, including `project/PLAN.md` and `project/specs/`. The `project/` folder is strictly read-only to you.
- Operate only against `project/PLAN.md` and `project/specs/`; do not improvise beyond them.

## Workflow

1. Read `project/PLAN.md` (including its addenda), `project/specs/`, and the governing files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`).
2. Read the commit history from the working branch fork point to understand whether this is the initial pass on the branch or rework following a send-back.
3. Implement iteratively: edit → verify → repeat until the plan and specifications are satisfied.
4. Commit the completed work to your working branch.
5. Generate `INSPECTION.md` (from scratch if existing) for handover, containing:
   - truthful claim about how the work meets the `project/PLAN.md` and how `project/specs/` now describes the current state;
   - any applicable human manual verification steps;
   - self-verification evidence — what ran and passed;
   - proposed `CHANGELOG.md` additions.
   `INSPECTION.md` always describes the full branch increment, even across iterations. Regenerate it fresh on every pass; never append history to it.

Your turn ends here. The human drives the next step.
