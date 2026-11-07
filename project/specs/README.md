# Domain Specifications

## Purpose

Living, long-lived documents that describe how the system's core domains currently behave.

## Rules

- **One file per domain**: Each file in `project/specs/` represents a single domain. 
- **Current state only**: Reflect how the domain behaves as of the current branch. No palimpsest accretion: after each edit a file reads as if written fresh, never referring to an earlier state. Git history is the archive.
- **Branch lifecycle**: When chambering an increment on a feature branch, planning directly modifies `project/specs/` to express the desired behavior alongside writing `project/PLAN.md` to achieve it.
- **Right-sized deltas**: Keep the spec changes on a single feature branch narrow enough to be implemented and verified reliably in one increment. Place subsequent spec changes in `project/ROADMAP.md` and execute them one inspected increment at a time.

## Domain Boundaries

Extracting clean domain specs from an unstructured human description is a primary planning responsibility. Use the `decompose-domains` skill and apply these four boundary tests:

- **State ownership**: Group capabilities around the entity that owns the data lifecycle. A domain spec must own its state entirely; no two domains may directly mutate the same data.
- **Autonomy test**: Can this domain continue to function if another domain is refactored internally?
- **Vocabulary test**: Does a shared word change meaning across contexts (for example, a "product" in a catalog vs. a "product" in logistics)? A shared term with divergent meanings marks a domain boundary.
- **Lifetime test**: Does the data change at the same frequency (for example, slow-moving user profile data vs. high-churn cart state)? Different update cadences mark a domain boundary.
