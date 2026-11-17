# Template Changelog

## Purpose

Reverse-chronological record of released template versions. Written for the grafting agent and the human to answer "what does a graft from version A to version B bring?" This file belongs to the template repository; it is never copied into projects.

## Rules

- One entry per released template version, newest first.
- Entries describe delivered template changes and name the governing files they touch.
- The version bump and its entry ship in the same change set as the change; there is no separate release step.
- The release commit carries a lightweight tag naming its version (`git tag X.Y.Z <commit>`), and tags travel with pushes to the remote.
- Version tiers follow the mapping in `GRAFT.md` under **Template Versioning**.
- One bullet per change, naming the files touched; no rationale beyond a clause.
- The 1.0.0 baseline entry carries no date: it was never a marked release.

## Format

```
## <version> (<date>) — <short title>

- <change>
```

## History

## 8.0.0 (2026-11-16) — Planner stops recording its open questions as decisions

- Added `## Interview Discipline` to `.ai/agents/planner.md`, closing a leak of the Planner's own reasoning into the artifacts: its open questions and analysis now stay in the conversation rather than landing in `project/` and `PLAN.md` as if the human had decided them, unanswered questions stay unanswered, and detail below the human's altitude is an open question rather than an oversight to document. Agent behavior changed, so MAJOR.
- Routed in-branch rework planning through the same discipline in `.ai/agents/reviewer.md`.

## 7.0.0 (2026-11-16) — Graft finds local modifications by anchored content, not history

- Rewrote graft step 3 in `GRAFT.md`: the working tree's template-owned regions are diffed against the reference's tag for the project's own `template_version`, replacing the enumeration of every commit since the first. The work is bounded by file count, the verdict stays correct across past grafts — whose replacement commits the old rule misread as local modifications — and the diff feeds step 5's arbitration directly. The fallback for pre-versioning projects is dropped: step 1 already stops a project carrying no version. The graft protocol changed, so MAJOR.
- `GRAFT.md` **Template Versioning** now promises each release commit carries a lightweight tag naming its version and that the grafting agent reads the project's own version tag from the reference clone; this file's **Rules** carries the obligation against the template repository itself. Releases 2.0.0–6.0.0 are tagged retroactively; 1.0.0 was never a marked release and stays untagged.

## 6.0.0 (2026-11-16) — Leaner governing text; graft protocol split out

- Moved **Template Versioning** and **Grafting Template Updates** out of `SDD-WORKFLOW.md` into a new wholesale file, `GRAFT.md`, so the workflow a session must read before work stays short. The workflow points to it in one line, and `README.md` routes there.
- Defined **Strategy artifacts** once in `SDD-WORKFLOW.md` and routed to it from the agent files, replacing four separate enumerations.
- Gave each governing rule one home: the no-palimpsest rule to `CONSTITUTION.md`, the squash-merge rule to `.ai/agents/reviewer.md`, `INSPECTION.md` contents to `.ai/agents/coder.md`, and amendment etiquette to the workflow's **Coder Blocked Halt**.
- Compressed Roles to one line each, the ownership preamble to three sentences, and every agent, skill, and strategy file to lower-entropy prose. Shortened all four mirrored copies of each skill description.
- Leaving `SDD-WORKFLOW.md` wholesale but adding a wholesale file changes the inventory, and flow step numbers moved, so MAJOR.

## 5.1.0 (2026-11-16) — Convention splits stop leaking into references

- Fixed an ownership ambiguity in the `CONVENTIONS.md` domain-split rule: a `CONVENTIONS-<DOMAIN>.md` file was "treated exactly like this one", which left open whether a project copies the hub's template-owned Rules above a boundary line. Such a file now binds exactly as the hub does but is wholly project content — no boundary line, and a graft never touches it — and the hub's route line sits under `## Project Conventions`, below the boundary, where a graft cannot erase it. `SDD-WORKFLOW.md` names domain convention files in the graft inventory's **Project content** bullet, where the closed file lists had left them uncovered.
- Added the reference rule to the `CONVENTIONS.md` scaffold: a convention is cited as `CONVENTIONS.md` (topic optional), never a `CONVENTIONS-<DOMAIN>.md` file — only the hub's routes name domain files — so a split leaves every reference intact. Purely additive, touching no existing rule or inventory, so MINOR.

## 5.0.1 (2026-11-15) — Graft-facing release note loses its planning-commit claim

- Dropped the trailing sentences of **Template Versioning** in `SDD-WORKFLOW.md`: the version-bump discipline and a claim that template-owned changes land as planning commits. The first is already stated verbatim in `TEMPLATE-CHANGELOG.md` **Rules**, and the second described the project flows — a graft runs as a basic agent outside all three identities, so the claim misdirected the reader it was addressed to. The hard gate in Flow 1 Step 4 still states that every commit touching this file is a planning commit. No rule changed behavior, so PATCH.

## 5.0.0 (2026-11-15) — One demarcation line for every split file

