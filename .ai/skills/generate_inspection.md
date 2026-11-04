# generate_inspection

## Purpose

Automates Phase 2 teardown when the Coder completes `PLAN.md`.

## Steps

1. Generate `INSPECTION.md` containing:
   - manual verification steps — a human testing protocol;
   - self-verification evidence — what ran and passed;
   - proposed `CHANGELOG.md` additions.
2. Delete `PLAN.md`.

## Rules

- `INSPECTION.md` is the only handover artifact. Keep it self-contained and truthful.
- Do not touch `.project/` while generating it.

## Triggers

- Coder declares `PLAN.md` complete.
