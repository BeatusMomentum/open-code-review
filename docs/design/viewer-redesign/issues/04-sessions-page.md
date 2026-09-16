# Viewer redesign: Sessions list page

> Part of the viewer UI redesign (see main tracking issue). Depends on #01, #02.

## Summary

Restyle the per-repo Sessions list (`GET /r/{repo}`) to match the mockup.

## Design reference

![Sessions mockup](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/sessions.png)

A back chevron + title "Sessions: <repo>", and a table
with columns **Session ID | Branch | Mode | Model | Files | Status | Comments | Duration |
Started At | Action** (green `Check`), with bottom-right pagination.

## Current state

- Template: `internal/viewer/templates/sessions.html`
- Handler: `handleSessions` in `internal/viewer/handler.go`
- Back navigation exists (added in PR #1217).

## Scope

- [ ] Restyle the title row with the back-navigation chevron (use the icon from #02).
- [ ] Match the table columns, alignment, truncation (Session ID) and status styling.
- [ ] Style `Check` as the accent action; align pagination with the mockup.
- [ ] Keep column semantics identical to current data.

## Out of scope

- Session detail screen (#05–#08).

## Acceptance criteria

- Matches the mockup in light and dark; back nav and pagination work.
- `make check` and `make test` pass.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
