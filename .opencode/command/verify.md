---
description: verify a change with typecheck, lint, and targeted tests
subtask: true
---

Run the verification loop for the current change before opening a PR.

Order matters: cheapest signal first.

1. Scope: only the touched packages. Never run package tests from the repo root.

## TYPECHECK

!`bun turbo typecheck --help`

## LINT

!`bunx oxlint --help`

## TESTS

!`git status --short`

Rules:

- `bun turbo typecheck` for the whole repo is slow; prefer the typecheck task filtered to touched packages when turbo supports it, otherwise run from the package directory.
- Run tests from the package directory (e.g. `packages/opencode`), using that package's existing Effect test helpers for service tests.
- If anything fails, report the failing package, command, and first error. Do not open a PR on red checks.
- PRs must reference an issue (`Fixes #123`) and follow the title prefixes in `CONTRIBUTING.md` (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`).
