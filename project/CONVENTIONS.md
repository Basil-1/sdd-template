# Conventions

## Purpose

Tactical implementation guide: coding standards, directory structure, naming, and tool usage. Applies to all execution.

## Rules

- Add a convention only if it is enforceable and repeatable. Remove conventions that no longer apply.
- A domain's conventions may split into a `CONVENTIONS-<DOMAIN>.md` file beside this one when its bulk would overburden agents working elsewhere (visual design is the classic case). Route it with one line under `## Project Conventions`. Such a file binds fully but is wholly project content: no boundary line, never grafted.
- Cite a convention as `CONVENTIONS.md` (topic optional), never a `CONVENTIONS-<DOMAIN>.md` file; only the hub's routes name domain files, so a split touches no reference.
- Every agent commit follows the `commit` skill.
- Feature branches reach the base branch only through the Reviewer's squash merge, one commit per increment with a `Branch:` trailer, retaining exactly one merged branch for troubleshooting.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Conventions

<!-- Add project-specific conventions below. -->
