# SDD Template

A harness vendor-neutral, light, zero-dependency, and updateable spec-driven development workflow scaffold for projects built with AI agents.

Starting a project with an AI framework is easy; keeping it coherent six months later is not. Markdown context piles up and drifts out of date, and answering a simple question forces your agent to wade through history. Documentation should be living, describing how a system works right now. Archaeological history belongs in git and the docs on `main` should always read as if the project were designed that way from day one.

- **Vendor-neutral:** Switch between the three supported harnesses freely. All agent definitions, skills, and rules live once in `.ai/`, and the harnesses all use that single source of truth.
- **Light and zero-dependency:** No CLI to install, no background daemon, and no stack opinions smuggled into your repository.
- **Updatable:** If a newer version of SDD Template has something you want, you can easily graft it in with confidence that you have the whole thing and didn't squash your customizations.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Requirements

You need git and one of the supported harnesses: OpenCode V2, Claude Code, or GitHub Copilot.

## Quickstart on a fresh project

1. Get the whole repo minus the template files `.git/`, `README.md`, `TEMPLATE-CHANGELOG.md`, and `CONTRIBUTING.md` into your project. You can click **Use this template** on GitHub so your repo starts with a clean first commit and delete those three files, or clone the repo and copy everything else over.
2. `git init` (if cloning) and write your own `README.md`.
3. Open a session with the `planner` agent and work through the vision together to populate the initial strategy artifacts.
4. Chamber your first increment into `PLAN.md`. Follow [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md) through coding, adversarial review, rework, and squash-merge.

## Strategy artifacts

Strategy artifacts are the written state of the project's present and future, stored in `project/`:

- `CONSTITUTION.md` and `CONVENTIONS.md` set the laws and tactical standards every agent obeys.
- `ARCHITECTURE.md` plus `adr/` capture the current design and the decisions behind it.
- `ROADMAP.md` tracks ambition; `specs/` holds one living specification per domain, describing how it behaves now.
- `CHANGELOG.md` records delivered increments.

## How it works

- The Planner evolves strategy on the base branch and chambers each increment on a feature branch by updating domain specs and writing `PLAN.md`.
- The Coder builds against that plan, writing `INSPECTION.md` when finished or `BLOCKED.md` if it hits a problem.
- The Reviewer audits the branch adversarially, triggers in-branch rework addendums if something misses, and squash-merges once everything passes.

Full details, including the rework loop and subagent delegation rules, live in [`SDD-WORKFLOW.md`](SDD-WORKFLOW.md).

## What this includes (and doesn't)

The template enforces workflow invariants that hold regardless of your language or stack. Your project supplies the enforcement mechanisms for your specific stack, including test suites, CI gates, linters, harness configs, and parallel release management.

## Upgrading existing projects

Each release is tagged and tracked via `template_version` in `SDD-WORKFLOW.md` frontmatter. When a newer version drops, run a plain agent session (outside the three workflow roles) with [`GRAFT.md`](GRAFT.md) to pull template updates into an existing project without touching your project-owned content.

## License

MIT. See [LICENSE](LICENSE). You can copy, modify, and use this scaffold in commercial or private projects as long as you keep the copyright and permission notice with the copied files. Your application code gets whatever license you want.