---
name: manage-ai-capabilities
description: Maintains the project's DRY AI capability layer. Agent and skill behavior lives in .ai/ as the single source of truth, mirrored into the .claude/, .github/, and .opencode/ routing stubs; the project tailors roles only below each file's boundary line, which a graft preserves while replacing the template-owned text above. Use when the project wants to change agent or skill behavior, or when checking for drift between .ai/ and the vendor stubs.
---

Routing stub. Read and follow the vendor-neutral instructions in `.ai/skills/manage-ai-capabilities.md`. Do not duplicate those instructions here.
