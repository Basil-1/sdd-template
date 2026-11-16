# Grafting and Versioning

How a project adopts improvements from a newer version of the template it was built from, and how the template is versioned.

## Template Versioning

The template is versioned semantically; the version lives in `SDD-WORKFLOW.md` frontmatter (`template_version`) and names the template as a whole. A graft replaces that file wholesale, so every project carries its template version.

- **MAJOR** — any change to the meaning of the governing text: rules, roles, artifact lifecycles, ownership boundaries, the graft protocol, or the inventories. Projects build local practice against this text, so changing it is breaking.
- **MINOR** — purely additive text that alters no rule and no inventory: new guidance, expanded rationale, new project placeholders.
- **PATCH** — meaning-preserving corrections: typos, grammar, and clarity edits that leave every rule behaving as before.
- A change between tiers takes the higher tier.

Releases are recorded in `TEMPLATE-CHANGELOG.md` at the template repository root, newest first. That file is excluded from the scaffold copy, so projects never carry stale history; the grafting agent reads it from the reference template.

## Grafting Template Updates

The scaffold separates template-owned text from project-owned content:

- **Wholesale files** — `AGENTS.md`, `CLAUDE.md`, `SDD-WORKFLOW.md`, `GRAFT.md`, everything in `.claude/`, `.github/`, `.opencode/`, plus `project/specs/README.md`. Template-owned; a graft replaces them whole.
- **Split files** — `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `CHANGELOG.md`, `project/adr/README.md`, and every `.ai/` agent and skill file. Each carries the boundary line; a graft replaces everything up to and including it, verbatim.
- **Project content** — everything below a split file's boundary line, plus domain convention files (`CONVENTIONS-<DOMAIN>.md`), domain specs, and ADR files. Project-owned; a graft never touches them.

To adopt template improvements, the human starts a **basic AI agent** — a plain session operating under none of the three agent identities. The graft can replace the files that define those identities, so an agent running under one of them would be rewriting its own instructions mid-session. The basic agent:

1. Compare the reference's `template_version` with the local copy's. On a match, the project is up to date — report it and stop. If the reference is older, stop and tell the human: it may not be the source this project tracks.
2. Read `TEMPLATE-CHANGELOG.md` from the reference and summarize every entry between the local and reference versions — what the graft brings. Call out each major boundary crossed: governing rules changed there, and local practice built on the old rules may need the human's arbitration.
3. Find local modifications to template-owned text using git history: the scaffold arrived whole at the first commit, so every later change to a wholesale file, or to the text at or above a split file's boundary line, is a local modification. Enumerate the commits that touched each file and note what changed.
4. Replace all template-owned text with the current template's: each wholesale file whole, each split file up to and including its boundary line.
5. For each local modification found in step 3, show the human the local change beside the new template text; the human decides whether to reapply it.
6. If the project has a policy about who does what in git, follow it. Otherwise stage the graft and don't commit, so the human can review and iterate.
