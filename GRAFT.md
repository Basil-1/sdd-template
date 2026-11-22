# Grafting and Versioning

How a project adopts improvements from a newer version of the template it was built from, and how the template is versioned.

## Template Versioning

The template is versioned semantically; the version lives in `SDD-WORKFLOW.md` frontmatter (`template_version`) and names the template as a whole. That frontmatter sits above the file's boundary line, which a graft replaces, so every project carries its template version. The version location and the release tags below are what a grafting agent needs; the tiers are for release authors.

- **MAJOR** — any change to the meaning of the governing text: rules, roles, artifact lifecycles, ownership boundaries, the graft protocol, or the inventories. Projects build local practice against this text, so changing it is breaking.
- **MINOR** — purely additive text that alters no rule and no inventory: new guidance, expanded rationale, new project placeholders.
- **PATCH** — meaning-preserving corrections: typos, grammar, and clarity edits that leave every rule behaving as before.
- A change between tiers takes the higher tier.

Releases are recorded in `TEMPLATE-CHANGELOG.md` at the template repository root, newest first, and each release commit carries a lightweight git tag naming its version, pushed with the repository. That file is excluded from the scaffold copy, so projects never carry stale history; the grafting agent shallow-fetches it, `SDD-WORKFLOW.md`, and the tag for the project's own version from the template repository at <https://github.com/Basil-1/sdd-template>.

## Grafting Template Updates

The scaffold separates template-owned text from project-owned content:

- **Wholesale files** — `AGENTS.md`, `CLAUDE.md`, `GRAFT.md`, every stub the template ships in `.claude/`, `.github/`, `.opencode/`, plus `project/specs/README.md`. Template-owned; a graft replaces them whole.
- **Split files** — `SDD-WORKFLOW.md`, `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `CHANGELOG.md`, `project/adr/README.md`, `.ai/SUBAGENT.md`, and every `.ai/` agent and skill file. Each carries the boundary line; a graft replaces everything up to and including it, verbatim.
- **Project content** — everything below a split file's boundary line, plus domain convention files (`CONVENTIONS-<DOMAIN>.md`), domain specs, ADR files, and any agent or skill file a project creates under `.claude/`, `.github/`, or `.opencode/` that the template does not ship. Project-owned; a graft never touches them.

A **template-owned region** is a wholesale file whole, or a split file up to and including its boundary line; grafts compare and replace regions, never whole split files.

To adopt template improvements, the human starts a **basic AI agent** — a plain session operating under none of the three agent identities. The graft can replace the files that define those identities, so an agent running under one of them would be rewriting its own instructions mid-session. The basic agent creates one temporary directory and shallow-fetches with git from <https://github.com/Basil-1/sdd-template>: `git init` in it, then one `git fetch --depth 1 <url> refs/tags/<tag>:refs/tags/<tag> refs/heads/main:refs/remotes/origin/main`, where `<tag>` is the project's own `template_version`. It reads current-template files from `origin/main` and anchor files from `<tag>` with `git show <ref>:<path>`. The agent:

1. Compare the current template's `template_version` with the local copy's. On a match, the project is up to date — report it and stop. If the current version is older than the local one, stop and tell the human: it may not be the source this project tracks.
2. Read `TEMPLATE-CHANGELOG.md` from the current template and summarize every entry between the local and current versions — what the graft brings. Call out each major boundary crossed: governing rules changed there, and local practice built on the old rules may need the human's arbitration.
3. Find local modifications by diffing each template-owned region at the project's anchor tag against the local copy, by content not history. Any difference is a local modification, reported with its diff; a split file missing its boundary line is itself one. If the fetch of the anchor tag fails, it may not be the source this project tracks — tell the human. Consult git history only to attribute a flagged change when that helps the human arbitrate.
4. Replace every template-owned region with the current template's. Add any template-owned file the current template ships that the project lacks, and report any the project carries that the current template no longer ships — the human decides whether to delete it.
5. For each local modification found in step 3, show the human the local change beside the new template text; the human decides whether to reapply it.
6. If the project has a policy about who does what in git, follow it. Otherwise stage the graft and don't commit, so the human can review and iterate.
