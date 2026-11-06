---
name: manage-adr
description: Creates, supersedes, and compacts Architecture Decision Records (ADRs), keeps the ADR index current, and detects desync between ADRs and strategy files. Use when recording or changing an architectural or technical decision, adding or updating an ADR, superseding an old decision, compacting a supersession chain, or checking that the ADR index matches ARCHITECTURE.md, CONVENTIONS.md, and CONSTITUTION.md.
---

# manage-adr

## Purpose

Automates ADR creation, supersession, and chain compaction, and keeps the records consistent.

## References

- Follow `project/adr/README.md` for authoring, superseding, and compaction rules.

## Duties

1. **Create**: add a numbered ADR file and its index row.
2. **Supersede**: write the new ADR, link the old one, and update index statuses.
3. **Compact**: when a supersession chain exceeds 3 ADRs, squash the lessons into the newest and archive the older ones.
4. **Watch for desync**, then fix or report:
   - index vs. ADR files;
   - compaction opportunities (chains over 3);
   - index vs. `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
