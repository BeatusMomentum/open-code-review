# Viewer redesign: integrate the shared SVG icon set

> Part of the viewer UI redesign (see main tracking issue). **Foundation — land first.**

## Summary

Add the exported 24×24 SVG icons to the viewer's embedded static assets and wire them into
the templates as a consistent icon system, replacing ad-hoc glyphs/emoji.

## Design reference

The mockups use a small, uniform icon set (24×24) for the brand mark, back navigation,
search, status/action affordances, etc. Source assets: 7 SVG icons from the design export
(bundled as `assets/icon-1.svg` … `assets/icon-7.svg`).


> Note: the raw export names them all `容器 4*.svg` ("container" placeholder names) and a
> quick check shows overlapping path data — confirm on the Figma side what each icon is, then
> rename to meaningful English names as part of this issue.

## Current state

- Icons today are inconsistent (inline unicode/emoji or none). Assets are embedded via
  `//go:embed templates/*.html static/style.css static/session.js static/repos.js` in
  `internal/viewer/server.go`.

## Scope

- [ ] Rename the exported SVGs to meaningful English names (e.g. `icon-back.svg`,
      `icon-search.svg`, `icon-logo.svg`, …) and place them under
      `internal/viewer/static/icons/`.
- [ ] Extend the `//go:embed` directive in `server.go` to include the new icon dir, and
      confirm they are served under `GET /static/…`.
- [ ] Provide a CSP-safe way to render icons (inline `<svg>` via a template partial, or
      `<img src="/static/icons/…">`). Prefer inline `<use>`/symbol sprite or a template
      helper so `currentColor` works in both themes.
- [ ] Document the icon inventory (name → usage) in a short comment or the partial.

## Out of scope

- Applying icons to each screen's final layout (done incrementally in #03–#09; this issue
  lands the assets + rendering mechanism and swaps the obvious ones like back/search/logo).

## Acceptance criteria

- Icons render in light and dark, inheriting color where appropriate.
- No CSP violations (check the browser console; the viewer sets strict headers in
  `internal/viewer/securityheaders.go`).
- `make check` and `make test` pass; SVGs added to `.gitattributes` if needed for line
  endings, SPDX added where applicable.

## Notes

- Keep SVGs small; strip editor cruft/`<defs>` bloat from the Figma export.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
