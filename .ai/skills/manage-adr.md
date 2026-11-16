---
name: manage-adr
description: Creates and supersedes ADRs, keeps the index and ARCHITECTURE.md in sync, and detects desync. Use for any ADR change or index check.
---

# manage-adr

## References

- Follow `project/adr/README.md` for authoring and superseding rules.

## Duties

1. **Create**: add a numbered ADR file and its index row. Update `ARCHITECTURE.md`.
2. **Supersede**: write the new ADR, link the old one, and update the index. Update `ARCHITECTURE.md`.
3. **Watch for desync**, then fix or report: index vs. ADR files, and index vs. `ARCHITECTURE.md`.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Customizations

<!-- Add project-specific customizations below. -->
