---
name: manage-ai-capabilities
description: Maintains the DRY AI capability layer — behavior lives in .ai/, mirrored by vendor routing stubs, with project customizations below each file's boundary line. Use when changing agent or skill behavior or checking stub drift.
---

# manage-ai-capabilities

## Rules

- Agent and skill behavior is defined only under `.ai/`. No logic is duplicated into `.claude/`, `.github/`, or `.opencode/`.
- Change the `.ai/` file, never the vendor stub, when behavior changes.
- The Coder's OpenCode stub carries `permissions` front matter that mechanically enforces its read-only rule; keep it aligned when that rule changes. All other stubs stay prose-only.
- When the set of agents or skills changes, refresh the matching stubs in every vendor folder.
- Skill identifiers use lowercase kebab-case everywhere: the `.ai/skills/` filename, the frontmatter `name`, the vendor skill directory, and each vendor stub's `name`. Use only `a-z`, `0-9`, and single hyphens, starting and ending with a letter or digit, within 64 characters — the intersection Claude Code, GitHub Copilot, and OpenCode accept, so one identifier works everywhere.
- Every `.ai/` agent and skill file carries a `GRAFT BOUNDARY` line and ends with `## Project Customizations`; `SDD-WORKFLOW.md` carries one too and ends with `## Project Workflow Rules`. Local behavior lives only below the boundary line; a graft replaces the text above it and preserves everything below verbatim.
- A customization that contradicts the template-owned text — in a `.ai/` file or in the workflow's project-owned tail — weakens what the template guarantees. Name the specific conflict to the human and offer wording that serves the intent within the design, then follow the human's decision. Advise, never veto.

## Duties

1. Add, rename, or remove a `.ai/agents/*.md` or `.ai/skills/*.md` → mirror it in all three vendor folders.
2. Verify each stub points to the correct core file, carries that harness's front matter, and uses the same identifier. Skills copy `name` and `description` from the core front matter; agents carry no core front matter, so keep the stub's `description` aligned in substance with the core Purpose. Only harness-required fields, such as OpenCode `permissions`, may differ.
3. Route project-specific behavior into that file's `## Project Customizations` section, applying the contradiction rule above; route workflow-level rules into `SDD-WORKFLOW.md`'s `## Project Workflow Rules`, naming any project-owned file the mechanics live in. Stubs point into `.ai/`, so they need no change.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Customizations

<!-- Add project-specific customizations below. -->
