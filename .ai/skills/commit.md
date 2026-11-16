---
name: commit
description: The commit protocol for every agent, in any identity, branched or not — message economy, attribution trailers, privacy allowlist.
---

# commit

## Message

Unless superseded by the Reviewer's merge protocol or a direct human request, give a commit the smallest possible low-entropy narrative: a subject naming the change, plus a body only when it holds metadata of durable value beyond what the diff shows — the why, a decision, a caveat.

## Attribution Trailers

End every commit message with a trailer block — blank line before it, one `Key: value` per line — stating what the harness actually exposes:

- `Agent:` the identity you run as — `planner`, `coder`, `reviewer`, or `basic` for none of the three.
- `Harness:` the agent harness you run in.
- `Model:` the model you run on.
- `Human:` the initials of the human you act for, when the harness identifies them.

Extract, never invent. Omit any trailer you cannot determine from your own context. Add no others — merge commits add `Branch:` per the Reviewer's merge protocol.

## Privacy Allowlist

Commits can become public. State only the four trailer values above — never hostname, username, operating system, hardware, file paths, or environment details. Never write human information into the repository to feed these trailers; what the harness does not know is left out.

<!-- GRAFT BOUNDARY: template-owned above, project-owned below. Do not edit or remove this line. -->

## Project Customizations

<!-- Add project-specific customizations below. -->
