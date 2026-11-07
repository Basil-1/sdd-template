This project runs on spec-driven development. Read and follow [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md) before starting any work.

## Layout

- `project/` — the governing and specification layer; start with `project/CONSTITUTION.md`.
- `.ai/` — agent and skill definitions; the single source of truth for AI behavior.
- `.claude/`, `.github/`, `.opencode/` — harness routing stubs pointing into `.ai/`.

Discovery tools exclude dot-prefixed folders by default. Include hidden files (`hidden: true` / `--hidden`) when searching this layout, or use explicit paths.