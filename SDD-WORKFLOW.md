---
template_version: 10.0.0
---

# SDD Workflow

How work moves through a project built from this template: the roles, the artifacts, and two flows. Flow 1 is the standard path; Flow 2 adds in-branch re-planning and rework.

## Roles

- **Human** — drives every phase transition; plans, verifies manually, directs merges.
- **Planner** (`.ai/agents/planner.md`) — evolves strategy on the base branch, then chambers each increment on a new branch by updating `project/specs/` and writing `PLAN.md`.
- **Coder** (`.ai/agents/coder.md`) — implements against `PLAN.md` and the specs on the branch, treating strategy artifacts as read-only, then writes `INSPECTION.md`.
- **Reviewer** (`.ai/agents/reviewer.md`) — audits the branch adversarially, runs in-branch rework planning when needed, and on a pass holds the merge for a routing session on any durable findings before pruning the roadmap, folding the changelog entry, squash-merging, and pruning old merged branches.

## Artifacts and Lifecycles

**Strategy artifacts** — `PLAN.md`, everything under `project/`, and the AI capability layer (`.ai/`, `.claude/`, `.github/`, `.opencode/`, `AGENTS.md`, `CLAUDE.md`, `SDD-WORKFLOW.md`). Only planning commits write them; the Coder never does.

Every artifact is template-owned (a graft renews it) or project-owned (a graft never touches it). A split file marks the seam with one boundary line: everything up to and including it is the template's, everything below it the project's. Both halves bind equally.

- **Unbranched strategic files** (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md`, `project/adr/`): evolved continuously with understanding. `ARCHITECTURE.md` is backed by ADRs (`manage-adr`). `ROADMAP.md` is pruned as ambition changes: the Reviewer prunes delivered topics at merge; the Planner prunes abandoned topics on sight.
- **Living domain specifications** (`project/specs/<domain>.md`): one file per core domain, describing how the domain behaves now, with no palimpsest. Modified on the feature branch during planning and rework.
- **Branch-ephemeral files** (`PLAN.md`, root `INSPECTION.md`): created on a feature branch to drive and verify one increment, deleted at merge.
- **Merge archive** (`CHANGELOG.md` and git history): each merge lands as one squash commit whose message carries the increment's durable narrative, plus one `CHANGELOG.md` entry. The most recent merged branch is retained for troubleshooting; older ones are deleted.

## Flow 1: Standard Increment (Pass on First Review)

### 1. Unstructured Discovery & Strategy Updates (No Branch)

The human and **Planner** explore ideas openly. Cross-cutting changes to `CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, or `ARCHITECTURE.md` (with new or superseded ADRs via `manage-adr`) are committed by the Planner directly on the base branch.

### 2. Chambering the Increment (Feature Branch Created)

To **chamber** an increment is to load it onto a feature branch — scoped and ready to implement. When the human and Planner agree on the next narrow increment:

1. The Planner creates a new feature branch.
2. On the branch, the Planner edits `project/specs/` to describe the desired behavior, narrowly scoped enough to execute cleanly without model confusion or hard-to-isolate bugs.
3. The Planner writes `PLAN.md`: the implementation steps that bring the codebase into alignment with the updated specifications.
4. The Planner commits these strategy artifacts to the feature branch.

### 3. Autonomous Implementation (Coder)

The human starts a fresh **Coder** session on the feature branch.

1. The Coder reads `PLAN.md`, the updated specs, and the governing files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`).
2. Never modifying strategy artifacts, the Coder implements and verifies iteratively until `PLAN.md` and `project/specs/` are satisfied, then commits.
3. The Coder writes root `INSPECTION.md` fresh, per `.ai/agents/coder.md`, commits it, and hands control back to the human.

### 4. Adversarial Review & Human Verification (Reviewer + Human)

The human starts a fresh **Reviewer** session on the feature branch while running any manual testing specified in `INSPECTION.md`. The Reviewer:

1. Verifies the hard gate: every branch commit touching strategy artifacts is a planning commit by the Planner or the Reviewer.
2. Diffs the branch against its base and audits the implementation and `INSPECTION.md` against `PLAN.md`, `project/specs/`, and the governing files.
3. Reports a **Pass** verdict, or a rework verdict with findings; either carries a triage of the increment's findings for durable value — knowledge planning needed and will need again.
4. Durable findings route with the Reviewer into the branch's planning artifacts — on a pass in a pre-merge session like Flow 2's mini-planning, on a rework in the rework planning itself.
5. On an agreed pass: the Reviewer folds the `INSPECTION.md` entry into `CHANGELOG.md`, prunes the increment's delivered topics from `ROADMAP.md`, and squash-merges into the base branch per its merge protocol, deleting `PLAN.md` and `INSPECTION.md` and retaining only the most recently merged branch.

## Flow 2: Increment with Rework (Including Substantive `project/` Changes)

Steps 1–3 are Flow 1's. The human's manual verification, alongside the Reviewer's audit, shows the increment cannot merge as-is: a spec needs substantive refinement, an architectural constraint or convention needs adjustment, or the remaining delta needs re-scoping.

### 4. In-Branch Mini-Planning (Reviewer + Human)

The Reviewer already holds the adversarial mindset and the review context, so the human plans directly with it:

1. **Substantive `project/` updates**: anything the Planner may do between branches is done here, with the human's agreement — for example `ARCHITECTURE.md` plus an ADR (`manage-adr`), a refined `CONVENTIONS.md` or `CONSTITUTION.md`, or deferred scope moved into `ROADMAP.md`.
2. **Rework addendum**: the Reviewer appends to `PLAN.md` why rework is required and what must change to match the revised `project/` files.
3. The Reviewer commits these strategy artifacts on the feature branch as the next baseline.

### 5. Rework Pass and Re-Review (Fresh Coder, then Reviewer)

1. A fresh **Coder** session runs Flow 1 step 3 unchanged — it need not know this is a rework — and regenerates `INSPECTION.md` fresh so it describes the full branch increment.
2. The **Reviewer** reruns Flow 1 step 4, recognizing the rework baseline commits as planning commits. Steps 4–5 repeat until a pass and successful manual verification.

## Coder Blocked Halt

Working autonomously, the Coder may report **BLOCKED** rather than guess, per its protocol in `.ai/agents/coder.md`. On a BLOCKED report, the human routes it to the **Reviewer**, whose mini-planning session (Flow 2, Step 4) resolves it.

When the block is a gap in a governing artifact, the report carries the problem's shape and may carry a proposed amendment, drafted by the Coder from the clearest view of its specific shape. The Reviewer extracts that ground truth, then shapes the ratified amendment with the human against the big picture the Coder does not hold. The resolution lands in the planning artifacts on the branch: a clarified or re-scoped spec, an adjusted governing file, or a rework addendum to `PLAN.md`. A fresh Coder session then executes it as a normal rework pass.

No `INSPECTION.md` is produced for halted work; partial work stands as committed and is inspectable. A gap the remaining work does not depend on is not a halt: the Coder records it in `INSPECTION.md` as a planning-relevant observation for the Reviewer's triage.

## Grafting and Versioning

Grafting template updates into a project, and the template's semantic versioning: [`GRAFT.md`](GRAFT.md).
