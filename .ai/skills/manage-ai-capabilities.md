---
name: manage-ai-capabilities
description: Maintains the project's DRY AI capability layer. Agent and skill behavior lives in .ai/ as the single source of truth, mirrored into the .claude/, .github/, and .opencode/ routing stubs; the project tailors roles only below each file's boundary line, which a graft preserves while replacing the template-owned text above. Use when the project wants to change agent or skill behavior, or when checking for drift between .ai/ and the vendor stubs.
---

# manage-ai-capabilities

## Purpose

Enforces the DRY AI architecture: `.ai/` is the single source of truth; vendor folders hold only routing stubs.

## Rules

- Agent and skill behavior is defined only under `.ai/`. No logic is duplicated into `.claude/`, `.github/`, or `.opencode/`.
- Change the `.ai/` file, never the vendor stub, when behavior changes.
- The Coder's OpenCode stub carries `permissions` front matter that mechanically enforces its read-only rule; keep it aligned when that rule changes. All other stubs stay prose-only.
- When the set of agents or skills changes, refresh the matching stubs in every vendor folder.
- Skill identifiers use lowercase kebab-case everywhere: the `.ai/skills/` filename, the frontmatter `name`, the vendor skill directory, and each vendor stub's `name`. Use only `a-z`, `0-9`, and single hyphens, start and end with a letter or digit, and stay within 64 characters. This is the intersection accepted by Claude Code, GitHub Copilot, and OpenCode, so one identifier works in every harness.
- Every `.ai/` agent and skill file carries a `GRAFT BOUNDARY` line and ends with `## Project Customizations`, the project-owned section. Local behavior lives only below the boundary line — never edit the template-owned text above it to fit a project; a graft replaces that text and preserves everything below the line verbatim.
- A customization that contradicts the template-owned text or the workflow's design is the project's to write — the section is theirs — but the contradiction weakens what the template guarantees. Before writing one, name the specific conflict to the human and offer wording that serves the intent within the design; then follow the human's decision. Advise, never veto.

## Duties

1. Add, rename, or remove a `.ai/agents/*.md` or `.ai/skills/*.md` → mirror the change in all three vendor folders.
2. Verify each vendor stub points to the correct core file, carries that harness's required front matter, and uses the same lowercase kebab-case identifier as the core file.
3. Keep each vendor stub's front matter aligned with its `.ai/` source. Skills copy `name` and `description` from the core front matter. Agents carry no core front matter, so keep the stub's one-line `description` aligned in substance with the core file's Purpose. Let only harness-required fields, such as OpenCode `permissions`, differ.
4. The human wants project-specific behavior from an agent or skill → add it to that file's `## Project Customizations` section, applying the contradiction rule above. Routing stubs point into `.ai/`, so they need no change.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Customizations

<!-- Add project-specific customizations below. -->
