# Architecture Decision Records

## Purpose

Canonical index of all current ADRs. This index — not the individual ADR files — is the entry point for agents. Individual ADR files are excluded from default agent context.

## Authoring

1. Add `NNNN-title.md` under this directory; `NNNN` is the next unused number.
2. Record the ADR.
3. Append one row to the `## Index` table at the end of this file.

## Superseding and Clarification

- A change affecting an architectural decision or system design constraint is generally a supersession; small or cosmetic changes can be clarifications.
- Supersession: write a new ADR that links the old one and states it is replaced. Remove the old ADR from the index, and add `Superseded by NNNN-title` at the top of the old ADR file.
- Clarification: add an addendum to the existing ADR.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Index

<!-- Maintain one row per active ADR below. -->

| ID | Title |
| --- | --- |
