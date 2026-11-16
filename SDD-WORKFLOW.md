---
template_version: 4.0.0
---

# SDD Workflow

## Purpose

A guide to how work moves through a project built from this template: the roles, the artifacts, and two flows. Flow 1 is the standard path — review passes on the first attempt. Flow 2 adds in-branch re-planning and rework when review or manual testing requires it.

## Roles

- **Human** — drives every phase transition, collaborates on planning, runs manual verification protocols, and directs the merge of completed branches.
- **Planner** (`.ai/agents/planner.md`) — conducts unstructured, iterative planning conversations with the human; updates strategy files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md` + ADRs) directly without a branch; and chambers narrow increments on a new feature branch by updating `project/specs/` and writing `PLAN.md`.
- **Coder** (`.ai/agents/coder.md`) — executes on the feature branch against `PLAN.md` and `project/specs/` in autonomous edit/verify loops while treating strategy artifacts (`PLAN.md`, everything under `project/`, and the AI capability layer) as strictly read-only, then writes a fresh `INSPECTION.md` at the repository root.
- **Reviewer** (`.ai/agents/reviewer.md`) — performs an adversarial review of the coder's branch work against `PLAN.md`, `project/specs/`, `INSPECTION.md`, and the governing files; if rework is needed, leads an in-branch mini-planning session with the human to update `project/` and append a rework addendum to `PLAN.md`; and, on a pass, prunes the increment's delivered topics from `ROADMAP.md`, performs the squash merge into the base branch as a single narrative commit, then prunes superseded merged branches, keeping only the most recent.

## Artifacts and Lifecycles

Ownership precedes lifecycle. Every artifact belongs either to the **template** — governing text that a graft renews — or to the **project** — content that a graft never touches. Files with two owners are divided by section: from its boundary section down, the file is the project's; above, the template's. Both halves bind the agents equally, and each owner's intent belongs on its own side of the divider. The lifecycles below are of the project's half.

- **Unbranched strategic files** (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md`, `project/adr/`): Evolved continuously with understanding. `ARCHITECTURE.md` is backed by ADRs (maintained via `manage-adr`). `ROADMAP.md` reflects the ambitions as items are delivered or abandoned: the Reviewer prunes delivered topics at merge; the Planner prunes abandoned or overlooked topics on sight as a backstop.
- **Living domain specifications** (`project/specs/<domain>.md`): One file per core domain. Each spec describes how its domain behaves right now with no palimpsest. Modified directly on a feature branch during planning (and during rework re-planning) alongside `PLAN.md`.
- **Branch-ephemeral files** (`PLAN.md` and root `INSPECTION.md`): Created on a feature branch to drive and verify a single narrow increment, and deleted when the branch merges.
- **Merge archive** (`CHANGELOG.md` and Git history): Each branch merge lands on the base branch as a single squash commit whose message carries the increment's narrative of durable value, plus one `CHANGELOG.md` entry summarizing delivered behavior. The most recently merged feature branch is retained for troubleshooting; older merged branches are deleted. The narrative and the retained branch are the archive — never a palimpsest.

---

## Flow 1: Standard Increment (Pass on First Review)

### 1. Unstructured Discovery & Strategy Updates (No Branch)
The human and the **Planner** explore ideas in an open-ended conversation.
- Cross-cutting changes to `CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, or `ARCHITECTURE.md` (with new or superseded ADRs via `manage-adr`) are committed **by the Planner** directly on the base branch.

### 2. Chambering the Increment (Feature Branch Created)
To **chamber** an increment is to load it onto a feature branch — scoped and ready for implementation. When the human and **Planner** agree it's time for the next narrow increment:
1. The Planner creates a new feature branch.
2. On the branch, the Planner directly edits `project/specs/` to describe the desired behavior, narrowly scoped enough to execute cleanly without model confusion or hard-to-isolate bugs. 
3. The Planner writes `PLAN.md` detailing the implementation steps to bring the codebase into alignment with the updated specifications.
4. **The Planner** commits the strategy artifact changes to the feature branch.

### 3. Autonomous Implementation (Coder)
The human starts a fresh **Coder** session on the feature branch.
1. The Coder reads `PLAN.md`, the updated domain specs in `project/specs/`, and the governing files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`).
2. Without ever modifying strategy artifacts, the Coder implements and verifies the changes iteratively until `PLAN.md` and `project/specs/` are satisfied, then commits the implementation.
3. The Coder writes `INSPECTION.md` from scratch at the repository root with manual verification steps, self-verification evidence, and proposed `CHANGELOG.md` additions, then commits the file and hands control back to the human.

