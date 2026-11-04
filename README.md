# SDD Template

A spec-driven development (SDD) scaffold. This repository is a **template, not a project**: it holds the common governing text that any project adopting an SDD workflow needs, and deliberately omits everything project-specific.

## Invariants vs mechanisms

The design rests on one split:

- **Invariants** — rules about the workflow itself that hold for every project, regardless of domain: who may write which files, file lifecycles, JIT planning, phase handover, ADR indexing and compaction, pruning over archiving, no palimpsest, one entry per branch. These live in this template.
- **Mechanisms** — how an invariant is enforced in a specific project: tests, CI gates, linting, deterministic smell detection, TDD discipline, harness permission rules. These are project-specific.

The template states invariants; the instantiated project supplies mechanisms. That split is what keeps this scaffold language- and domain-agnostic.

## What is included, and why

- `.project/` — the strategic layer (`ROADMAP`, `CONSTITUTION`, `CONVENTIONS`, `ARCHITECTURE`, `CHANGELOG`, ADRs). Expresses the invariants a project's intent and rules must obey.
- `.ai/` — the vendor-neutral core: three agent personas (`planner`, `coder`, `reviewer`) and three shared skills (`manage_adr`, `generate_inspection`, `manage_ai_capabilities`). Expresses the workflow invariants as role instructions.
- `.claude/`, `.github/`, `.opencode/` — routing stubs only. Each carries that harness's required front matter and a pointer to the `.ai/` core, so behavior is defined exactly once.
- `PLAN.md` and `INSPECTION.md` are ephemeral runtime artifacts, intentionally not committed here; their lifecycle is documented inside the agent files.

## What is deliberately omitted

- Project-specific enforcement: TDD, hard gating, lint and smell detection, CI drift checks.
- Dogmatic methodology rules (TDD, agile, DDD as doctrine).
- Filled-in examples and sample content; each file describes its own structure instead.

Anything you add for your own project is an *instantiation*, not a template change.

## Using this template

1. Copy this scaffold into a new project repository. 
2. Instantiate: write your project's law into `CONSTITUTION.md`, `CONVENTIONS.md`, and `ARCHITECTURE.md`, and add your mechanisms (gates, tests, linting) alongside.
3. Follow the SDD lifecycle: JIT plan (`PLAN.md`) → execute → inspect (`INSPECTION.md`) → merge (changelog entry, roadmap prune).

## Contributing back

Improve this template with changes that are domain-independent and would benefit any project:

- It states or sharpens an invariant, or a rule for maintaining the invariant layer itself (ADR indexing, compaction, pruning, no-palimpsest).
- It is not a mechanism or a methodology opinion.
