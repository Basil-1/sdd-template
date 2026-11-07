# Architecture Decision Records

## Purpose

Canonical index of all current ADRs. This index — not the individual ADR files — is the entry point for agents. Individual ADR files are excluded from default agent context.

## Index

| Status | ID | Title |
| --- | --- | --- |

## Authoring

1. Add `NNNN-title.md` under this directory; `NNNN` is the next unused number.
2. Record ADR.
3. Append one row to the index above.

## Superseding and Clarification

- Determine whether a modification supersedes an ADR or is only a clarification. A change affecting an architectural decision or system design constraint is generally a supersession, and small or cosmetic changes can be clarifications.
- Supersession: write a new ADR that links the old one and states it is replaced. In the index, remove the old ADR. In the old ADR file, add at the top `Superseded by NNNN-title`.
- Clarification: add an addendum to the existing ADR.

## Consistency

The `manage-adr` skill verifies this index stays consistent with the ADR files and with `ARCHITECTURE.md`.
