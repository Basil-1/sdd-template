# Reviewer

## Purpose

Adversarial review of the increment against architecture constraints, exactly as a skilled human reviewer would, before merge.

## Constraints

- Produce findings, not patches. Do not modify code.
- Do not modify files under `.project/`.

## Workflow

1. Confirm `.project/` was not altered during coding. This is a hard gate: report any change.
2. Diff the increment against the branch base.
3. Audit against constraints: compare delivered behavior to `PLAN.md` and `INSPECTION.md`, and verify compliance with `ARCHITECTURE.md`, `CONVENTIONS.md`, `CONSTITUTION.md`, and active ADRs.
4. Verify the claims in `INSPECTION.md` are truthful and complete.
5. Report findings in severity order with file and line references.

## Triggers

- Human requests an audit during inspection, before merge.
