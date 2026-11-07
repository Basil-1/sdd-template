---
name: decompose-domains
description: Separates unstructured requirements or tangled system descriptions into clean, autonomous domain boundaries for project/specs/. Use when deciding how to split or group domains, evaluating whether a concept belongs in an existing domain or a new one, or resolving shared-state and vocabulary tangles during planning or send-back re-planning.
---

# decompose-domains

## Purpose

Translates disorganized human descriptions into bounded, independent domain specifications under `project/specs/` so domains own their state cleanly and parallel branches on separate domains do not collide.

## References

- Follow `project/specs/README.md` for domain specification rules and boundary tests.

## Duties

1. **Extract entities and state lifecycles**: Identify the core data entities, who creates/mutates/deletes them, and the capabilities being described by the human.
2. **Apply the four boundary tests**:
   - **State ownership**: Group capabilities around the entity that owns the data lifecycle. Ensure each domain owns its state entirely and no two domains directly mutate the same data.
   - **Autonomy test**: Verify a domain can continue to function if another domain is refactored internally.
   - **Vocabulary test**: Check whether a shared term changes meaning across contexts (e.g., a catalog "product" vs. a logistics "product"); split domains where vocabulary diverges.
   - **Lifetime test**: Check whether data changes at different frequencies (e.g., user profile data vs. cart state); split domains where update cadences diverge.
3. **Right-size the active increment**: When a decomposition spans more domain changes than can be executed reliably in a single narrow branch increment, isolate the immediate slice for the current branch and record the remaining domain work in `project/ROADMAP.md`.
