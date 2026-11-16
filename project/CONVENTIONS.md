# Conventions

## Purpose

Tactical implementation guide: coding standards, directory structure, naming, and tool usage. Applies to all execution.

## Rules

- Add a convention only if it is enforceable and repeatable. Remove conventions that no longer apply.
- Nothing requires this file to stay whole: when its bulk would overburden agents working outside some domain (visual design is the classic case), that domain's conventions may move to a `CONVENTIONS-<DOMAIN>.md` file beside this one, routed by one line under `## Project Conventions`. A domain file binds exactly as this one does, but it is wholly project content: it carries no boundary line, and a graft never touches it.
- Cite a convention as `CONVENTIONS.md` (topic optional), never a `CONVENTIONS-<DOMAIN>.md` file; only the hub's routes name domain files, so a split touches no reference.
- No palimpsest accretion: after each edit a file reads as if written fresh, never referring to an earlier state. Git history is the archive.
- Every agent commit follows the `commit` skill: minimal narrative of durable value, plus attribution trailers naming the agent identity, harness, model, and — when the harness provides it — the human's initials. Nothing about machines, accounts, or environments.
- Feature branches reach the base branch only through the Reviewer's squash merge: one commit per increment, carrying the narrative and a `Branch:` trailer. Exactly one merged branch is retained for troubleshooting; older merged branches are deleted.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Conventions

<!-- Add project-specific conventions below. -->
