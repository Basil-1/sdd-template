# Constitution

## Purpose

Root governance. Defines the architectural laws and safety guardrails. All agent behavior must conform to this file.

## Laws

Violating a law is a defect regardless of outcome.

1. `.project/` is read-only during execution. Only the Planner agent or the human may edit it, and only during a planning session.
2. Every architectural decision is recorded as an ADR under `.project/adr/`. 
3. `ARCHITECTURE.md` and `CONVENTIONS.md` may state only rules supported by an ADR. 
4. `.ai/` is the single source of truth for agent and skill behavior. Vendor folders (`.claude/`, `.github/`, `.opencode/`) hold only routing stubs.
5. Execution artifacts (`PLAN.md`, `INSPECTION.md`) are ephemeral. They are never committed as permanent state.
