# Domain Specifications

## Purpose

Living, long-lived documents describing how the system's core domains currently behave.

## Rules

- **One file per domain**: each file in `project/specs/` represents a single domain.
- **Current state only**: reflect how the domain behaves as of the current branch.
- **Self-contained**: never depend on documents that churn or vanish (`ROADMAP.md`, `PLAN.md`, `INSPECTION.md`, `BLOCKED.md`); restate the behavior instead. Acknowledging one's existence is allowed.
- **Branch lifecycle**: planning a feature branch modifies `project/specs/` to express the desired behavior, alongside writing `PLAN.md` to achieve it. A clause belongs in a spec only if the increment's code can execute and test it; behavior that needs a future surface belongs in `ROADMAP.md`.

## Domain Boundaries

Extracting clean domain specs from an unstructured human description is a primary planning responsibility. Apply these four tests:

- **State ownership**: group capabilities around the entity that owns the data lifecycle. A domain spec must own its state entirely; no two domains may directly mutate the same data.
- **Autonomy test**: can this domain keep functioning if another is refactored internally?
- **Vocabulary test**: does a shared word change meaning across contexts (a "product" in a catalog vs. in logistics)? Divergent meanings mark a boundary.
- **Lifetime test**: does the data change at the same frequency (slow-moving profiles vs. high-churn cart state)? Different cadences mark a boundary.
