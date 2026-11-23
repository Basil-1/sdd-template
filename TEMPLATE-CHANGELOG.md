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

## 18.0.0 (2026-11-23) — Deterministic increments and maximum-doable halt

- Increments are now chambered by determinism rather than narrowness: a bounded decision space with verifiable contracts, where length is not the test (`.ai/agents/planner.md` Constraints and Purpose, `SDD-WORKFLOW.md` chambering, `project/ROADMAP.md` campaign rule). Agent rules changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.
- The Coder now maximizes doable work before a BLOCKED halt: it completes all unblocked contracts first, commits partial work, then reports completed evidence with verification alongside deferred work and the exact unblock input, with authority unchanged (`.ai/agents/coder.md` **Blocked Halt**, `SDD-WORKFLOW.md` **Coder Blocked Halt**). Agent behavior changed, so MAJOR.

## 17.0.0 (2026-11-22) — Classify LICENSE as a carried notice

- `GRAFT.md` adds a **Carried notice** ownership class: `LICENSE` is not template-owned and a graft never adds, replaces, or flags it; projects that only use the template to build their own work may drop it (`GRAFT.md` **Grafting Template Updates**). The graft's reporting rule changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 16.0.0 (2026-11-22) — Grafting agents shallow-fetch the template with git

- The grafting agent now makes one `git fetch --depth 1` from <https://github.com/Basil-1/sdd-template> into a single temporary directory, fetching `refs/heads/main` for the current template and the tag for the project's own `template_version` as the anchor, and reads both by ref (`GRAFT.md` **Template Versioning** closing paragraph, **Grafting Template Updates** intro, steps 1–4). The graft protocol's reference changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.
- `GRAFT.md` defines a template-owned region once, for grafts to compare and replace, and marks the version tiers as rules for release authors rather than grafting agents (`GRAFT.md` **Template Versioning** opening paragraph, **Grafting Template Updates**). Purely clarifying, so no additional tier change.
- `README.md` **Upgrading existing projects** now states what a graft brings without duplicating the recipe, **Quickstart** step 1 says "delete the last three files" instead of "those three files" after listing four excluded paths, and step 4 glosses "chamber" for first-time readers (`README.md` Quickstart, Upgrading). Documentation of the protocol change above, so no additional tier change.

## 15.0.0 (2026-11-22) — Contracts and predictions

- `PLAN.md` is now written in two kinds of statements: **contracts** — what the Reviewer will verify — which bind, and **predictions** — the Planner's falsifiable claims about existing code and likely mechanism, handed to the Coder as a head start; a falsified prediction can be a planning-relevant observation, never a Coder fault (`.ai/agents/planner.md` **Plan Altitude**).
- The Coder keeps every contract, may overrule a prediction, and halts only on conflicts between contracts; a contradicted prediction is a falsification to record when it carries planning value (`.ai/agents/coder.md` Constraints, workflow steps 2 and 4, **Blocked Halt** trigger).
- The Reviewer audits against contracts, treats a falsified prediction as routable feedback rather than a defect, and plans rework at the Planner's altitude (`.ai/agents/reviewer.md` workflow step 4, **Rework & Mini-Planning**).
- Agent rules changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 14.0.0 (2026-11-21) — Reviewer's verdict opens the mini-planning session

- The Reviewer's verdict now opens the mini-planning session directly — it never asks whether to start one — and the session resolves one of two ways: on a pass, route the durable findings into the branch's planning artifacts, then merge; on a rework, append a rework addendum and iterate (`.ai/agents/reviewer.md` step 6, **Rework & Mini-Planning**). Agent behavior changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 13.1.0 (2026-11-21) — Spec clauses must be executable by the increment

- Tightened the **Branch lifecycle** rule in `project/specs/README.md` to the executability test — a spec clause belongs in a spec only if the increment's code can execute and test it, with behavior needing a future surface routed to `ROADMAP.md` — folding the **Right-sized deltas** bullet into it. Additive wording that alters no other rule, so MINOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 13.0.0 (2026-11-20) — Blocked halt lands in a file the resolution deletes

