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
