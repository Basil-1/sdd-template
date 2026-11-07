# SDD Workflow

## Purpose

A guide to how work moves through a project built from this template: the roles, the artifacts, the standard flow when an increment passes review on the first pass, and the send-back flow when review or manual testing requires re-planning and rework on the branch.

## Roles

- **Human** — drives every phase transition, collaborates on planning and domain boundaries, runs manual verification protocols, and merges completed branches.
- **Planner** (`.ai/agents/planner.md`) — conducts unstructured, iterative planning conversations with the human; updates strategy files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, `ARCHITECTURE.md` + ADRs) directly without a branch; and chambers narrow increments on a new feature branch by updating `project/specs/` and writing `project/PLAN.md`.
- **Coder** (`.ai/agents/coder.md`) — executes on the feature branch against `project/PLAN.md` and `project/specs/` in autonomous edit/verify loops while treating `project/` as strictly read-only, then writes a fresh `INSPECTION.md` at the repository root.
- **Reviewer** (`.ai/agents/reviewer.md`) — performs an adversarial review of the coder's branch work against `project/PLAN.md`, `project/specs/`, `INSPECTION.md`, and the governing files; enforces the hard gate that the coder did not modify `project/`; and, if a send-back is needed, leads an in-branch mini-planning session with the human to update `project/` and append a rework addendum to `project/PLAN.md`.

## Artifacts and Lifecycles

- **Unbranched strategic files** (`project/CONSTITUTION.md`, `project/CONVENTIONS.md`, `project/ROADMAP.md`, `project/ARCHITECTURE.md`, `project/adr/`): Evolved continuously as understanding matures. `ARCHITECTURE.md` is backed by ADRs (maintained via `manage-adr`). `ROADMAP.md` is pruned on sight as items are delivered or abandoned.
- **Living domain specifications** (`project/specs/<domain>.md`): One file per core domain, separated using the `decompose-domains` skill (state ownership, autonomy, vocabulary, and lifetime tests). Each spec describes how its domain behaves right now with no palimpsest. Modified directly on a feature branch during planning (and during send-back re-planning) alongside `project/PLAN.md`.
- **Branch-ephemeral files** (`project/PLAN.md` and root `INSPECTION.md`): Created on a feature branch to drive and verify a single narrow increment, and deleted when the branch merges.
- **Merge archive** (`project/CHANGELOG.md` and Git history): Updated once per branch merge with a single entry summarizing delivered behavior. Git history serves as the archive for all pruned roadmap items and superseded states.

---

## Flow 1: Standard Increment (Pass on First Review)

### 1. Unstructured Discovery & Strategy Updates (No Branch)
The human and the **Planner** explore ideas in an open-ended conversation.
- Cross-cutting changes to `CONSTITUTION.md`, `CONVENTIONS.md`, `ROADMAP.md`, or `ARCHITECTURE.md` (with new or superseded ADRs via `manage-adr`) are applied directly on the base branch.
- Obsolete roadmap topics are deleted immediately.
- If the human's vision spans multiple domains or a large body of work, the Planner uses `decompose-domains` to separate the domain boundaries and parks future slices in `project/ROADMAP.md` so each branch stays narrow enough to execute cleanly without model confusion or hard-to-isolate bugs.

### 2. Chambering the Increment (Feature Branch Created)
When the human and **Planner** agree on the next narrow increment:
1. The Planner creates a new feature branch.
2. On the branch, the Planner directly edits `project/specs/` to describe the desired behavior.
3. The Planner writes `project/PLAN.md` detailing the implementation steps to bring the codebase into alignment with the updated specifications.
4. The Planner commits the `project/` changes to the feature branch.

### 3. Autonomous Implementation (Coder)
The human starts a fresh **Coder** session on the feature branch.
1. The Coder reads `project/PLAN.md`, the updated domain specs in `project/specs/`, and the governing files (`CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md`).
2. Checking the commit history from the branch fork point, the Coder sees this is the initial implementation pass.
3. Without ever modifying `project/`, the Coder implements and verifies the changes iteratively until `project/PLAN.md` and `project/specs/` are satisfied, then commits the implementation.
4. The Coder writes `INSPECTION.md` from scratch at the repository root with manual verification steps, self-verification evidence, and proposed `CHANGELOG.md` additions, then hands control back to the human.

