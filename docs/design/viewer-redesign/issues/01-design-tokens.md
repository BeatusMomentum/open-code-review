# Viewer redesign: design tokens & app header/wordmark (light + dark)

> Part of the viewer UI redesign (see main tracking issue). **Foundation — land first.**

## Summary

Refresh the viewer's design tokens and add the "Open Code Review Viewer" app header so
every screen shares one visual language before the per-screen work begins.

## Design reference

All mockups share a top-left brand lockup ("⬡ Open Code Review Viewer") and a consistent
palette/typography in both light and dark. See the light and dark variants of the session
mockup for the target colors, surface elevations and text hierarchy.

## Current state

- Tokens already exist in `internal/viewer/static/style.css` `:root` (`--bg`, `--radius`,
  `--radius-sm/-xs`, `--font`, …) with a `@media (prefers-color-scheme: dark)` block.
- There is no persistent app header/wordmark across pages today.

## Scope

- [ ] Consolidate and expand the token set to match the mockups: surface/background layers,
      border, text primary/secondary/muted, accent (the green used for `Check`/links),
      severity colors, spacing scale, radii, shadows — defined once for light and dark.
- [ ] Add a shared header partial (wordmark + logo) rendered on every page; extract into a
      template block reused by `repos`, `sessions`, `session`, `compare`.
- [ ] Keep the existing `prefers-color-scheme` behavior; do not add a JS theme toggle in
      this issue (can be a follow-up).
- [ ] Ensure contrast passes WCAG AA for body text and the accent-on-surface combinations.

## Out of scope

- Per-screen layout changes (owned by #03–#09).
- The icon assets themselves (#02).

## Acceptance criteria

- Light and dark render cleanly with the new tokens; no hard-coded colors left inline in
  templates for the shared chrome.
- The app header appears identically on all four screens.
- `make check` and `make test` pass.

## Notes

- Header markup must be CSP-safe (no inline styles/scripts).
- New files need SPDX headers (`make license-add`).

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
