# Viewer redesign: integrate the shared SVG icon set

> Part of the viewer UI redesign (see #1319). **Foundation — land first.**

## Summary

Add the UI icons the redesign mockups use to the viewer as offline, CSP-safe SVGs, and wire
them into the templates. **Re-scoped 2026-09-17** — see the correction below; the original
"rename and integrate seven exported SVGs" framing was based on a mislabeled export.

## Correction to the original scope

The exported design set (`容器 4*.svg`) turned out to be a **single brand/logo mark in
black/white variants — not seven distinct icons** (all seven share identical path geometry).
That brand mark is **already integrated** in #1338 (inlined as `.brand-icon` in
`static/style.css`). So there is no seven-icon set to rename.

What the mockups actually need is a small set of **five UI glyphs**. They have been sourced
from **[Ant Design Icons](https://github.com/ant-design/ant-design-icons) (MIT)** — the same
set the design reference renders — and are provided here, normalized to `fill="currentColor"`
and ready to embed:

📁 https://github.com/alibaba/open-code-review/tree/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/icons

| File | Used for |
|------|----------|
| `chevron-left.svg` | back navigation; pagination "previous" |
| `chevron-right.svg` | collapsed section toggle; pagination "next" |
| `chevron-down.svg` | expanded section toggle |
| `search.svg` | repositories search box |
| `settings.svg` | settings / theme control |

## Scope

- [ ] Copy the five SVGs into `internal/viewer/static/icons/`.
- [ ] Extend the `//go:embed` directive in `internal/viewer/server.go` to include the icons dir; confirm they serve under `GET /static/…`.
- [ ] Render them CSP-safe — inline `<svg>` via a template partial, or `<img src="/static/icons/…">`; prefer a form where `currentColor` works so icons adapt to light and dark.
- [ ] Replace the current ad-hoc glyphs/unicode in the templates (back nav, collapse/expand toggles, search, pagination) with these icons.
- [ ] Add MIT attribution for Ant Design Icons in `internal/viewer/static/icons/` (a short `NOTICE`/`README`); do **not** add the project's Apache SPDX header to the third-party SVGs.
- [ ] Update/extend viewer tests as needed; keep the read-only route contract (`TestMux_HasNoWriteRoutes`) and the CSP/security-header tests green.

## Non-goals

- The brand/logo mark (already shipped in #1338).
- The remote iconfont `<script>` and the `antd` runtime from the reference — **must not** be introduced (CSP + offline + bundle size).
- Per-screen layout changes (owned by the per-screen issues).

## Parallelization & conflicts

Foundational — land alongside/after #1320 and before the per-screen issues. Mostly adds new
files (icon assets + a render partial) plus one `//go:embed` line and small template edits, so
it rarely conflicts with the screen work.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
