---
name: bun-windows-dev
description: Develop opencode on Windows with Bun. Use when running, testing, or debugging the repo on Windows, or when writing shell commands and scripts that must work in PowerShell.
---

# Bun Windows Dev

Shell commands in this environment run under PowerShell, not bash.

## Shell Rules

- Chain commands with `;`, not `&&` or `||`.
- Do not use `head`, `tail`, `grep`, `timeout`, or `which`. Prefer `Out-String -Width`, `Select-Object -First`, or dedicated file tools.
- Quote paths with spaces. Prefer `$HOME` over `~` in scripts.
- `git` prints progress to stderr; PowerShell surfaces that as errors. Pipe informational output with `| Out-String -Width <n>` and treat exit code 1 with full file progress as success.

## Bun on Windows

- Required: Bun 1.3+ (`bun --version`). Install via `winget install --id Oven-sh.Bun -e`.
- Run package scripts from the repo root with `bun run --cwd <package> ...`, e.g. `bun run --cwd packages/opencode src/index.ts --help`.
- Run package tests from the package directory, never from the repo root.
- `node-pty` is patched postinstall (`bun run --cwd packages/core fix-node-pty`); if TUI input behaves oddly on Windows, rerun `bun install`.

## Watch Out

- Native modules and symlinks may need Developer Mode or admin rights.
- Line endings: do not convert LF files to CRLF. Check `.gitattributes` before touching shared scripts.
- Windows-only failures belong in the issue with the `windows` team label (see `.opencode/agent/triage.md`).