### 4. Adversarial Review & Human Verification (Reviewer + Human)
While the human runs manual testing using `INSPECTION.md`, the **Reviewer** audits the branch:
1. Checks the branch commit history to confirm the hard gate: `project/` was not modified after the Planner's initial commit on the branch.
2. Diffs the branch against the base branch and audits the implementation and `INSPECTION.md` against `project/PLAN.md`, `project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. Reports a **Pass** verdict to the human.

### 5. Merge & Cleanup (Human)
1. The human appends the single branch entry from `INSPECTION.md` into `project/CHANGELOG.md`.
2. The human deletes `project/PLAN.md` and `INSPECTION.md`.
3. The feature branch is merged into the base branch.

---

## Flow 2: Increment with a Send-Back (Including Substantive `project/` Changes)

Steps **1 through 3** happen exactly as in Flow 1: strategy is updated, a feature branch is created with updated specifications in `project/specs/` and `project/PLAN.md`, and the **Coder** implements the first pass and generates `INSPECTION.md`.

### 4. Adversarial Review Uncovers a Deeper Issue (Reviewer + Human)
The human runs manual verification alongside the **Reviewer**'s adversarial audit. Together they discover that the increment cannot be merged as-is—not merely because of a coding mistake, but because seeing the working attempt reveals a deeper problem:
- A domain boundary in `project/specs/` was tangled (for example, two domains needed to mutate the same state, or a shared term meant different things in two contexts),
- A desired behavior in the spec needs substantive refinement,
- An architectural constraint in `ARCHITECTURE.md` (and its backing ADR) or a rule in `CONVENTIONS.md` needs adjustment, or
- The remaining delta needs to be re-scoped and run with a stronger model.

### 5. In-Branch Mini-Planning Session (Reviewer + Human)
Instead of switching back to the Planner or abandoning the branch, the human conducts a mini-planning session directly with the **Reviewer**, who already holds the adversarial mindset and the code review context:
1. **Substantive `project/` updates**: Anything the Planner can do between branches can be done here on the feature branch. With the human's agreement, the Reviewer updates the affected files in `project/`—for example:
   - Modifying or splitting domain specifications in `project/specs/` (applying the `decompose-domains` skill if domain boundaries shift),
   - Updating `ARCHITECTURE.md` and creating or superseding an ADR via `manage-adr`,
   - Refining `CONVENTIONS.md` or `CONSTITUTION.md`, or moving deferred scope into `ROADMAP.md`.
2. **Plan rework addendum**: The Reviewer appends a rework addendum to `project/PLAN.md` explaining why the increment was sent back and what must be addressed to match the revised `project/` files.
3. **Commit `project/`**: The Reviewer commits all `project/` changes on the feature branch (after the earlier creation of `INSPECTION.md`), establishing the new baseline for the coder.

### 6. Rework Pass (Fresh Coder Session)
The human invokes a fresh **Coder** session (selecting a different or higher-capability model if warranted):
1. The Coder inspects the branch commit history from the fork point, sees the existing implementation commits followed by the Reviewer's send-back commit to `project/`, and recognizes it is continuing work on an existing feature branch after a send-back.
2. The Coder reads the updated `project/` files (`project/specs/`, `ARCHITECTURE.md`, `CONVENTIONS.md`, `CONSTITUTION.md`) and `project/PLAN.md` including the new rework addendum.
3. Keeping `project/` strictly read-only, the Coder reworks the implementation iteratively until the revised specs and plan addendum are satisfied, and commits the code changes.
4. The Coder regenerates `INSPECTION.md` completely from scratch so it reflects the full, updated branch increment (never appending history).

### 7. Re-Review & Merge (Reviewer + Human)
1. The **Reviewer** runs again on the branch, sees from the commit history that this is a review subsequent to a send-back modification to `project/`, and verifies the hard gate: `project/` was not modified since the most recent commit to `project/` after the previous `INSPECTION.md`.
2. The Reviewer audits the updated code and newly regenerated `INSPECTION.md` against the revised `project/specs/`, `project/PLAN.md` (and its addenda), `ARCHITECTURE.md`, `CONVENTIONS.md`, and `CONSTITUTION.md`.
3. If further iteration is needed, Steps 5–7 repeat. Once the Reviewer reports **Pass** and manual verification succeeds, the human folds the branch's work into a single entry in `project/CHANGELOG.md`, deletes `project/PLAN.md` and `INSPECTION.md`, and merges the branch.
