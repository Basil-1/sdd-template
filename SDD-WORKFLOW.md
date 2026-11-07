# SDD Workflow

## Purpose

A guide to how work moves through a project built from this template: the roles, the artifacts, the standard flow when an increment passes review on the first pass, and the rework flow when review or manual testing requires re-planning and rework on the branch.

## Roles

- **Human** — drives every phase transition, collaborates on planning, runs manual verification protocols, and merges completed branches.
- **Planner** (`.ai/agents/planner.md`) — conducts unstructured, iterative planning conversations with the human; updates strategy files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md` + ADRs) directly without a branch; and chambers narrow increments on a new feature branch by updating `project/specs/` and writing `PLAN.md`.
- **Coder** (`.ai/agents/coder.md`) — executes on the feature branch against `PLAN.md` and `project/specs/` in autonomous edit/verify loops while treating `project/` as strictly read-only, then writes a fresh `INSPECTION.md` at the repository root.
- **Reviewer** (`.ai/agents/reviewer.md`) — performs an adversarial review of the coder's branch work against `PLAN.md`, `project/specs/`, `INSPECTION.md`, and the governing files; and, if rework is needed, leads an in-branch mini-planning session with the human to update `project/` and append a rework addendum to `PLAN.md`.

## Artifacts and Lifecycles

- **Unbranched strategic files** (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md`, `project/adr/`): Evolved continuously with understanding. `ARCHITECTURE.md` is backed by ADRs (maintained via `manage-adr`). `ROADMAP.md` is updated to reflect the ambitions as items are delivered or abandoned.
- **Living domain specifications** (`project/specs/<domain>.md`): One file per core domain. Each spec describes how its domain behaves right now with no palimpsest. Modified directly on a feature branch during planning (and during rework re-planning) alongside `PLAN.md`.
- **Branch-ephemeral files** (`PLAN.md` and root `INSPECTION.md`): Created on a feature branch to drive and verify a single narrow increment, and deleted when the branch merges.
- **Merge archive** (`CHANGELOG.md` and Git history): Updated once per branch merge with a single entry summarizing delivered behavior. Git history serves as the archive for all pruned roadmap items and superseded states.

---

## Flow 1: Standard Increment (Pass on First Review)

### 1. Unstructured Discovery & Strategy Updates (No Branch)
The human and the **Planner** explore ideas in an open-ended conversation.
- Cross-cutting changes to `CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, or `ARCHITECTURE.md` (with new or superseded ADRs via `manage-adr`) are committed **by the human** directly on the base branch.

### 2. Chambering the Increment (Feature Branch Created)
When the human and **Planner** agree it's time for the next narrow increment:
1. The Planner creates a new feature branch.
2. On the branch, the Planner directly edits `project/specs/` to describe the desired behavior, narrowly scoped enough to execute cleanly without model confusion or hard-to-isolate bugs. 
3. The Planner writes `PLAN.md` detailing the implementation steps to bring the codebase into alignment with the updated specifications.
4. **The human** commits the `project/` changes to the feature branch.

### 3. Autonomous Implementation (Coder)
The human starts a fresh **Coder** session on the feature branch.
1. The Coder reads `PLAN.md`, the updated domain specs in `project/specs/`, and the governing files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`).
2. Without ever modifying `project/`, the Coder implements and verifies the changes iteratively until `PLAN.md` and `project/specs/` are satisfied, then commits the implementation.
3. The Coder writes `INSPECTION.md` from scratch at the repository root with manual verification steps, self-verification evidence, and proposed `CHANGELOG.md` additions, then commits the file and hands control back to the human.

### 4. Adversarial Review & Human Verification (Reviewer + Human)
The human starts a fresh **Reviewer** session on the feature branch while running any manual testing specified in `INSPECTION.md`. The Reviewer audits the branch:
1. Checks the branch commit history to confirm the hard gate: `project/` was not modified after the Planner's initial commit on the branch.
2. Diffs the branch against the base branch and audits the implementation and `INSPECTION.md` against `PLAN.md`, `project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. Reports a **Pass** verdict to the human.
4. If the human agrees, appends the single branch entry from `INSPECTION.md` into `CHANGELOG.md`.
5. Deletes `PLAN.md` and `INSPECTION.md`.
6. **The human** merges the feature branch into the base branch.

---

## Flow 2: Increment with Rework (Including Substantive `project/` Changes)

Steps **1 through 3** happen exactly as in Flow 1: strategy is updated, a feature branch is created with updated specifications in `project/specs/` and `PLAN.md`, and the **Coder** implements the first pass and generates `INSPECTION.md`.

### 4. Adversarial Review Uncovers a Deeper Issue (Reviewer + Human)
The human runs manual verification alongside the **Reviewer**'s adversarial audit. Together they discover that the increment cannot be merged as-is because seeing the working attempt reveals a deeper problem, for example:
- A desired behavior in the spec needs substantive refinement,
- An architectural constraint in `ARCHITECTURE.md` (and its backing ADR) or a rule in `CONVENTIONS.md` needs adjustment, or
- The remaining delta needs to be re-scoped and run with a stronger model.

### 5. In-Branch Mini-Planning Session (Reviewer + Human)
The human conducts a mini-planning session directly with the **Reviewer**, who already holds the adversarial mindset and the code review context:
1. **Substantive `project/` updates**: Anything the Planner can do between branches can be done here on the feature branch. With the human's agreement, the Reviewer updates the affected files in `project/`—for example:
   - Updating `ARCHITECTURE.md` and creating or superseding an ADR via `manage-adr`,
   - Refining `CONVENTIONS.md` or `CONSTITUTION.md`, or moving deferred scope into `ROADMAP.md`.
2. **Plan rework addendum**: The Reviewer appends a rework addendum to `PLAN.md` explaining why rework is required and what must be addressed to match the revised `project/` files.
3. **Commit `project/`**: **The human** commits all `project/` changes on the feature branch (after the earlier creation of `INSPECTION.md`), establishing the new baseline for the next review gate.

### 6. Rework Pass (Fresh Coder Session)
The human invokes a fresh **Coder** session (selecting a different model if warranted). The Coder runs the exact same workflow as on the first pass—it does not need to know whether this is an initial run or a rework:
1. The Coder reads the current `project/` files (`project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, `CONSTITUTION.md`) and `PLAN.md` (which now includes the rework addendum).
2. Keeping `project/` strictly read-only, the Coder updates and verifies the implementation iteratively until the revised specs and plan are satisfied, and commits the code changes.
3. The Coder regenerates `INSPECTION.md` completely from scratch (overwriting the previous file) so it reflects the full, updated branch increment.

### 7. Re-Review & Merge (Reviewer + Human)
1. The **Reviewer** runs again on the branch, sees from the commit history that this is a review subsequent to a rework modification to `project/`, and verifies the hard gate: `project/` was not modified since the most recent commit to `project/` after the previous `INSPECTION.md`.
2. The Reviewer audits the updated code and newly regenerated `INSPECTION.md` against the revised `project/specs/`, `PLAN.md` (and its addenda), `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. If further iteration is needed, Steps 5–7 repeat. Once the Reviewer reports **Pass** and manual verification succeeds, the human instructs the Reviewer to fold the branch's work into a single entry in `CHANGELOG.md`, delete `PLAN.md` and `INSPECTION.md`, and then **the human** merges the branch.
