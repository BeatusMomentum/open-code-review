# Viewer UI redesign — align `ocr viewer` with the new design system

## Background

`ocr viewer` already serves a working, read-only web UI from `internal/viewer/`
(server-rendered Go `html/template` + `static/style.css` + a little vanilla JS). It
covers all four screens — Repositories, Sessions, Session detail, and Compare — with
theming, search, pagination, comment filters and marked/hidden toggles already in place.

We now have a set of design mockups that give these screens a consistent, polished visual
language (refined tables, spacing, typography, a proper app header/wordmark, a shared icon
set, and cleaned-up light **and** dark themes). This is a **visual redesign of the existing
viewer**, not a rewrite: routes, data model, CSP/security posture and Go handlers stay as
they are — we are restyling templates, CSS and static assets to match the mockups.

## Goal

Bring every viewer screen in line with the mockups while keeping the viewer read-only,
CSP-safe and server-rendered.

## Scope & sub-issues

Foundational (land first):
- [ ] #1320 — Design tokens & app header/wordmark (light + dark)
- [ ] #1321 — Shared SVG icon set integration

Per-screen (parallelizable after the foundation):
- [ ] #1322 — Repositories page
- [ ] #1323 — Sessions list page
- [ ] #1324 — Session detail: header / meta bar
- [ ] #1325 — Session detail: Coverage & Token Usage
- [ ] #1326 — Session detail: Review Comments
- [ ] #1327 — Session detail: Files Reviewed, Session Tasks & Conversations
- [ ] #1328 — Compare page

Polish (last):
- [ ] #1329 — Responsive, accessibility & template/visual tests

## Design fidelity vs. current features

The mockups were produced during active development, so the live viewer has features that
post-date them or aren't drawn (e.g. session compare, per-file token breakdown, back
navigation). Guiding rule:

- **Keep every existing feature.** The redesign is visual — do not drop functionality that
  isn't in a mockup.
- **Where a mockup exists, match it.** Where it doesn't, style the feature to the mockup's
  visual language (tokens, tables, badges, spacing from #01/#02) so it stays consistent.
- **Resolve specifics in the PR.** Small layout/wording ambiguities are expected; settle
  them during review rather than blocking on a pixel-perfect spec.

## Design assets

Mockups for this effort (light + dark): Repositories, Sessions, and Session detail, plus the
24×24 icon set. They are attached to the relevant sub-issues.

## Non-goals

- No change to the viewer's routes, JSON/data model, or read-only guarantee.
- No migration to a client-side SPA framework — the viewer stays server-rendered Go
  templates.
- No relaxation of the Content-Security-Policy or the Host-header allowlist
  (`internal/viewer/securityheaders.go`, `hostguard.go`).

## Key files

- Templates: `internal/viewer/templates/{repos,sessions,session,compare}.html`
- Styles: `internal/viewer/static/style.css` (design tokens live in `:root`)
- Scripts: `internal/viewer/static/{repos,session}.js`
- Asset embedding & template funcs: `internal/viewer/server.go`

## Conventions for contributors

- Disclose AI/LLM usage in your PR and which tools/models you used (AGENTS.md).
- Keep all UI copy in English; add SPDX headers to new files (`make license-add`).
- Run `make check` and `make test`; the project enforces 90% coverage (`make coverage`).
- Respect the CSP: no inline scripts/handlers; externalize JS into `static/` and wire via
  data attributes + a single addEventListener bootstrap (see PR #758 for the pattern).

## How to pick this up

Comment on a sub-issue to claim it. Start from the mockup for that screen and compare
against the live viewer (`ocr viewer`). Foundation issues (#01, #02) unblock the rest.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
