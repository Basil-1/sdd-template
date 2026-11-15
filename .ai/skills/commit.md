---
name: commit
description: The standard git commit protocol for every agent making any commit, in any identity (Planner, Coder, Reviewer, or basic agent), branched or not. Use whenever committing. Governs commit message narrative, attribution trailers, and the privacy allowlist.
---

# commit

## Purpose

One protocol for every agent commit, so history is cheap to read and honestly attributed.

## Message

Unless superseded by the Reviewer's merge protocol or a direct human request, give a commit the smallest possible low-entropy narrative: a subject naming the change, plus a body only when it holds metadata of durable value beyond what the diff already shows — the why, a decision, a caveat. Never restate the diff; never pad.

## Attribution Trailers

End every commit message with a trailer block — blank line before it, one `Key: value` per line — stating what the harness you run in actually exposes:

- `Agent:` the identity you are running as — `planner`, `coder`, `reviewer`, or `basic` when operating under none of the three personas.
- `Harness:` the agent harness you run in.
- `Model:` the model you run on.
- `Human:` the initials of the human you act for, when the harness identifies the logged-in human.

Extract, never invent. Omit any trailer whose value you cannot determine from your own context. Add no other trailers — merge commits add `Branch:` per the Reviewer's merge protocol in `.ai/agents/reviewer.md`.

## Privacy Allowlist

Commits can become public. Attribution may state only the agent identity, harness, model, and human initials as above — never anything about the machine or account: hostname, username, operating system, hardware, file paths, or environment details. Never write human information into the repository to feed these trailers; what the harness does not know is left out.

## Project Customizations

<!-- Add project-specific customizations below. -->
