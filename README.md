# SDD Template

A spec-driven development (SDD) scaffold. This repository is a **template, not a project**: it holds the common governing text and AI capability layer that any project adopting an SDD workflow needs, and omits everything project-specific.

## Creating a New Project from This Template

1. **Copy the scaffold into your new project directory, excluding `.git/` and `README.md`:**
   - Do **not** copy this repository's `.git/` folder or this `README.md`.
   - Copy `project/`, `.ai/`, `.claude/`, `.github/`, `.opencode/`, and `SDD-WORKFLOW.md` into your new project root.
2. **Initialize your project's own repository and README:**
   - Run `git init` in your new project root to create a fresh `.git/` directory.
   - Create a new `README.md` that describes your project.
3. **Instantiate the governing layer in `project/`:**
   - Write your project's root rules and guardrails in `project/CONSTITUTION.md`.
   - Write your coding standards, naming, and tooling rules in `project/CONVENTIONS.md`.
   - Document your initial architecture in `project/ARCHITECTURE.md` (recording architectural decisions under `project/adr/` via the `manage-adr` skill).
   - Seed `project/ROADMAP.md` with your initial goals, and add initial domain specifications in `project/specs/` as you begin planning.
4. **Add project-specific mechanisms:**
   - Add your language toolchain, test runner, linters, CI checks, and harness permissions alongside the scaffold.
5. **Run the workflow:**
   - Follow [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md) to move work from planning through coding, adversarial review, rework (when needed), and merge.

## What Is Included

- `project/` — the governing and specification layer:
  - `CONSTITUTION.md` — root governance and safety guardrails.
  - `CONVENTIONS.md` — tactical coding, directory, naming, and tool rules.
  - `ARCHITECTURE.md` & `adr/` — current system design, backed by indexed Architecture Decision Records (`ADR`s). Only `ARCHITECTURE.md` requires ADR backing.
  - `specs/` — living domain specifications (`one file per domain`), describing how each core domain currently behaves.
  - `ROADMAP.md` — pruned, living view of upcoming and active work.
  - `CHANGELOG.md` — reverse-chronological record of merged branch increments.
  - `PLAN.md` (ephemeral, on feature branches only) — scopes the current branch increment.
- `.ai/` — the vendor-neutral AI core: three agents (`planner`, `coder`, `reviewer`) and three skills (`decompose-domains`, `manage-adr`, `manage-ai-capabilities`).
- `.claude/`, `.github/`, `.opencode/` — harness routing stubs pointing to `.ai/` so behavior is defined in one place.
- `SDD-WORKFLOW.md` — end-to-end guide to the SDD lifecycle, both with and without a send-back loop.
- `INSPECTION.md` (ephemeral, generated at the repository root on feature branches) — handover verification protocol, test evidence, and proposed changelog entry produced by the coder.

## Invariants vs. Mechanisms

The template rests on one split:

- **Invariants** (included here) — workflow rules that hold for every project regardless of language or domain: who may write which files, file lifecycles, domain boundary tests, branch-scoped planning, phase handover, adversarial review and in-branch send-back re-planning, ADR indexing and supersession, pruning over archiving, and no palimpsest.
- **Mechanisms** (supplied by your project) — how invariants are enforced in a specific stack: tests, CI gates, linting, smell detection, and harness permission rules.

## Contributing Back to This Template

Improve this template with changes that are domain-independent and benefit any project:

- Sharpens a workflow invariant or a rule for maintaining the invariant layer (`decompose-domains`, `manage-adr`, `manage-ai-capabilities`, pruning, no palimpsest).
- Does not bake in stack-specific mechanisms or dogmatic methodology opinions.
