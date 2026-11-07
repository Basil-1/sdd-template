---
name: manage-adr
description: Creates and supersedes Architecture Decision Records (ADRs), keeps the ADR index and ARCHITECTURE.md current, and detects desync between ADRs and ARCHITECTURE.md. Use when recording or changing an architectural decision, adding or updating an ADR, superseding an old decision, or checking that the ADR index matches ARCHITECTURE.md.
---

# manage-adr

## Purpose

Automates ADR creation and supersession, and keeps the records consistent.

## References

- Follow `project/adr/README.md` for authoring and superseding rules.

## Duties

1. **Create**: add a numbered ADR file and its index row. Update `project/ARCHITECTURE.md`.
2. **Supersede**: write the new ADR, link the old one, and update the index. Update `project/ARCHITECTURE.md`.
3. **Watch for desync**, then fix or report:
   - index vs. ADR files;
   - index vs. `ARCHITECTURE.md`.