### 4. Adversarial Review & Human Verification (Reviewer + Human)
The human starts a fresh **Reviewer** session on the feature branch while running any manual testing specified in `INSPECTION.md`. The Reviewer audits the branch:
1. Checks the branch commit history to confirm the hard gate: the Coder never modified strategy artifacts — `PLAN.md`, everything under `project/`, and the AI capability layer (`.ai/`, `.claude/`, `.github/`, `.opencode/`, `AGENTS.md`, `CLAUDE.md`, `SDD-WORKFLOW.md`). Every commit touching them is a planning commit.
2. Diffs the branch against the base branch and audits the implementation and `INSPECTION.md` against `PLAN.md`, `project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. Reports a **Pass** verdict to the human.
4. If the human agrees, appends the single branch entry from `INSPECTION.md` into `CHANGELOG.md` and prunes the increment's delivered topics from `ROADMAP.md`.
5. On the human's direction, performs the squash merge per its merge protocol in `.ai/agents/reviewer.md`: composes the narrative of durable value from the review context, deletes `PLAN.md` and `INSPECTION.md`, squash-merges the feature branch into the base branch as a single commit, and prunes previously merged branches, retaining only the most recently merged.

---

## Flow 2: Increment with Rework (Including Substantive `project/` Changes)

Steps **1 through 3** happen exactly as in Flow 1: strategy is updated, a feature branch is created with updated specifications in `project/specs/` and `PLAN.md`, and the **Coder** implements the first pass and generates `INSPECTION.md`.

### 4. Adversarial Review Uncovers a Deeper Issue (Reviewer + Human)
The human runs manual verification alongside the **Reviewer**'s adversarial audit. Together they discover that the increment cannot be merged as-is because seeing the working attempt reveals a deeper problem, for example:
- A desired behavior in the spec needs substantive refinement,
- An architectural constraint in `ARCHITECTURE.md` (and its backing ADR) or a rule in `CONVENTIONS.md` needs adjustment, or
- The remaining delta needs to be re-scoped.

### 5. In-Branch Mini-Planning Session (Reviewer + Human)
The human conducts a mini-planning session directly with the **Reviewer**, who already holds the adversarial mindset and the code review context:
1. **Substantive `project/` updates**: Anything the Planner can do between branches can be done here on the feature branch. With the human's agreement, the Reviewer updates the affected files in `project/`—for example:
   - Updating `ARCHITECTURE.md` and creating or superseding an ADR via `manage-adr`,
   - Refining `CONVENTIONS.md` or `CONSTITUTION.md`, or moving deferred scope into `ROADMAP.md`.
2. **Plan rework addendum**: The Reviewer appends a rework addendum to `PLAN.md` explaining why rework is required and what must be addressed to match the revised `project/` files.
3. **Commit strategy artifacts**: **The Reviewer** commits all strategy artifact changes on the feature branch (after the earlier creation of `INSPECTION.md`), establishing the new baseline for the next review gate.

### 6. Rework Pass (Fresh Coder Session)
The human invokes a fresh **Coder** session. The Coder runs the exact same workflow as on the first pass—it does not need to know whether this is an initial run or a rework:
1. The Coder reads the current `project/` files (`project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, `CONSTITUTION.md`) and `PLAN.md` (which now includes the rework addendum).
2. Keeping strategy artifacts strictly read-only, the Coder updates and verifies the implementation iteratively until the revised specs and plan are satisfied, and commits the code changes.
3. The Coder regenerates `INSPECTION.md` completely from scratch (overwriting the previous file) so it reflects the full, updated branch increment.

