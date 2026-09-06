# CLAUDE.md — DiscVault Plugins

Instructions for Claude Code (and any AI agent) working in this repository.

## About this repository

Audited, standalone plugins for DiscVault 26. Source, tests, checksums and reproducible
release packaging live together here, with `catalog.json` describing what is published.

## Branches

`main` is the integration branch and there is no promotion model here. Branch feature and
fix work off `main`, open a pull request into `main`, and never commit to `main` directly.
The pre-commit hook in `.githooks/` runs before every commit.

## A plugin change is not done when the code passes

A plugin is a contract with an external system, so every new plugin and every behavioural
version bump carries its documentation in the same change set — and that documentation
lives in App-Guidance, not here.

- **A new plugin** needs an entry covering its purpose, the source it speaks to, and its
  precedence against the plugins answering the same question.
- **A version bump** needs an entry only when behaviour a reader depends on changed: a new
  field, a changed precedence, a different upstream. A routine fix is release-notes
  material.
- **A packaged artefact is a release step, not a substitute.** Shipping a new zip without
  repointing whatever pins the version leaves every installation on the old one.
- Say in the pull request body what you recorded, or that you judged the change
  documentation-neutral. An unexplained silence is not the same as "nothing to record".

## The shared instructions live in App-Guidance

The engineering guidance for every Flux76 project lives in
**[`Flux76HQ/App-Guidance`](https://github.com/Flux76HQ/App-Guidance)**, not in this
repository. Read it before starting work here; this file records only what is specific
to this repo.

| What you need | Where it is |
|---|---|
| The enforceable baseline — versioning, CI guardrails, secrets, release discipline, PR workflow | [`shared/guidelines/project-baseline.md`](https://github.com/Flux76HQ/App-Guidance/blob/main/shared/guidelines/project-baseline.md) |
| Which document leads per domain, and where that document lives | [`AUTHORITY.md`](https://github.com/Flux76HQ/App-Guidance/blob/main/AUTHORITY.md) |
| How to work inside App-Guidance itself (branch, PR, when the `VERSION` bump applies) | [`CLAUDE.md`](https://github.com/Flux76HQ/App-Guidance/blob/main/CLAUDE.md) |
| DiscVault specs, the normative sync contract, and cross-repo change specs | [`projects/discvault/`](https://github.com/Flux76HQ/App-Guidance/tree/main/projects/discvault) |

Two baseline rules apply here from the first commit, so they are worth naming rather
than leaving to be discovered:

- **A new feature gets a fresh worktree and a separate session**
  ([§16](https://github.com/Flux76HQ/App-Guidance/blob/main/shared/guidelines/project-baseline.md#16-feature-work-gets-its-own-workspace-and-its-own-session)).
  One feature, one workspace, one session. A checkout is on one branch at a time, so two
  features in one directory share a working tree and an index, and the first `git add -A`
  mixes them into a single commit that nothing can separate afterwards. Say so *before*
  the first edit, not after. It is a warning, not a veto, and it is about features — a
  fix, a refactor or a chore inherits the workspace it is given.
- **An agent carries its own PR to merge**
  ([§8](https://github.com/Flux76HQ/App-Guidance/blob/main/shared/guidelines/project-baseline.md#8-agent-pull-requests-standing-authorisation-to-merge)).
  Standing authorisation across every Flux76 repository, bounded and revocable: watch the
  PR, drive failing checks to green, merge once every check passes — without asking again
  at the green light. "All green" is the condition, not a formality.

**Precedence.** On anything shared — versioning, CI, secrets, the PR workflow, the
DiscVault contracts — App-Guidance leads and this file must not contradict it. On this
repository's own branch topology, build and release flow, this file leads. When a session
settles something that outlives its own PR — a contract between systems, an ownership or
precedence rule, a deliberate policy and why — write it up in App-Guidance in the same
change set, on a branch and through a pull request, never straight onto its `main`.