- Defined ownership's seam as a single line — `<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->` — in `SDD-WORKFLOW.md`: everything up to and including it is the template's, everything below it the project's, and no heading name marks the division. **Scaffold sections** became **Split files**, a list of filenames plus every `.ai/` agent and skill file, dropping the exhaustive section names; template-side sections can now be added, reordered, or renamed without touching the inventory. `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `CHANGELOG.md`, `project/adr/README.md`, and every `.ai/` agent and skill file all carry the line.
- Graft steps 3 and 4 now read the line mechanically: a local modification is any later change to a wholesale file or to the text at or above a split file's boundary line, and replacement runs up to and including it. `manage-ai-capabilities` states the same rule for the `.ai/` files, and its description — in all four mirrored copies — points at the boundary line rather than at a named section.
- Fixed a contradicted ownership entry: `project/adr/README.md` was listed wholesale while the ADR index rows were listed as project content, so a graft would have wiped the project's index. The file is a split file like the rest; its `## Index` moved below the boundary line to the end of the file, and Authoring's "append one row to the index above" points there.
- Ownership moved from section names to a marker, and the ADR index changed hands, so MAJOR.

## 4.0.1 (2026-11-15) — Repair the manage-ai-capabilities description

- Restored the broken sentence in the `manage-ai-capabilities` description across all four mirrored copies (`.ai/skills/manage-ai-capabilities.md` and its `.claude/`, `.github/`, and `.opencode/` stubs): `layer- agent` became `layer. Agent`. The stray hyphen replaced a colon in an unquoted YAML scalar, where `: ` is invalid; the sentence is now punctuated without one, so the front matter parses cleanly in every harness without quoting. Wording and triggers are unchanged, so PATCH.

## 4.0.0 (2026-11-15) — Roadmap cleanup moves to the merge flow

- Delivered-topic pruning now runs at merge: a new step in the Reviewer's `## Merge` protocol (`.ai/agents/reviewer.md`) removes the increment's delivered topics from `ROADMAP.md` beside the `CHANGELOG.md` append, riding the merge-prep commit into the squash. Merge is the moment what was delivered is exactly known. `SDD-WORKFLOW.md` carries the routing in **Roles**, **Artifacts and Lifecycles**, and Flow 1 Step 4; Flow 2 inherits it via "exactly as in Flow 1".
- The Planner's on-sight pruning (`.ai/agents/planner.md` step 5) stays as a de-emphasized backstop for abandoned or overlooked topics only. The `ROADMAP.md` **Rules** wording matches: delivered topics are pruned at merge, everything else on sight.
- The cleanup moment inside the increment lifecycle changed owners, so MAJOR.

## 3.0.0 (2026-11-15) — Project customizations for agents and skills

- Appended a project-owned `## Project Customizations` section to every `.ai/` agent and skill file, letting a project give its roles local specifications the way it gives `CONVENTIONS.md` local conventions. The Planner maintains these sections on the base branch and the Reviewer during in-branch rework — via `manage-ai-capabilities`, landing as planning commits; the Coder keeps the whole capability layer strictly read-only, so no hard-gate or permission changes were needed.
- Moved `.ai/` agent and skill files in **Grafting Template Updates** from the wholesale inventory to split ownership: everything above `## Project Customizations` joins the scaffold sections (replaced verbatim), the section itself joins project content (never touched). An ownership-boundary and inventory change, hence MAJOR.
- Rewrote the `manage-ai-capabilities` description — in all four mirrored copies — as a project-facing text: its triggers are now changing agent or skill behavior and checking stub drift, pointing the project at the graft-safe move, `## Project Customizations`, and away from the template-owned text a graft replaces. The body rules keep weigh-the-contradiction advisory: name the cost, offer fitted wording, defer to the human — advise, never veto.
- Stated the template/project split once, as a form, in an ownership lead atop **Artifacts and Lifecycles** in `SDD-WORKFLOW.md`: divided by section, both halves binding, intent stays on its owner's side of the divider. With the form central, in-file markers shrank to boundary heading plus locator comment — the six customization sections dropped their framing sentence, and the four strategy files' placeholder comments shed the `The sections above are owned by the template.` tail.
- Removed the "Your turn ends here. The human drives the next step." closer from the Planner and Coder — phase handover is the workflow's domain, and the line no longer belongs where the customization section ends the file.

## 2.1.1 (2026-11-15) — README skills count

- Corrected `README.md`: `.ai/` holds three skills — `commit`, `manage-adr`, `manage-ai-capabilities` — not two. The count had been stale since the `commit` skill was added without updating the inventory line.

## 2.1.0 (2026-11-15) — Optional domain conventions split

- Added a permissive rule to the `CONVENTIONS.md` scaffold: a domain's conventions may split into a `CONVENTIONS-<DOMAIN>.md` file beside the hub, routed by a one-line entry there, when the hub's bulk would overburden agents working outside that domain. The rule states the split is an allowed flexibility, not an expected structure, and that any such file is treated exactly like the hub (`project/CONVENTIONS.md`).

## 2.0.0 (2026-11-15) — Template versioning

- Added `template_version` frontmatter to `SDD-WORKFLOW.md`; the version names the template as a whole and travels with this wholesale-replaced file.
- Added the **Template Versioning** section to `SDD-WORKFLOW.md`: the semver tiers (MAJOR — any change to governing text; MINOR — purely additive text; PATCH — meaning-preserving corrections) and this release-history convention.
- Added this file at the template repository root, excluded from the scaffold copy alongside `README.md`.
- Extended **Grafting Template Updates** in `SDD-WORKFLOW.md`: the graft now compares template versions, stops when the project is already up to date, and summarizes the entries between the two versions for the human, calling out major boundaries.
- Wired the versioning into `README.md`: the copy instructions exclude this file, and the update section points at the version and the history.

## 1.0.0 — Unversioned baseline

- The template text as it stood before versioning was introduced.
