# Changelog

## Purpose

Reverse-chronological record of completed increments. Written for humans to answer "what changed and when." Updated only on branch merge.

## Format

One section per increment, newest first:

```
## <date> — <short title>

- <change> (<ADR ref> where relevant)
```

## Rules

- Entries describe delivered behavior, not intent.
- Update only at merge. Do not edit during execution.
- At merge, append the entries proposed in `INSPECTION.md`, then delete `INSPECTION.md`.
- One entry per branch: all changes from a branch fold into a single entry at merge.

## History

<!-- Empty until the first merge. -->