- A Coder **BLOCKED** halt report is now written to root `BLOCKED.md`, a sibling of `PLAN.md` (`.ai/agents/coder.md` **Blocked Halt**, `SDD-WORKFLOW.md` **Coder Blocked Halt**, **Artifacts and Lifecycles**), so the halt survives the session that raised it and the Reviewer reads it on the branch.
- The Reviewer deletes `BLOCKED.md` when it commits the resolution as the next baseline (`.ai/agents/reviewer.md` **Rework & Mini-Planning**); `README.md` names the new ephemeral file. An artifact lifecycle and agent behavior changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 12.0.0 (2026-11-20) — Subagent delegation contract

- Added `.ai/SUBAGENT.md` as the template's basic-subagent definition, and a `## Delegation` section with a verbatim role addendum to `.ai/agents/planner.md`, `.ai/agents/coder.md`, and `.ai/agents/reviewer.md`; `project/CONSTITUTION.md` and `SDD-WORKFLOW.md` name the shape. The contract is embedded verbatim into any subagent a project delegates to; the template ships no vendor subagent definitions, and a project wanting a persistent one creates its own agent file under a vendor folder.
- `GRAFT.md` inventory: `.ai/SUBAGENT.md` joins the split files; agent or skill files a project creates under `.claude/`, `.github/`, or `.opencode/` are project content a graft never touches; and graft step 4 now adds template-owned files the project lacks (this release's `SUBAGENT.md` is the first) and reports files the template no longer ships.
- Extended `.ai/skills/manage-ai-capabilities.md` with the contract and addendum alignment duty and the rule that the contract is never mirrored into a vendor folder; `README.md` names the delegation boundary.
- Agent behavior and an ownership boundary changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 11.0.1 (2026-11-20) — OpenCode V2-only requirement stated

- Stated the OpenCode V2-only requirement in a `manage-ai-capabilities` rule and the `README.md` layout bullet, so a stub rewritten to V1 syntax is caught instead of silently dropping the Coder's `permissions` enforcement.
- Text only, so PATCH; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 11.0.0 (2026-11-19) — Workflow gains a project-owned tail

- Moved `SDD-WORKFLOW.md` from wholesale to split ownership in `GRAFT.md` **Grafting Template Updates**, and gave it the `GRAFT BOUNDARY` line plus a closing `## Project Workflow Rules` section, so a project can bind the roles to local process without forking template text. The version frontmatter sits above the line, so a graft still refreshes it.
- Restated the versioning rationale in `GRAFT.md` **Template Versioning**: the version lives above the boundary line rather than in a wholesale file.
- Extended `manage-ai-capabilities` to the new seam: the boundary-line rule names both tails, the contradiction rule covers the workflow tail, and routing sends workflow-level rules there while their mechanics stay in project-owned files.
- An ownership boundary changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 10.0.0 (2026-11-17) — Execution harvests what it learned back into planning

- Stated the halting rationale once in `CONSTITUTION.md`: AI time is cheap, human judgment is not, and a guess that later work builds on spends both; halting stays a success of the process.
- Tuned the Coder's Blocked Halt (`.ai/agents/coder.md`, `SDD-WORKFLOW.md` **Coder Blocked Halt**) to the dependency test: halt only when the remaining work depends on a decision the planning artifacts do not supply; a gap it does not depend on goes in `INSPECTION.md` instead.
- Told the Coder that changing course within the decision space the plan and specs afford is normal when an attempt's outcome calls for it, and to ask on each iteration whether it is still moving in the right direction (`.ai/agents/coder.md` step 2).
- Added planning-relevant observations to `INSPECTION.md` (`.ai/agents/coder.md`): what would have helped at planning time, and decisions made under ambiguity with their reasoning.
- Folded a durable-findings triage into the Reviewer's verdict (`.ai/agents/reviewer.md` step 6, observations read in step 4, gate in **Merge**; `SDD-WORKFLOW.md` **Roles**, Flow 1): pass and rework both report findings of durable value, routed with the human into the branch's planning artifacts — pre-merge mini-planning on a pass, the rework planning on a rework; the rest ride the changelog entry.
- Merged the Planner's chambering steps (`.ai/agents/planner.md` step 6) into one charge: guide the human to the plan that runs longest unattended and is least likely to end in a blocked halt, encouraging a bounded decision space and naming where it is thinnest.
- Agent behavior changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

## 9.0.0 (2026-11-16) — Planner stages its changes and waits for the human before committing

- Added a commit gate to `.ai/agents/planner.md` **Constraints**: strategic updates and chambering both stage and report rather than commit, so the human can inspect them first. Agent behavior changed, so MAJOR; `SDD-WORKFLOW.md` frontmatter carries the new `template_version`.

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
