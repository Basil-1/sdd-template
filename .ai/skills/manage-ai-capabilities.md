---
name: manage-ai-capabilities
description: Maintains the DRY AI capability layer: keeps .ai/ as the single source of truth and mirrors agent and skill changes into the .claude/, .github/, and .opencode/ routing stubs. Use when adding, renaming, removing, or editing AI agents or skills, updating vendor harness stubs or their front matter, or checking for drift between .ai/ and the vendor folders.
---

# manage-ai-capabilities

## Purpose

Enforces the DRY AI architecture: `.ai/` is the single source of truth; vendor folders hold only routing stubs.

## Rules

- Agent and skill behavior is defined only under `.ai/`. No logic is duplicated into `.claude/`, `.github/`, or `.opencode/`.
- Change the `.ai/` file, never the vendor stub, when behavior changes.
- When the set of agents or skills changes, refresh the matching stubs in every vendor folder.
- Skill identifiers use lowercase kebab-case everywhere: the `.ai/skills/` filename, the frontmatter `name`, the vendor skill directory, and each vendor stub's `name`. Use only `a-z`, `0-9`, and single hyphens, start and end with a letter or digit, and stay within 64 characters. This is the intersection accepted by Claude Code, GitHub Copilot, and OpenCode, so one identifier works in every harness.

## Duties

1. Add, rename, or remove a `.ai/agents/*.md` or `.ai/skills/*.md` → mirror the change in all three vendor folders.
2. Verify each vendor stub points to the correct core file, carries that harness's required front matter, and uses the same lowercase kebab-case identifier as the core file.
3. Keep each vendor stub's front matter in sync with its `.ai/` source: copy `name`, `description`, and other portable fields from the core file, and let only harness-required fields differ.