### 7. Re-Review & Merge (Reviewer + Human)
1. The **Reviewer** runs again on the branch and verifies the hard gate exactly as in Flow 1, recognizing the rework baseline commits from Step 5 as planning commits.
2. The Reviewer audits the updated code and newly regenerated `INSPECTION.md` against the revised `project/specs/`, `PLAN.md` (and its addenda), `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. If further iteration is needed, Steps 5–7 repeat. Once the Reviewer reports **Pass** and manual verification succeeds, the human instructs the Reviewer to fold the branch's work into a single entry in `CHANGELOG.md` and perform the squash merge, exactly as in Flow 1.

## Template Versioning

The template is versioned semantically, and the version lives in this file's frontmatter (`template_version`). It names the template as a whole, not this document: a graft replaces this file wholesale, so every project carries its template version, and every graft delivers the next one.

The tiers:

- **MAJOR** — any change to the meaning of the template's governing text: rules, roles, artifact lifecycles, ownership boundaries, the graft protocol, or the wholesale and scaffold inventories. Projects build local practice against this text, so changing it is breaking.
- **MINOR** — purely additive text that alters no rule and no inventory: new non-normative guidance, expanded rationale, new project-content placeholders.
- **PATCH** — meaning-preserving corrections: typos, grammar, and clarity rewrites that leave every rule behaving as before.
- When a change sits between tiers, choose the higher.

Releases are recorded in `TEMPLATE-CHANGELOG.md` at the template repository root — one entry per released version, newest first. The file is excluded from the scaffold copy, so projects never carry a stale history; the grafting agent reads it from the reference template. Whoever ships a change to template-owned text bumps `template_version` and writes its entry in the same change set; there is no separate release step. Such changes touch strategy artifacts, so under this workflow they land with a planning commit — the Planner's, or the Reviewer's during in-branch rework.

## Grafting Template Updates

The scaffold separates template-owned text from project-owned content:

- **Wholesale files** — `AGENTS.md`, `CLAUDE.md`, `SDD-WORKFLOW.md`, everything in `.claude/`, `.github/`, `.opencode/`, plus `project/specs/README.md` and `project/adr/README.md`. Template-owned; a graft replaces them whole.
- **Scaffold sections** — the Purpose, Rules, and Format sections of `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`, `ROADMAP.md`, and `CHANGELOG.md`, plus everything in each `.ai/` agent and skill file above its `## Project Customizations` section. Template-owned; a graft replaces them verbatim.
- **Project content** — everything else: the designated content sections (`## Project Laws`, `## Project Conventions`, `## System Design`, `## Campaigns`, `## History`), the `## Project Customizations` section of each `.ai/` agent and skill file, table rows in the ADR index and the changelog, domain specs, and ADR files. Project-owned; a graft never touches them.

To adopt template improvements, the human starts a **basic AI agent** — a plain AI session that does **not** operate under any of the three agent identities (Planner, Coder, or Reviewer) — to run the graft on the base branch. The graft can replace the very files that define those identities (everything in `.ai/`, `.claude/`, `.github/`, and `.opencode/`), so an agent running under one of them would be rewriting its own instructions mid-session and cannot do this safely. The basic agent:

1. Obtain the current template as reference. Compare the `template_version` in the reference's `SDD-WORKFLOW.md` against the local copy's. On a match, the project is up to date — report that and stop. If the reference is older than the local copy, stop and tell the human: the reference may not be the source this project tracks.
2. Read `TEMPLATE-CHANGELOG.md` from the reference and summarize for the human every entry between the local and reference versions — this is what the graft brings. Call out each major boundary crossed: governing rules changed there, and local practice built on the old rules may need the human's arbitration.
3. Find local modifications to template-owned text using the project's Git history: the scaffold arrived whole at the first commit, so every later change to template-owned files or sections is a local modification. Enumerate the commits that touched each file and note what they changed in template-owned territory.
4. Replace all template-owned files and sections with the current template's text.
5. For each local modification found in step 3, show the human the local change alongside the new template text; the human decides whether to reapply the local change on top of it.
6. If the project has an existing policy about who does what in git, follow it. Otherwise, stage the graft but don't commit, so the human can review and iterate.

## Coder Blocked Halt

Working autonomously, the Coder may report **BLOCKED** rather than proceed by guessing, per its protocol in `.ai/agents/coder.md`.

On a BLOCKED report, the human routes it to the **Reviewer**, whose in-branch mini-planning session (Flow 2, Step 5) is the resolution path. When the block is a gap in a governing artifact, the report describes the gap in enough detail to plan against, and may carry the Coder's proposed amendment — drafted language to close the gap, written from the clearest view of its specific shape. The Reviewer extracts that problem-shape context as ground truth, then shapes the ratified amendment with the human against the big picture the Coder does not hold. The resolution lands in the planning artifacts on the feature branch — a clarified or re-scoped spec, an adjusted governing file, or a rework addendum to `PLAN.md`. A fresh Coder session then executes it as a normal rework pass.

No `INSPECTION.md` is produced for halted work; partial work stands as committed and is inspectable. A halt is the cheapest possible time to find a flaw — welcome it.
