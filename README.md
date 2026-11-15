# SDD Template

A spec-driven development (SDD) scaffold. This repository is a **template, not a project**: it holds the common governing text and AI capability layer that any project adopting an SDD workflow needs, and omits everything project-specific.

## Creating a New Project from This Template

1. **Copy the scaffold into your new project directory, excluding `.git/`, this `README.md`, and `TEMPLATE-CHANGELOG.md`:**
   - Copy everything else in this repository into your new project root.
2. **Initialize your project's own repository and README:**
   - Run `git init` in your new project root to create a fresh `.git/` directory.
   - Create a new `README.md` that describes your project.
3. **Bootstrap and run the project with the `planner` agent:**
   - Start a session with the `planner` agent and work through your vision together to populate `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md` (with backing ADRs in `project/adr/`), `ROADMAP.md`, and your initial domain specifications in `project/specs/`.
   - Chamber your first increment on a feature branch (such as scaffolding your toolchain, test runner, linters, and CI mechanisms) into `PLAN.md`, then follow [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md) through coding, adversarial review, rework (when needed), and merge.

## Updating a Project Built from This Template

Projects instantiated from this template graft improvements from the current template. The template is semantically versioned: `SDD-WORKFLOW.md` carries the version in its frontmatter and travels with every graft, and `TEMPLATE-CHANGELOG.md` in this repository records what each release delivers. The protocol ships with the scaffold: see **Grafting Template Updates** in [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md).

## What Is Included

- `AGENTS.md` — the entry point: steers any AI session into the workflow before work starts.
- `CLAUDE.md` & `.github/copilot-instructions.md` — entry-point routing stubs pointing to `AGENTS.md`.
- `project/` — the governing and specification layer:
  - `CONSTITUTION.md` — root governance and safety guardrails.
  - `CONVENTIONS.md` — tactical coding, directory, naming, and tool rules.
  - `ARCHITECTURE.md` & `adr/` — current system design, backed by indexed Architecture Decision Records (`ADR`s).
  - `specs/` — living domain specifications (`one file per domain`), describing how each core domain currently behaves.
  - `ROADMAP.md` — pruned, living view of upcoming and active work.
  - `CHANGELOG.md` — reverse-chronological record of merged branch increments.
  - `PLAN.md` (ephemeral, on feature branches only) — scopes the current branch increment.
- `.ai/` — the vendor-neutral AI core: three agents (`planner`, `coder`, `reviewer`) and three skills (`commit`, `manage-adr`, `manage-ai-capabilities`).
- `.claude/`, `.github/`, `.opencode/` — harness routing stubs pointing to `.ai/` so behavior is defined in one place.
- `SDD-WORKFLOW.md` — end-to-end guide to the SDD lifecycle, both with and without a rework loop.
- `INSPECTION.md` (ephemeral, generated at the repository root on feature branches) — handover verification protocol, test evidence, and proposed changelog entry produced by the coder.

## Invariants vs. Mechanisms

The template rests on one split:

- **Invariants** (included here) — workflow rules that hold for every project regardless of language or domain: who may write which files, file lifecycles, domain boundary tests, branch-scoped planning, phase handover, adversarial review and in-branch rework re-planning, ADR indexing and supersession, pruning over archiving, and no palimpsest.
- **Mechanisms** (supplied by your project) — how invariants are enforced in a specific stack: tests, CI gates, linting, smell detection, and harness permission rules.
- **Deliberately unsolved** — release management for parallel work. Domain boundaries are chosen so work on separate domains *can* proceed independently, but coordinating concurrent branches, merge order, and release sequencing is left to your project.

## Contributing Back to This Template

Improve this template with changes that are domain-independent and benefit any project:

- Sharpens a workflow invariant or a rule for maintaining the invariant layer (`manage-adr`, `manage-ai-capabilities`, pruning, no palimpsest).
- Does not bake in stack-specific mechanisms or dogmatic methodology opinions.
