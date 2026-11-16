# Domain Specifications

## Purpose

Living, long-lived documents describing how the system's core domains currently behave.

## Rules

- **One file per domain**: each file in `project/specs/` represents a single domain.
- **Current state only**: reflect how the domain behaves as of the current branch.
- **Branch lifecycle**: planning a feature branch modifies `project/specs/` to express the desired behavior, alongside writing `PLAN.md` to achieve it.
- **Right-sized deltas**: keep a branch's spec changes narrow enough to implement and verify reliably in one increment. Later spec changes go in `ROADMAP.md`, one inspected increment at a time.

## Domain Boundaries

Extracting clean domain specs from an unstructured human description is a primary planning responsibility. Apply these four tests:

- **State ownership**: group capabilities around the entity that owns the data lifecycle. A domain spec must own its state entirely; no two domains may directly mutate the same data.
- **Autonomy test**: can this domain keep functioning if another is refactored internally?
- **Vocabulary test**: does a shared word change meaning across contexts (a "product" in a catalog vs. in logistics)? Divergent meanings mark a boundary.
- **Lifetime test**: does the data change at the same frequency (slow-moving profiles vs. high-churn cart state)? Different cadences mark a boundary.
