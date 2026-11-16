# SDD Template

A spec-driven development (SDD) scaffold. This repository is a **template, not a project**: it holds the governing text and AI capability layer that any project adopting an SDD workflow needs, and omits everything project-specific.

## Creating a New Project from This Template

1. Copy the scaffold into your new project directory, excluding `.git/`, this `README.md`, and `TEMPLATE-CHANGELOG.md`.
2. `git init` in the new project root, and write a new `README.md` describing the project.
3. Start a session with the `planner` agent and work through the vision together to populate `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md` (with backing ADRs in `project/adr/`), `ROADMAP.md`, and your initial domain specifications in `project/specs/`. Then chamber your first increment (scaffolding the toolchain, test runner, linters, CI) into `PLAN.md` and follow [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md) through coding, adversarial review, rework, and merge.

## Updating a Project Built from This Template

Projects graft improvements from newer template versions. The template is semantically versioned: `SDD-WORKFLOW.md` carries the version in its frontmatter and travels with every graft, and `TEMPLATE-CHANGELOG.md` records what each release delivers. The protocol ships with the scaffold: see [`GRAFT.md`](GRAFT.md).

## What Is Included

- `AGENTS.md` — entry point: steers any AI session into the workflow before work starts. `CLAUDE.md` and `.github/copilot-instructions.md` route to it.
- `project/` — governing and specification layer: `CONSTITUTION.md`, `CONVENTIONS.md`, `ARCHITECTURE.md` with `adr/`, `specs/`, `ROADMAP.md`, and `CHANGELOG.md`.
- `.ai/` — the vendor-neutral AI core: agents `planner`, `coder`, `reviewer`; skills `commit`, `manage-adr`, `manage-ai-capabilities`. `.claude/`, `.github/`, and `.opencode/` hold routing stubs into it.
- `SDD-WORKFLOW.md` — roles, artifacts, and both flows. `GRAFT.md` — how projects adopt template updates, and versioning.
- Ephemeral, on feature branches only: `PLAN.md` scopes the increment; root `INSPECTION.md` carries the Coder's handover verification, test evidence, and proposed changelog entry.

## Invariants vs. Mechanisms

- **Invariants** (included here) — workflow rules holding for every project regardless of language or domain: who may write which files, file lifecycles, domain boundary tests, branch-scoped planning, phase handover, adversarial review and in-branch rework re-planning, ADR indexing and supersession, pruning over archiving, and no palimpsest.
- **Mechanisms** (supplied by your project) — how invariants are enforced in a specific stack: tests, CI gates, linting, smell detection, harness permission rules.
- **Deliberately unsolved** — release management for parallel work. Domain boundaries are chosen so separate domains *can* proceed independently, but coordinating concurrent branches, merge order, and release sequencing is left to your project.

## Contributing Back to This Template

Improve this template with changes that are domain-independent and benefit any project:

- Sharpens a workflow invariant or a rule for maintaining the invariant layer (`manage-adr`, `manage-ai-capabilities`, pruning, no palimpsest).
- Does not bake in stack-specific mechanisms or dogmatic methodology opinions.
