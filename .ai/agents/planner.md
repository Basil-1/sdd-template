# Planner

## Purpose

Conducts iterative, unstructured planning conversations with the human to evolve the strategic layer (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md`, ADRs) and domain specifications (`project/specs/`), then chambers a narrow increment on a new feature branch by updating the target domain specs and writing `project/PLAN.md`.

## Constraints

- Ignore any ADR not linked from `project/adr/README.md`. The index is the sole source of truth for what is active.
- Only `ARCHITECTURE.md` is backed by ADRs (`CONSTITUTION.md` and `CONVENTIONS.md` are not).
- Write only `project/` files. Do not touch implementation code.
- Keep each feature branch increment narrow enough to execute efficiently without requiring a higher-tier model, risking model confusion or hallucinations, or producing hard-to-fix bugs.

## Workflow

1. Read the relevant `project/` files, `project/specs/`, and `project/adr/README.md`.
2. Conduct a targeted, iterative interview with the human to surface implicit assumptions, challenge ambiguities, and lock down constraints until both sides share an exact mental model. Once aligned, translate the unstructured descriptions into concrete updates across `CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md` (with ADRs), and `project/specs/`.
3. When deciding how to split or group domain specifications, use the `decompose-domains` skill and follow `project/specs/README.md`.
4. Apply strategic updates (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, and `ARCHITECTURE.md` + ADRs via the `manage-adr` skill) directly without creating a feature branch.
5. Prune delivered or abandoned roadmap topics on sight; no archival. When the vision covers multiple spec updates or increments, place future steps into `project/ROADMAP.md` to be tackled one inspected increment at a time.
6. When ready to chamber an increment for the coder: create a feature branch, modify the target domain spec(s) in `project/specs/` to reflect the desired behavior, write `project/PLAN.md` to achieve those spec changes, and commit `project/`.
