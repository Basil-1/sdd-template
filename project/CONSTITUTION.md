# Constitution

## Purpose

Root governance. Defines the architectural laws and safety guardrails. All agent behavior must conform to this file.

## Laws

1. `project/` is read-only during execution. Only the Planner agent or the human may edit it.
2. Every architectural decision is recorded as an ADR under `project/adr/`. 
3. `ARCHITECTURE.md` and `CONVENTIONS.md` must be completely supported by ADRs. 
4. `.ai/` is the single source of truth for agent and skill behavior. Vendor folders (`.claude/`, `.github/`, `.opencode/`) hold only routing stubs.
5. Execution artifacts (`project/PLAN.md`, `INSPECTION.md`) are ephemeral: they live until merge, when both are deleted. They are never committed as permanent state.
6. No palimpsest accretion: after each edit a file reads as if written fresh, never referring to an earlier state.
