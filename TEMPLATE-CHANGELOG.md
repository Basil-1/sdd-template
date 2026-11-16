# Template Changelog

## Purpose

Reverse-chronological record of released template versions. Written for the grafting agent and the human to answer "what does a graft from version A to version B bring?" This file belongs to the template repository; it is never copied into projects.

## Rules

- One entry per released template version, newest first.
- Entries describe delivered template changes and name the governing files they touch.
- The version bump and its entry ship in the same change set as the change; there is no separate release step.
- Version tiers follow the mapping in `SDD-WORKFLOW.md` under **Template Versioning**.
- The 1.0.0 baseline entry carries no date: it was never a marked release.

## Format

```
## <version> (<date>) — <short title>

- <change>
```

## History

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
