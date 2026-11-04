# manage_ai_capabilities

## Purpose

Enforces the DRY AI architecture: `.ai/` is the single source of truth; vendor folders hold only routing stubs.

## Rules

- Agent and skill behavior is defined only under `.ai/`. No logic is duplicated into `.claude/`, `.github/`, or `.opencode/`.
- Change the `.ai/` file, never the vendor stub, when behavior changes.
- When the set of agents or skills changes, refresh the matching stubs in every vendor folder.

## Duties

1. Add, rename, or remove a `.ai/agents/*.md` or `.ai/skills/*.md` → mirror the change in all three vendor folders.
2. Verify each vendor stub points to the correct core file and carries that harness's required front matter.

## Triggers

- Any change to the set of `.ai/` capabilities.
