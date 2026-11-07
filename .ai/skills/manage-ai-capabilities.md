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
- OpenCode stubs may carry `permissions` front matter that mechanically enforces the write restrictions stated in the `.ai/` core file; keep it aligned when those restrictions change. Claude Code and Copilot stubs stay prose-only.
- When the set of agents or skills changes, refresh the matching stubs in every vendor folder.
- Skill identifiers use lowercase kebab-case everywhere: the `.ai/skills/` filename, the frontmatter `name`, the vendor skill directory, and each vendor stub's `name`. Use only `a-z`, `0-9`, and single hyphens, start and end with a letter or digit, and stay within 64 characters. This is the intersection accepted by Claude Code, GitHub Copilot, and OpenCode, so one identifier works in every harness.

## Duties

1. Add, rename, or remove a `.ai/agents/*.md` or `.ai/skills/*.md` → mirror the change in all three vendor folders.
2. Verify each vendor stub points to the correct core file, carries that harness's required front matter, and uses the same lowercase kebab-case identifier as the core file.
3. Keep each vendor stub's front matter aligned with its `.ai/` source. Skills copy `name` and `description` from the core front matter. Agents carry no core front matter, so keep the stub's one-line `description` aligned in substance with the core file's Purpose. Let only harness-required fields, such as OpenCode `permissions`, differ.
