# Viewer redesign: Repositories page

> Part of the viewer UI redesign (see #1319). Depends on #1320, #1321.

## Summary

Restyle the Repositories landing page (`GET /`) to match the mockup.

## Design reference

![Repositories mockup](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/repositories.png)

Page title "Repositories", a right-aligned "Search repositories"
input, and a table with columns **Repository | Sessions | Last Modified | Action** (green
`Check` link), with pagination at the bottom right.

## Current state

- Template: `internal/viewer/templates/repos.html`
- Script: `internal/viewer/static/repos.js` (client-side search; already externalized for
  CSP, see PR #758)
- Handler: `handleRepos` in `internal/viewer/handler.go`

## Scope

- [ ] Match header + search input styling and placement to the mockup.
- [ ] Restyle the table (column headers, row height, dividers, hover) to the new tokens.
- [ ] Style the `Check` action as the accent link/affordance.
- [ ] Align pagination control styling with the mockup.
- [ ] Preserve existing client-side search behavior and CSP compliance.

## Out of scope

- Backend/data changes (repo list already provided by the handler).

## Acceptance criteria

- Matches the mockup in light and dark.
- Search and pagination still work; no CSP console errors.
- `make check` and `make test` pass; add/adjust template tests as needed.

## Parallelization & conflicts

Depends on #1320/#1321. Owns `repos.html` + `repos.js`, so it runs in parallel with the other
screens (#1323, #1328). The only shared file is `static/style.css` — keep changes to the repos
section and rebase often.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
