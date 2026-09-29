---
name: solid-ui-review
description: Review UI contributions to the TUI, web app, or desktop app. Use when implementing or reviewing SolidJS components, opentui layouts, or shared UI in packages/app.
---

# Solid UI Review

Core pieces (see `CONTRIBUTING.md`): `packages/opencode/src/cli/cmd/tui/` (TUI, SolidJS + opentui), `packages/app` (shared web UI, SolidJS), `packages/desktop` (Electron wrapper).

## Checklist

- Keep components small and colocated with their styles. Reuse `packages/app` shared components instead of duplicating markup in web and desktop.
- Respect direction: use logical CSS (`padding-inline-start`, `inset-inline-end`, `text-align: start`). See the `rtl-aware-development` skill.
- Keep logic out of views: decode input and call services at the boundary; put business rules in services, mirroring the Effect skill's thin-handler rule.
- No `any`, no non-null assertions to silence the type checker. Prefer precise types.
- Avoid `else` chains and unnecessary destructuring, per the PR style preferences in `CONTRIBUTING.md`.

## Verify

- UI PRs must include before/after screenshots or video.
- Test with `bun run --cwd packages/app dev` against a running server (`bun dev serve`), plus the TUI path if the change touches `cmd/tui`.
- Cover both LTR and forced-RTL rendering for layout changes.
